---
layout: post
title: Java 8 Stream Note
categories:
- JAVA
tags:
- Java8
- Stream

---
<p>We have seen <a title="Java 8 Lambda Learning Notes" href="http://www.from0to1.net/java-8-lambda-learning-notes/" target="_blank">How the Java8 Lambda working</a>.</p>
<p>And another big new stuff  is the Steam Interface. When they co-operate with each other, will be much more powerful.</p>

###WHAT IS STREAM?


* As Javadoc says , streams  are sequences of elements supporting sequential and parallel aggregate operations
* A Stream is the internal iteration analogue of an Iterator

<p>Let's see a example, previously, we have to do loops like</p>

```java
	int count = 0;
		for (Artist artist : allArtists) {
	  	if (artist.isFrom("London")) { 
        	count++;
	} }

```
	
But with Stream, you can make a much clean code like
```java
	long count = allArtists.stream()
    	.filter(artist -> artist.isFrom("London"))
        .count();

```

So, A Stream is a tool for building up complex operations on collections using a functional approach.  We can also simply describe the change of Collections as from external iteration to **internal iteration**.

###COMMON STREAM OPERATIONS
The Stream Interface provide quite many methods to facilitate using collections. Here, just introduce a few most common operations. <a title="Java8 Stream" href="http://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html" target="_blank">You may need check the document yourself</a>

####MAP

If you've got a function that converts a value of one type into another, map lets you apply this function to a stream of values, producing another stream of the new values.

```java
	List<String> collected = Arrays.asList("a", "b", "hello")
	     .stream()
         .map(string -> string.toUpperCase())
         .collect(Collectors.toList());
```

####FILTER
Any time you’re looping over some data and checking each element, you might want to think about using the new filter method on Stream

```java
	List<String> beginningWithNumbers = Arrays.asList("a", "1abc", "abc1")
	    .stream()
    	.filter(value -> isDigit(value.charAt(0)))
        .collect(Collectors.toList());
```     

####FLATMAP
flatMap lets you replace a value with a Stream and concatenates all the streams together.

```java
	List<Integer> together = Arrays.asList(Arrays.asList(1, 2)
		, Arrays.asList(3, 4))
		.stream()
		.flatMap(numbers -> numbers.stream()).collect(Collectors.toList());
```

####MAX and MIN

```java
	List<Track> tracks = Arrays.asList(new Track("Bakai", 524),
    	new Track("Violets for Your Furs", 378),
		new Track("Time Was", 451));

	Track shortestTrack = tracks.stream()
        .min(Comparator.comparing(track -> track.getLength()))
        .get();
```
        
####REDUCE

Use the reduce operation when you've got a collection of values and you want to generate a single result.

```java
	int count = Arrays.asList(1, 2, 3).stream()
    	.reduce(0, (acc, element) -> acc + element);
	assertEquals(6, count);

	List<String> numerals = Arrays.asList("1","2","3","4");
	String concatation = numerals.stream()
           .reduce("", String::concat); //same as (s1,s2) -> s1 + s2
	assertEquals("1234", concatation);
```

####ADVANCE STREAM OPERATIONS

#####Element Ordering

```java

	Set<Integer> numbers = new HashSet<>(Arrays.asList(4, 3, 2, 1));
	List<Integer> sameOrder = numbers.stream()
                                     .sorted()
                                     .collect(Collectors.toList());
	assertEquals(asList(1, 2, 3, 4), sameOrder);
```

#####Collector Interface
As we already seen a lot of **.collect(toSet()) **and **.collect(toList()) **. Usually, we use a List to produce from a Stream, but we can also generate Map or Set.

#####Collecting into a custom collection

```java

	stream.collect(toCollection(TreeSet::new));
```
	
#####Collecting into Values
It’s also possible to collect into a single value using a collector. There are maxByand minBy collectors that let you obtain a single value according to some ordering.

```java

	public Optional<Artist> biggestGroup(Stream<Artist> artists) {
      Function<Artist,Long> getCount = artist -> artist.getMembers().count();
      return artists.collect(Collectors.maxBy(Comparator.comparing(getCount)));
	}
```

and even can get average number

```java

	public double averageNumberOfTracks(List<Album> albums) {
    	return albums.stream()
                    .collect(Collectors.averagingInt(album -> 				 	              album.getTrackList().size()));
	}
```
	
#####Partitioning the Data
you might want to do with a Stream is partition it into two collections of values.

```java

	public Map<Boolean, List<Artist>> bandsAndSoloRef(Stream<Artist> artists) { 
      return artists.collect(Collectors.partitioningBy(Artist::isSolo));
	}
```

#####Grouping the Data
you need partitioning then you also can grouping

```java

	public Map<Artist, List<Album>> albumsByArtist(Stream<Album> albums) { 
      return albums.collect(Collectors.groupingBy(album -> 							album.getMainMusician()));
	}
```
	
#####Strings
it's quite often, I want to concatenate Strings with collection value as some kind of standard, like "[AA, BB, CC, DD, EE]"

And now it's very convenient to do that.

```java

	String result = artists.stream()
                           .map(Artist::getName)
                           .collect(Collectors.joining(",", "[", "]"));

```

####WHAT'S THE PROBLEM STREAM ?

#####How to print the looping items
we can use **.forEach()**, but we can't continue operate on stream any more.

```java

	album.getMusicians()
     .filter(artist -> artist.getName().startsWith("The"))
     .map(artist -> artist.getNationality())
     .forEach(nationality -> System.out.println("Found: " + nationality));

	Set<String> nationalities = album.getMusicians()
     .filter(artist -> artist.getName().startsWith("The"))
     .map(artist -> artist.getNationality())
     .collect(Collectors.<String>toSet());
```
     
Lucky, we have a solution to use **peek()**

```java

	Set<String> nationalities= album.getMusicians()
       .filter(artist -> artist.getName().startsWith("The"))
       .map(artist -> artist.getNationality())
       .peek(nation -> System.out.println("Found nationality: " + nation))
       .collect(Collectors.<String>toSet());
 ```
       
#####Can't handle Exception, can't break the iteration
In previous for loop, some if we may need **breakor** and **continue** on some condition, but not able to do it in Stream.

####WHY USING STREAM

Although you may not feeling convenient at the beginning, but once you do familiar with this new grammar, you will see it's really easy to do internal iteration.</p>
<p>beside that, the most powerful function should be **Parallelism.** There're a lot parallel methods, let's see a example.

```java

	public int parallelArraySum() {
    	return albums.parallelStream()
                 .flatMap(Album::getTracks)
                 .mapToInt(Track::getLength)
                 .sum();
	}
```
	
It's obviously what Parallelism can bring, but you have to be careful, not all situations is able to do it.

