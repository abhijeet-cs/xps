# ConcurrentModificationException in ArrayList

### Cause
Occurs when an `ArrayList` is **structurally modified during iteration**.
Examples:
- `add()`
- `remove()`
- `clear()`

Iterator detects change via internal `modCount` and throws exception. 

## Reason
Multiple threads modifying same list or same thread modifying during iteration.
```java
for (String s : list) {
    list.remove(s);
}
```

## Fixes
1. Use Iterator.remove()
```java
Iterator<String> it = list.iterator();
while (it.hasNext()) {
    if (it.next().equals("x")) it.remove();
}
```
2. Thread safe data structure
```java
CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<>();
```
