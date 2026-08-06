# 01 — CRUD Basics

## Create — Insert a document

In Compass: **Insert Document**, paste, then **Save**.

```json
{
  "roll_no": 121,
  "name": "Your Name",
  "age": 19,
  "course": "BCA-AI",
  "city": "Your City",
  "email": "you@example.com",
  "marks": 80,
  "is_active": true,
  "enrolled_on": "2024-06-25"
}
```

Command line equivalent:

```javascript
db.students.insertOne({
  roll_no: 121,
  name: "Your Name",
  age: 19,
  course: "BCA-AI",
  city: "Your City",
  email: "you@example.com",
  marks: 80,
  is_active: true,
  enrolled_on: "2024-06-25"
})
```

Insert many at once:

```javascript
db.students.insertMany([
  { roll_no: 122, name: "Student A", age: 19, course: "BCA-DS", city: "Surat", marks: 70, is_active: true },
  { roll_no: 123, name: "Student B", age: 20, course: "BCA-Cyber", city: "Rajkot", marks: 85, is_active: true }
])
```

## Read — Find a document

```javascript
db.students.findOne({ roll_no: 101 })
```

## Update — Edit a document

In Compass: hover a document → pencil icon → edit → **Update**.

```javascript
db.students.updateOne(
  { roll_no: 101 },
  { $set: { marks: 82 } }
)
```

Update many documents at once — give everyone in `BCA-AI` 2 bonus marks:

```javascript
db.students.updateMany(
  { course: "BCA-AI" },
  { $inc: { marks: 2 } }
)
```

## Delete — Remove a document

```javascript
db.students.deleteOne({ roll_no: 121 })
```

Delete every inactive student:

```javascript
db.students.deleteMany({ is_active: false })
```

> ⚠️ Careful with `deleteMany` — it removes every matching document. Always test the filter with `find()` first.
