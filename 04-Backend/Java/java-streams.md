Java Streams
1
2
3
Java Streams, introduced in Java 8, provide a functional approach to processing sequences of elements from sources like Collections, arrays, or I/O channels without modifying the original data. They support aggregate operations such as filtering, mapping, reducing, and sorting, and can be executed sequentially or in parallel.

A stream pipeline consists of:

Source (e.g., List, Set, Array, Files.lines())

Intermediate operations (lazy, return another stream)

Terminal operation (produces a result or side-effect)

Example — Creating and Processing a Stream

import java.util.*;
import java.util.stream.*;

public class StreamExample {
public static void main(String[] args) {
List<String> names = Arrays.asList("Reflection", "Collection", "Stream", "Structure", "Sorting", "State");

List<String> result = names.stream()
.filter(s -> s.startsWith("S")) // Intermediate: filter
.map(String::toUpperCase) // Intermediate: map
.sorted() // Intermediate: sorted
.collect(Collectors.toList()); // Terminal: collect

result.forEach(System.out::println);
}
}
Copy
Output:

SORTING
STATE
STREAM
STRUCTURE
Copy
Key Intermediate Operations

map() — transforms each element.

filter() — selects elements matching a predicate.

sorted() — sorts elements (natural order or comparator).

flatMap() — flattens nested structures.

distinct() — removes duplicates.

peek() — performs an action without altering elements.

Key Terminal Operations

collect() — gathers results into a collection or string.

forEach() — iterates over elements.

reduce() — combines elements into a single value.

count(), findFirst(), allMatch(), anyMatch() — various aggregations and checks.

Parallel Streams

long count = names.parallelStream()
.filter(s -> s.isEmpty())
.count();
Copy
Parallel streams leverage the ForkJoinPool for concurrent processing but should be used when tasks are uniform in execution time.

Java 9+ Enhancements

takeWhile() / dropWhile() — process elements until a condition fails or skip until it fails.

Enhanced iterate() — allows a stopping condition.

ofNullable() — creates a stream with zero or one element, avoiding null checks.

Best Practices

Place size-reducing operations (filter, distinct, skip) early in the pipeline for efficiency.

Avoid reusing a stream after a terminal operation.

Use parallel streams judiciously to prevent performance degradation in uneven workloads.

This API enables concise, readable, and efficient data processing, replacing verbose loops with declarative pipelines.