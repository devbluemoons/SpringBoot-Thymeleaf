##### remove duplicate element from List<custom-object>
```java
public static <T> Predicate<T> distinctByKey(Function<? super T, ?> keyExtractor) {
    Set<Object> seen = ConcurrentHashMap.newKeySet();
    return t -> seen.add(keyExtractor.apply(t));
}

people.stream().filter(distinctByKey(Person::getName)).collect(Collectors.toList());
```
  
Reference - https://stackoverflow.com/questions/23699371/java-8-distinct-by-property
