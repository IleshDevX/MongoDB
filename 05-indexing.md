# 05 — Indexing Basics

Indexes make searches faster on large collections. With only 20 documents you won't see a speed difference, but it's worth knowing how they work.

## Create an index

Speed up searches by course:

```javascript
db.students.createIndex({ course: 1 })
```

`1` means ascending order, `-1` means descending.

## Compound index (multiple fields)

Speed up searches that filter by course and sort by marks:

```javascript
db.students.createIndex({ course: 1, marks: -1 })
```

## List all indexes on a collection

```javascript
db.students.getIndexes()
```

## Check if a query uses an index

```javascript
db.students.find({ course: "BCA-AI" }).explain("executionStats")
```

Look for `"stage": "IXSCAN"` in the output — that means the index was used. `"COLLSCAN"` means MongoDB scanned every document instead.

## Drop an index

```javascript
db.students.dropIndex({ course: 1 })
```

> In Compass, indexes can be created and viewed from the **Indexes** tab of a collection — no shell needed.
