# 05 — Indexing Basics

Indexes make searches faster on large collections, like the index at the back of a book. With only 20 documents you won't see a speed difference, but it's worth knowing how they work.

## Create an index

Speed up searches by course:

```javascript
db.students.createIndex({ course: 1 })
```
> This tells MongoDB to keep a sorted lookup on `course`, so it doesn't have to scan every document to find matches. `1` means ascending order, `-1` means descending.

## Compound index (multiple fields)

Speed up searches that filter by course and sort by marks:

```javascript
db.students.createIndex({ course: 1, marks: -1 })
```
> A compound index covers two fields at once — here, students are grouped by course and pre-sorted by marks within each course, useful when a query filters *and* sorts by these fields.

## List all indexes on a collection

```javascript
db.students.getIndexes()
```
> Shows every index on the collection, including the default one MongoDB always creates on `_id`.

## Check if a query uses an index

```javascript
db.students.find({ course: "BCA-AI" }).explain("executionStats")
```
> Runs the query and reports how MongoDB executed it.

Look for `"stage": "IXSCAN"` in the output — that means the index was used. `"COLLSCAN"` means MongoDB scanned every document instead.

## Drop an index

```javascript
db.students.dropIndex({ course: 1 })
```
> Removes an index you no longer need — indexes take up storage and slow down writes slightly, so it's good to drop unused ones.

> In Compass, indexes can be created and viewed from the **Indexes** tab of a collection — no shell needed.
