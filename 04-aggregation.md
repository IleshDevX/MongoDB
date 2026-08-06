# 04 — Aggregation Basics

Aggregation lets you group and compute statistics, similar to `GROUP BY` in SQL. In Compass, use the **Aggregations** tab; on the shell use `db.students.aggregate([...])`.

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

## Count active vs inactive students

```javascript
db.students.aggregate([
  { $group: {
      _id: "$is_active",
      count: { $sum: 1 }
  } }
])
```

## Students per city, only cities with 3+ students

```javascript
db.students.aggregate([
  { $group: { _id: "$city", count: { $sum: 1 } } },
  { $match: { count: { $gte: 3 } } },
  { $sort: { count: -1 } }
])
```

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
