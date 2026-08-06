# 03 — Projection, Sorting & Paging

## Projection — show only certain fields

In Compass, use the **Project** box next to the filter bar. On the shell:

Show only name and marks (hide `_id`):

```javascript
db.students.find(
  {},
  { name: 1, marks: 1, _id: 0 }
)
```

## Sorting

Highest marks first:

```javascript
db.students.find().sort({ marks: -1 })
```

Alphabetical by name:

```javascript
db.students.find().sort({ name: 1 })
```

## Limiting results

Top 5 scorers:

```javascript
db.students.find().sort({ marks: -1 }).limit(5)
```

## Paging (skip + limit)

Second page of 5 results, sorted by roll number:

```javascript
db.students.find().sort({ roll_no: 1 }).skip(5).limit(5)
```

## Counting

How many students are in BCA-AI:

```javascript
db.students.countDocuments({ course: "BCA-AI" })
```
