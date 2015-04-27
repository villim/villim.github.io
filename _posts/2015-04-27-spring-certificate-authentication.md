---
title: Spring Certificate Authentication
layout: post

---

## Outline
* Why Certificate
* Generate Certificates
* SSL configuration
* Spring Certificate Authentication

## Why Certificate?
After read [this article: What is a Digital Signature](http://www.youdzone.com/signature.html), it would be quite clear why we need certificate?

And read more about [SSL Handshake](http://www.ruanyifeng.com/blog/2014/09/illustration-ssl.html) 

In order to do Certificate Authentication, we have to make sure your Application Server working with SSL. But before that, we have to Generate Cetficates.

## Generate Certificates

We can using Keytool or Openssl to generate certificates. Here I will use Openssl. 

Want to know more Keytool commands, you can read more at [HERE](https://www.sslshopper.com/article-most-common-java-keytool-keystore-commands.html)

For using Openssl, read more at [How to create a self-signed SSL Certificate](http://www.akadia.com/services/ssh_test_certificate.html)

About Openssl, I encounter some problem with version 0.9.8, after research, it seems there's some defect their. I would suggest you upgrade to latest version. I upgraded to 1.0.1k.

Using the following Script, we will create self signed certificates for server and client.
{% highlight bash %}

    #!/bin/bash
 	PASSWORD=password
 	OUT_DIR=certs
 
	# Subject items
	C="Country"
	ST_CA="State"
	L_CA="Location"
	O_CA="Office"
	CN_CA="My CA Root"
	CN_SERVER="My Server"

	ST_CLIENT="Clinet State"
	L_CLIENT="Client Location"
	O_CLIENT="Client Office"
	CN_CLIENT="Client Name"
	###############################
	
	echo "-----Create output directory-----"
	mkdir -p ${OUT_DIR}
	###############################
 
	echo "-----create CA key-----"
	openssl genrsa -des3 -out ${OUT_DIR}/ca.key -passout pass:$PASSWORD 4096
 
	echo "-----create CA cert-----"
	openssl req -new -x509 -days 365 -key ${OUT_DIR}/ca.key -out ${OUT_DIR}/ca.crt  -passin pass:$PASSWORD -subj "/C=${C}/ST=${ST_CA}/L=${L_CA}/O=${O_CA}/CN=${CN_CA}/"
 
	echo "-----create jks truststore-----"
	keytool -import -trustcacerts -alias caroot -file ${OUT_DIR}/ca.crt  -keystore ${OUT_DIR}/ca-truststore.jks -storepass ${PASSWORD} -noprompt
 
	###############################
 
	echo "-----create server key-----"
	openssl genrsa -des3 -out ${OUT_DIR}/server.key -passout pass:$PASSWORD 4096
 
	echo "-----create server cert request-----"
	openssl req -new -key ${OUT_DIR}/server.key -out ${OUT_DIR}/server.csr  -passin pass:$PASSWORD -subj "/C=${C}/ST=${ST_CA}/L=${L_CA}/O=${O_CA}/CN=${CN_SERVER}/"
 
	echo "-----create server cert-----"
	openssl x509 -req -days 365 -in ${OUT_DIR}/server.csr -CA ${OUT_DIR}/ca.crt  -CAkey ${OUT_DIR}/ca.key -set_serial 01 -out ${OUT_DIR}/server.crt  -passin pass:${PASSWORD}
 
	echo "-----convert server cert to PKCS12 format, including key-----"
	openssl pkcs12 -export -out ${OUT_DIR}/server.p12 -inkey ${OUT_DIR}/server.key  -in ${OUT_DIR}/server.crt -passin pass:${PASSWORD} -passout pass:${PASSWORD}

	echo "-----convert PKCS12 keystore to JKS keystore-----"
	keytool -importkeystore -srckeystore ${OUT_DIR}/server.p12 -srcstoretype PKCS12 -srcstorepass ${PASSWORD} -destkeystore ${OUT_DIR}/server.jks -deststorepass ${PASSWORD}
 
	###############################
 
	echo "-----create client key-----"
	openssl genrsa -des3 -out ${OUT_DIR}/client.key -passout pass:${PASSWORD} 4096
 
	echo "-----create client cert request------"
	openssl req -new -key ${OUT_DIR}/client.key -out ${OUT_DIR}/client.csr -passin pass:$PASSWORD -subj "/C=${C}/ST=${ST_CLIENT}/L=${L_CLIENT}/O=${O_CLIENT}/CN=${CN_CLIENT}/"
 
	echo "-----create client cert-----"
	openssl x509 -req -days 365 -in ${OUT_DIR}/client.csr -CA ${OUT_DIR}/ca.crt -CAkey ${OUT_DIR}/ca.key -set_serial 02 -out ${OUT_DIR}/client.crt  -passin pass:${PASSWORD}
 
	echo "-----convert client cert to PKCS12, including key-----"
	openssl pkcs12 -export -out ${OUT_DIR}/client.p12 -inkey ${OUT_DIR}/client.key  -in ${OUT_DIR}/client.crt -passin pass:${PASSWORD} -passout pass:${PASSWORD}

	echo "-----convert PKCS12 keystore to JKS keystore-----"
	keytool -importkeystore -srckeystore ${OUT_DIR}/client.p12 -srcstoretype PKCS12 -srcstorepass ${PASSWORD} -destkeystore ${OUT_DIR}/client.jks -deststorepass ${PASSWORD}

	###############################
	echo "----- Successfully Create all certificates -----"

{% endhighlight %}

## SSL Configuration

### maven-jetty-plugin 6.1.26

{% highlight xml %}

	<plugin>
      <groupId>org.mortbay.jetty</groupId>
      <artifactId>maven-jetty-plugin</artifactId>
      <configuration>
          <connectors>
              <connector implementation="org.mortbay.jetty.nio.SelectChannelConnector">
                  <port>8080</port>
                  <maxIdleTime>60000</maxIdleTime>
              </connector>
              <connector implementation="org.mortbay.jetty.security.SslSocketConnector">
                  <port>8443</port>
                  <maxIdleTime>60000</maxIdleTime>
                  <keystore>${basedir}/src/test/resources/server.jks</keystore>
                  <password>password</password>
                  <keyPassword>password</keyPassword>
                  <truststore>${basedir}/src/test/resources/ca-truststore.jks</truststore>
                  <trustPassword>password</trustPassword>
                  <wantClientAuth>false</wantClientAuth>
                  <needClientAuth>true</needClientAuth>
              </connector>
          </connectors>
          <contextPath>ps-api-webservice-deamon</contextPath>
          <jettyConfig>${basedir}/src/test/jetty.xml</jettyConfig>
      </configuration>
	</plugin>
{% endhighlight %}

### Standlone Jetty 9
Add SSL connector to Server.xml. Other application server should be similiar.

{% highlight xml%}
	
	<Connector SSLEnabled="true"
           clientAuth="true"
           truststoreFile="{CERTS_LOCATION}/ca-truststore.jks"
           acceptCount="100"
           connectionTimeout="20000"
           executor="tomcatThreadPool"
           keyAlias="1"
           keystoreFile="{CERTS_LOCATION}/server.jks"
           keystorePass="password"
           maxKeepAliveRequests="15"
           port="8443"
           protocol="org.apache.coyote.http11.Http11Protocol"
           redirectPort="8443"
	   scheme="https" />
{% endhighlight %}

After restarted, you should be able to connect with HTTPS now.


## Certificate Authentication

### Spring configuration

I'm using Spring 4, the configuration is very easy, just change Spring security configuration.

{% highlight xml %}

    <http>
        <intercept-url pattern="/**" access="hasRole('ROLE_USER')" /> 
        <x509 subject-principal-regex="CN=(.*?)," /> 
        <logout/>
    </http>
{% endhighlight %}

### Test with Browser and SoapUI

In order to test, you need configure certificate to Browser or SoapUI

Take FireFox for example, you just need Add client.p12 to **Certificate Manager -> Your Certificates** 

For SoapUI, you can 

1. find **Keystore** under **Show Project View -> WS-Security Configurations -> Keystores** 
2. Then add a **Encrytion** **WSS Entry** for **Outgoing WS-Security Configurations**
