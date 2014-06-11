---
layout: post
title: Java 8 Stream Note
categories:
- JAVA
tags:
- Java8
- Stream
status: publish
type: post
published: true
meta:
  _edit_last: '1'
author:
  login: villim
  email: villim@126.com
  display_name: Villim
  first_name: Villim
  last_name: Wong
---
<p>We have seen <a title="Java 8 Lambda Learning Notes" href="http://www.from0to1.net/java-8-lambda-learning-notes/" target="_blank">How the Java8 Lambda working</a>.</p>
<p>And another big new stuff  is the Steam Interface. When they co-operate with each other, will be much more powerful.</p>
<h4><span style="color: #993300;"><strong>WHAT IS STREAM?</strong></span></h4>
<ul>
<li>As Javadoc says , streams  are sequences of elements supporting sequential and parallel aggregate operations</li>
<li>A Stream is the internal iteration analogue of an Iterator</li>
</ul>
<p>Let's see a example, previously, we have to do loops like</p>
<pre class="lang:java decode:true">int count = 0;
for (Artist artist : allArtists) {
if (artist.isFrom("London")) { 
    count++;
} }</pre>
<p>But with Stream, you can make a much clean code like</p>
<pre class="lang:java decode:true">long count = allArtists.stream()
                       .filter(artist -&gt; artist.isFrom("London"))
                       .count();</pre>
<p>So, A Stream is a tool for building up complex operations on collections using a functional approach.  We can also simply describe the change of Collections as from external iteration to internal iteration.</p>
<h4></h4>
<h4><strong><span style="color: #993300;">COMMON STREAM OPERATIONS</span></strong></h4>
<p>The Stream Interface provide quite many methods to facilitate using collections. Here, just introduce a few most common operations. <a title="Java8 Stream" href="http://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html" target="_blank">You may need check the document yourself</a>.</p>
<p>&nbsp;</p>
<h5><strong><span style="color: #008000;">MAP</span></strong></h5>
<p>If you've got a function that converts a value of one type into another, map lets you apply this function to a stream of values, producing another stream of the new values.</p>
<pre class="lang:java decode:true">List&lt;String&gt; collected = Arrays.asList("a", "b", "hello").stream()
                               .map(string -&gt; string.toUpperCase())
                               .collect(Collectors.toList());</pre>
<h5><strong><span style="color: #008000;">FILTER</span></strong></h5>
<div class="page" title="Page 38">
<div class="layoutArea">
<div class="column">
<p>Any time you’re looping over some data and checking each element, you might want to think about using the new filter method on Stream</p>
<pre class="lang:java decode:true">List&lt;String&gt; beginningWithNumbers = Arrays.asList("a", "1abc", "abc1").stream()
                                          .filter(value -&gt; isDigit(value.charAt(0)))
                                          .collect(Collectors.toList());</pre>
<div class="page" title="Page 39">
<div class="layoutArea">
<div class="column">
<h5><span style="color: #008000;"><strong>FLATMAP</strong></span></h5>
<p>flatMap lets you replace a value with a Stream and concatenates all the streams together.</p>
<div class="page" title="Page 39">
<div class="layoutArea">
<div class="column">
<pre class="lang:java decode:true">List&lt;Integer&gt; together = Arrays.asList(Arrays.asList(1, 2), Arrays.asList(3, 4)).stream()
                               .flatMap(numbers -&gt; numbers.stream())
                               .collect(Collectors.toList());</pre>
<div class="page" title="Page 40">
<div class="layoutArea">
<div class="column">
<h5><span style="color: #008000;"><strong>MAX and MIN</strong></span></h5>
<pre class="lang:java decode:true">List&lt;Track&gt; tracks = Arrays.asList(new Track("Bakai", 524),
                            new Track("Violets for Your Furs", 378),
                            new Track("Time Was", 451));

Track shortestTrack = tracks.stream()
                            .min(Comparator.comparing(track -&gt; track.getLength()))
                            .get();</pre>
<h5><span style="color: #008000;"><strong>REDUCE</strong></span></h5>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="page" title="Page 42">
<div class="layoutArea">
<div class="column">
<div class="page" title="Page 42">
<div class="layoutArea">
<div class="column">
<p>Use the reduce operation when you've got a collection of values and you want to generate a single result.</p>
<pre class="lang:java decode:true">int count = Arrays.asList(1, 2, 3).stream()
                  .reduce(0, (acc, element) -&gt; acc + element);
assertEquals(6, count);

List&lt;String&gt; numerals = Arrays.asList("1","2","3","4");
String concatation = numerals.stream()
                             .reduce("", String::concat); //same as (s1,s2) -&gt; s1 + s2
assertEquals("1234", concatation);</pre>
<h5></h5>
<p>&nbsp;</p>
</div>
</div>
</div>
</div>
</div>
</div>
<h4><span style="color: #993300;"><strong>ADVANCE STREAM OPERATIONS</strong></span></h4>
<div class="page" title="Page 78">
<div class="layoutArea">
<h5></h5>
<h5></h5>
<h5><strong><span style="color: #008000;">Element Ordering</span></strong></h5>
<pre class="lang:java decode:true">Set&lt;Integer&gt; numbers = new HashSet&lt;&gt;(Arrays.asList(4, 3, 2, 1));
List&lt;Integer&gt; sameOrder = numbers.stream()
                                 .sorted()
                                 .collect(Collectors.toList());
assertEquals(asList(1, 2, 3, 4), sameOrder);</pre>
<h5><strong><span style="color: #008000;">Collector Interface</span></strong></h5>
<p>As we already seen a lot of <strong>.collect(toSet()) </strong>and <strong>.collect(toList()) </strong>. Usually, we use a List to produce from a Stream, but we can also generate Map or Set.</p>
<h5 class="column"><span style="color: #008000;"><strong>Collecting into a custom collection</strong></span></h5>
<pre class="lang:java decode:true ">stream.collect(toCollection(TreeSet::new));</pre>
<h5><strong><span style="color: #008000;">Collecting into Values</span></strong></h5>
<p>It’s also possible to collect into a single value using a collector. There are maxByand minBy collectors that let you obtain a single value according to some ordering.</p>
<pre class="lang:java decode:true">public Optional&lt;Artist&gt; biggestGroup(Stream&lt;Artist&gt; artists) {
    Function&lt;Artist,Long&gt; getCount = artist -&gt; artist.getMembers().count();
    return artists.collect(Collectors.maxBy(Comparator.comparing(getCount)));
}</pre>
<p>and even can get average number</p>
<pre class="lang:java decode:true">public double averageNumberOfTracks(List&lt;Album&gt; albums) {
   return albums.stream()
                .collect(Collectors.averagingInt(album -&gt; album.getTrackList().size()));
}</pre>
<p><strong><span style="color: #008000;">Partitioning the Data </span></strong></p>
<p>you might want to do with a Stream is partition it into two collections of values.</p>
<div class="page" title="Page 79">
<div class="layoutArea">
<div class="column">
<pre class="lang:java decode:true">public Map&lt;Boolean, List&lt;Artist&gt;&gt; bandsAndSoloRef(Stream&lt;Artist&gt; artists) { 
    return artists.collect(Collectors.partitioningBy(Artist::isSolo));
}</pre>
<p><strong><span style="color: #008000;">Grouping the Data </span></strong></p>
<p>you need partitioning then you also can grouping</p>
<div class="page" title="Page 79">
<div class="layoutArea">
<div class="column">
<div class="page" title="Page 79">
<div class="layoutArea">
<div class="column">
<pre class="lang:java decode:true">public Map&lt;Artist, List&lt;Album&gt;&gt; albumsByArtist(Stream&lt;Album&gt; albums) { 
   return albums.collect(Collectors.groupingBy(album -&gt; album.getMainMusician()));
}</pre>
<h5> <span style="color: #008000;"><strong>Strings </strong></span></h5>
<p>it's quite often, I want to concatenate Strings with collection value as some kind of standard, like "[AA, BB, CC, DD, EE]"</p>
<p>And now it's very convenient to do that.</p>
<div class="page" title="Page 80">
<div class="layoutArea">
<div class="column">
<pre class="lang:java decode:true crayon-selected">String result = artists.stream()
                       .map(Artist::getName)
                       .collect(Collectors.joining(",", "[", "]"));</pre>
<p>&nbsp;</p>
<h4><span style="color: #993300;"><strong>WHAT'S THE PROBLEM STREAM ?</strong></span></h4>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
<p><span style="color: #008000;"><strong>How to print the looping items</strong></span></p>
<p>we get  <strong>.forEach(), </strong>but we can't continue operate on stream any more</p>
<pre class="lang:java decode:true ">album.getMusicians()
     .filter(artist -&gt; artist.getName().startsWith("The"))
     .map(artist -&gt; artist.getNationality())
     .forEach(nationality -&gt; System.out.println("Found: " + nationality));

Set&lt;String&gt; nationalities = 
album.getMusicians()
     .filter(artist -&gt; artist.getName().startsWith("The"))
     .map(artist -&gt; artist.getNationality())
     .collect(Collectors.&lt;String&gt;toSet());</pre>
<p>Lucky, we have a solution to use <strong>peek()</strong></p>
<pre class="lang:java decode:true ">Set&lt;String&gt; nationalities
= album.getMusicians()
       .filter(artist -&gt; artist.getName().startsWith("The"))
       .map(artist -&gt; artist.getNationality())
       .peek(nation -&gt; System.out.println("Found nationality: " + nation))
       .collect(Collectors.&lt;String&gt;toSet());</pre>
<p><span style="color: #008000;"><strong>Can't handle Exception, can't break the iteration</strong></span></p>
<p>In previous for loop, some if we may need <strong>break</strong> or <strong>continue </strong>on some condition, but not able to do it in Stream.</p>
<p>&nbsp;</p>
</div>
</div>
</div>
<div class="page" title="Page 35">
<div class="layoutArea">
<div class="column">
<h4><strong><span style="color: #993300;">WHY USING STREAM</span></strong></h4>
<p>Although you may not feeling convenient at the beginning, but once you do familiar with this new grammar, you will see it's really easy to do internal iteration.</p>
<p>beside that, the most powerful function should be <strong>Parallelism. </strong>There're a lot parallel methods, let's see a example.</p>
<pre class="lang:java decode:true crayon-selected">public int parallelArraySum() {
    return albums.parallelStream()
                 .flatMap(Album::getTracks)
                 .mapToInt(Track::getLength)
                 .sum();
}</pre>
<p>It's obviously what Parallelism can bring, but you have to be careful, not all situations is able to do it.</p>
<p>&nbsp;</p>
</div>
</div>
</div>
