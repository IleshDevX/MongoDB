# 02 — Queries & Operators

Paste these into the Compass **Filter** bar, or run as `db.students.find({...})`.

## Exact match

```json
{ "city": "Surat" }
```

## Comparison operators

Marks greater than 80:

```json
{ "marks": { "$gt": 80 } }
```

Age less than or equal to 19:

```json
{ "age": { "$lte": 19 } }
```

Marks between 60 and 80:

```json
{ "marks": { "$gte": 60, "$lte": 80 } }
```

## Logical operators

Students from Surat **AND** in BCA-AI:

```json
{ "$and": [ { "city": "Surat" }, { "course": "BCA-AI" } ] }
```

Students from Surat **OR** Rajkot:

```json
{ "$or": [ { "city": "Surat" }, { "city": "Rajkot" } ] }
```

Students **NOT** in BCA-DS:

```json
{ "course": { "$ne": "BCA-DS" } }
```

## Set membership

City is one of a list:

```json
{ "city": { "$in": ["Surat", "Ahmedabad", "Rajkot"] } }
```

City is none of a list:

```json
{ "city": { "$nin": ["Bhavnagar", "Vadodara"] } }
```

## Boolean fields

Only active students:

```json
{ "is_active": true }
```

## Text search (starts with)

Names starting with "R":

```json
{ "name": { "$regex": "^R" } }
```
