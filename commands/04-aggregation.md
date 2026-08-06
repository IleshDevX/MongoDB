# 04 — Aggregation Basics

Aggregation lets you group and compute statistics, similar to `GROUP BY` in SQL. In Compass, use the **Aggregations** tab; on the shell use `db.students.aggregate([...])`. You pass a list of stages, and each stage transforms the data before passing it to the next one.

## Average marks per course

```javascript
db.students.aggregate([
  { $group: {
      _id: "$course",
      averageMarks: { $avg: "$marks" },
      totalStudents: { $sum: 1 }
  } },
  { $sort: { averageMarks: -1 } }
])
```
> `$group` bundles students by `course`, `$avg` computes the average marks per group, and `$sum: 1` counts students in each group. Then we sort by average, highest first.

## Highest scorer per course

```javascript
db.students.aggregate([
  { $sort: { marks: -1 } },
  { $group: {
      _id: "$course",
      topStudent: { $first: "$name" },
      topMarks: { $first: "$marks" }
  } }
])
```
> We sort by marks first so the top scorer comes first in each course. Then `$first` grabs that first (highest) student's name and marks per group.

## Count active vs inactive students

```javascript
db.students.aggregate([
  { $group: {
      _id: "$is_active",
      count: { $sum: 1 }
  } }
])
```
> Groups students by `is_active` (true/false) and counts how many fall into each group.

## Students per city, only cities with 3+ students

```javascript
db.students.aggregate([
  { $group: { _id: "$city", count: { $sum: 1 } } },
  { $match: { count: { $gte: 3 } } },
  { $sort: { count: -1 } }
])
```
> Group by city and count students, then `$match` filters those group totals to keep only cities with 3 or more students, sorted highest first.

## Join students with their course details ($lookup)

This pulls in matching documents from the `courses` collection:

```javascript
db.students.aggregate([
  { $lookup: {
      from: "courses",
      localField: "course",
      foreignField: "course_code",
      as: "course_details"
  } },
  { $unwind: "$course_details" },
  { $project: {
      name: 1,
      marks: 1,
      "course_details.course_name": 1,
      "course_details.instructor": 1
  } }
])
```
> `$lookup` works like a SQL join — it matches `course` to `course_code` in the `courses` collection. `$unwind` flattens the matched array into a single object, and `$project` picks just the fields we want to keep.
