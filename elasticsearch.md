## Elasticsearch Quick Notes

### 🧩 Cluster & Sharding
- Multiple servers together form an **Elasticsearch cluster**.
- Data is divided into **shards**.
- Number of **primary shards** is decided when the index is created.
- Each primary shard can have **N replicas** distributed across different nodes.
- If a primary shard fails, Elasticsearch automatically promotes a replica to primary.

---

## 🚀 Ways to Improve Write Speed

1. **Use Bulk API**  
   - Reduces per-request overhead.
2. **Increase Refresh Interval**  
   - Lower refresh intervals consume more CPU and I/O.  
   - Higher interval improves indexing speed.
3. **Increase Translog Durability Time**  
   - Faster writes.  
   - Tradeoff: possible data loss if node crashes before flush.
4. **Disable Replicas During Initial Load**  
   - Speeds up bulk ingestion.
5. **Use Auto-generated `_id`**  
   - Avoids lookup cost to check if custom ID already exists.
---
## 📖 Ways to Scale Reads

1. **Maintain Proper Shard Size**  
   - Recommended: **10 GB to 50 GB** per shard.
2. **Keep CPU Below 60-65%**  
   - Useful headroom during shard reassignment or traffic spikes.
3. **Use Replicas for Read Throughput**  
   - Search requests can be served by replicas too.
4. **Enable Caching at Index Level**  
   - Improves repeated query performance.
---

## 🔀 Routing & Rebalancing

- Shard is determined using:

```text
hash(_id) % number_of_primary_shards
```
Since primary shard count is fixed, shard location can always be identified.
Every node keeps a copy of cluster state, which maps shards to physical nodes.

---
## 🔤 String Field Types
1. Text
- Stored as an inverted index:
- token → list of document IDs
- Best for full-text search.
2. Keyword
- Best for: Aggregations, Sorting, Filtering, Exact matches

---
## 🎯 Precision vs Recall
Precision = How relevant returned results are.
Recall = How many relevant records were actually returned.

Improve Precision
Default query behavior often uses OR.
Use AND to make results stricter.

---
## 📊 Ranking / Relevance Score
Search results are sorted by relevance score.Traditionally based on TF-IDF. Modern Elasticsearch commonly uses BM25.

