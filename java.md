# ConcurrentModificationException in ArrayList
### Cause
Occurs when an `ArrayList` is **structurally modified during iteration** or **Multiple threads modifying same list**.
### How does it detect ?
Iterator detects change via internal `modCount` (count of structural modifications made to the collection) and throws exception. 

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
