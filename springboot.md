### 🧠 Transactional One Liner 
Same-class method calls bypass Spring proxy, so `@Transactional` advice is not applied. Fix is to move transactional method to another bean.
