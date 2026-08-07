# MongoDB Atlas Project — Student Management System (Extended)

A bigger, hands-on MongoDB project using **Atlas + Compass**. Two related collections, 20 student records, and a full run through CRUD, querying, projections, sorting, aggregation, and indexing.

No local MongoDB install needed — just a browser and Compass.

## What you'll build

```
Database: student_management

Collections:
├── students   (20 documents)
└── courses    (3 documents)
```

Each student references a course by `course` code, which matches `course_code` in the `courses` collection — so you also get a taste of how collections relate to each other.

```json
// students
{
  "roll_no": 101,
  "name": "Rahul Patel",
  "age": 19,
  "course": "BCA-AI",
  "city": "Surat",
  "email": "rahul.patel@example.com",
  "marks": 78,
  "is_active": true,
  "enrolled_on": "2024-06-15"
}
```

```json
// courses
{
  "course_code": "BCA-AI",
  "course_name": "BCA in Artificial Intelligence",
  "duration_years": 3,
  "instructor": "Dr. Mehta",
  "fees_inr": 85000
}
```

## Prerequisites

- Laptop with internet access
- [MongoDB Compass](https://www.mongodb.com/try/download/compass) installed beforehand
- A free [MongoDB Atlas](https://www.mongodb.com/cloud/atlas/register) account, or the shared connection string from your instructor

## Repository structure

```
mongodb-workshop/
├── README.md
├── starter-data/
│   ├── students.json
│   └── courses.json
├── commands/
│   ├── 01-crud.md
│   ├── 02-queries.md
│   ├── 03-projection-sort.md
│   ├── 04-aggregation.md
└── challenges/
    ├── challenge-1-crud.md
    ├── challenge-2-queries.md
    └── challenge-3-aggregation.md
```

## Getting the files

```
git clone https://github.com/yourname/mongodb-workshop
```

Or download the ZIP from the green **Code** button on GitHub.

---

## Step-by-step setup

### Step 1 — Connect to Atlas

**Option A (fastest, shared cluster):** Use the connection string your instructor provides. Skip to Step 2.

**Option B (your own cluster):**
1. Sign up at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas/register)
2. Create a Free (M0) Cluster
3. Create a database user (username + password)
4. Network Access → Add IP → Allow access from anywhere (`0.0.0.0/0`)
5. Click **Connect → Compass** and copy the connection string

### Step 2 — Connect with Compass

1. Open Compass
2. Paste the connection string → **Connect**

### Step 3 — Create the database and collections

1. Click **Create Database**
   - Database name: `student_management`
   - Collection name: `students`
2. Inside the same database, click **Create Collection** again
   - Collection name: `courses`

### Step 4 — Import both datasets

For each collection:
1. Open the collection
2. **Add Data → Import File**
3. Select the matching file from `starter-data/` (`students.json` or `courses.json`)
4. Click **Import**

You should see 20 documents in `students` and 3 documents in `courses`.

### Step 5 — Work through the command sheets in order

1. [`commands/01-crud.md`](commands/01-crud.md) — Insert, update, delete
2. [`commands/02-queries.md`](commands/02-queries.md) — Filtering with operators
3. [`commands/03-projection-sort.md`](commands/03-projection-sort.md) — Choosing fields, sorting, paging
4. [`commands/04-aggregation.md`](commands/04-aggregation.md) — Grouping and computing stats

### Step 6 — Challenges

Work through these on your own once you've finished the command sheets:

1. [`challenges/challenge-1-crud.md`](challenges/challenge-1-crud.md)
2. [`challenges/challenge-2-queries.md`](challenges/challenge-2-queries.md)
3. [`challenges/challenge-3-aggregation.md`](challenges/challenge-3-aggregation.md)

---
