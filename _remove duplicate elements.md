##### remove duplicate element from List<custom-object>
```java
public static <T> Predicate<T> distinctByKey(Function<? super T, ?> keyExtractor) {
    Set<Object> seen = ConcurrentHashMap.newKeySet();
    return t -> seen.add(keyExtractor.apply(t));
}

people.stream().filter(distinctByKey(Person::getName))
```
