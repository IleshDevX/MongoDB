# 03 — Projection, Sorting & Paging

## Projection — show only certain fields

Projection lets you pick which fields come back in the results, instead of the whole document. In Compass, use the **Project** box next to the filter bar. On the shell:

Show only name and marks (hide `_id`):

```javascript
db.students.find(
  {},
  { name: 1, marks: 1, _id: 0 }
)
```
> `1` = include the field, `0` = exclude it. `_id` shows by default, so we turn it off here.

## Sorting

`.sort()` controls the order results come back in — it doesn't change *which* documents match, just their sequence. `1` = ascending, `-1` = descending.

Highest marks first:

```javascript
db.students.find().sort({ marks: -1 })
```

Alphabetical by name:

```javascript
db.students.find().sort({ name: 1 })
```

## Limiting results

`.limit(n)` cuts the results down to the first `n` documents, usually after a sort so you get the "best" ones.

Top 5 scorers:

```javascript
db.students.find().sort({ marks: -1 }).limit(5)
```

## Paging (skip + limit)

`.skip()` jumps over a number of results, and `.limit()` grabs the next batch — together they simulate "pages" of results. Always sort first so pages stay consistent.

Second page of 5 results, sorted by roll number:

```javascript
db.students.find().sort({ roll_no: 1 }).skip(5).limit(5)
```

## Counting

`countDocuments()` returns just a number of matches, instead of the documents themselves.

How many students are in BCA-AI:

```javascript
db.students.countDocuments({ course: "BCA-AI" })
```
