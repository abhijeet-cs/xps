### 🧠 Transactional Annotation
Same-class method calls bypass Spring proxy, so `@Transactional` advice is not applied. Fix is to move transactional method to another bean.

### 🧠 Thread Safety of Spring Boot Beans
Spring Boot beans are not automatically thread-safe. Most beans are singleton scoped by default, meaning one shared instance serves many concurrent request. If the bean has mutable shared state => Multiple requests can race and corrupt data.
