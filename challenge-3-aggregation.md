# Challenge 3 — Aggregation

1. Find the average marks for each course.
2. Find which city has the most students.
3. Find the top scorer overall (across all courses).
4. Using `$lookup`, list each student's name along with their course's instructor name.
5. Count how many students are active vs inactive per course (hint: group by two fields using `{ course: "$course", active: "$is_active" }` as `_id`).
