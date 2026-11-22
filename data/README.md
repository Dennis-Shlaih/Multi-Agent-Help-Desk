# Riverview College help-desk data (fictional)

These files describe a fictional college. They are not Hunter College or CUNY policy. They are the same files as in Assignment 3.

The help desk plans the **Spring 2027** term. The current term is **Fall 2026**: courses listed as `in_progress` have no grade yet.

| File | Contents |
|---|---|
| `catalog.json` | Courses: title, credits, prerequisites, minimum prerequisite grade, terms usually offered |
| `sections.json` | Spring 2027 sections: days, start and end times, open seats, modality |
| `requirements.json` | General degree rules and the Computer Science major's required courses |
| `students.json` | Eight students: major, completed courses with grades, Fall 2026 courses in progress |
| `public_questions.json` | The ten public questions, with the fields of each message and the expected answer |

## Rules

Every tool and every expected answer follows these rules.

### Grades

- A passing grade is **D or better**. F earns no credit, and W (withdrawn) earns no credit.
- When a course was taken more than once, **only the latest attempt counts**.

### Eligibility for Spring 2027

A course's `prerequisites` is a list of **groups**: every group must be met, and inside a group **any one** course is enough. A group is met by a completed course whose latest grade is at least the course's `min_grade` (when `min_grade` is `null`, any passing grade). `check_eligibility` returns the first status that applies:

1. **`already_taken`**: the student has passed the course, or is taking it now.
2. **`not_eligible`**: at least one group is met neither by a completed course nor by a course in progress.
3. **`pending`**: every group is met, but at least one only by a course still in progress.
4. **`eligible`**: every group is met by completed courses.

### Schedule conflicts

- Two sections **conflict** when they meet on at least one common day **and** their times overlap: each starts before the other ends.
- Times that only touch do **not** conflict: a section ending at 10:40 and one starting at 10:40 can both be taken.
- Online asynchronous sections have no meeting times and never conflict.

### Degree progress (new)

- **`missing`**: every course in the major's `required` list that the student has not passed. A course in progress is **not** passed yet, so it is still missing.
- **`choose_one_done`**: true when, for every `choose_one` group, the student has passed at least one course in the group.
- Courses outside the major's lists do not count either way.

### Section picks (new)

A section can be picked for a student when **all** of these hold:

1. it is a Spring 2027 section of that course with **open seats** (`seats_open` above 0);
2. the student's eligibility for the course is **`eligible` or `pending`** (a student taking a prerequisite now may register for the next term);
3. it does **not conflict** with any section the student is already registered for;
4. it does **not conflict** with the other sections picked in the same answer.

When no section of a course meets rules 1–3, the answer for that course is **none** (`section_id` null). Any section that meets the rules is a right answer; the help desk does not have to pick a particular one.
