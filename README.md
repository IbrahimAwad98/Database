# Library Database

A normalised MySQL schema for a library system, with an ER diagram and the
course report that goes with it.

This repository is a database design exercise. There is no application code —
the deliverables are the schema, the diagram, and the documentation.

## What is here

| File | What it is |
| --- | --- |
| `Library-sql` | The schema: 12 tables, foreign keys, and seed data. Note there is no `.sql` extension. |
| `Library.png` | The ER diagram, exported. |
| `Library.drawio` | The editable diagram source, for draw.io / diagrams.net. |
| `Library system database.docx` | The course report — requirements, normalisation, and query explanations. |

## The schema

Twelve tables covering members, libraries, books, copies, loans and a
reservation queue:

`T_Member`, `T_Library`, `T_Member_Phone`, `T_Member_Email`, `T_Book`,
`T_Genre`, `T_Book_Genre`, `T_Author`, `T_Book_Author`, `T_Copy`, `T_Loan`,
`T_Book_Queue`

Design points worth pointing at:

- **Junction tables** for the many-to-many relationships — `T_Book_Genre` and
  `T_Book_Author` — plus `T_Book_Queue`, which carries a queue position
  alongside the member/book pair.
- **Multivalued attributes normalised out**: `T_Member_Phone` and
  `T_Member_Email` each hold a composite primary key, so a member can have
  several of either.
- **Copies separated from titles.** `T_Book` is the bibliographic record;
  `T_Copy` is the physical item that gets borrowed, which is what `T_Loan`
  references.
- **`ON DELETE CASCADE` and `ON UPDATE CASCADE` on all twelve foreign keys.**
- Loans carry `borrowDate`, `dueDate`, `returnDate`, an `extensionCount` capped
  by a `CHECK`, and an `ENUM` status of active / returned / overdue / extended.

Seed data covers all twelve tables: 6 members, 2 libraries, 2 books, 3 copies,
18 loans and 9 queue entries.

The file ends with **11 example queries — all commented out**, numbered 6 to 17.
They are the assignment answers: multi-table joins, `GROUP_CONCAT` aggregation,
overdue detection, and a loan-rate percentage. Uncomment one to run it.

## Requirements

**MySQL 8.0.16 or newer.** Two things set that floor: `DEFAULT (CURDATE())` is
an expression default and needs 8.0.13+, and the `CHECK` constraint on
`extensionCount` is parsed but silently ignored before 8.0.16.

This schema is **MySQL only**. It uses backtick identifiers, `AUTO_INCREMENT`,
inline `ENUM`, `USE`, `CURDATE()` and `GROUP_CONCAT`, none of which PostgreSQL
or SQL Server accept.

## Loading the schema

> **This script is destructive.** Its first statement is
> ``DROP DATABASE IF EXISTS `Library`;``. Any existing database named `Library`
> is removed without warning.

```bash
mysql -u root -p < Library-sql
```

Do not pass a database name — the script creates and selects `Library` itself.

In PowerShell, `<` is not an input redirect, so pipe instead:

```powershell
Get-Content Library-sql | mysql -u root -p
```

Or load it from inside the client, which avoids any re-encoding of the Swedish
characters in the comments:

```
mysql> source Library-sql;
```

## Known gaps

- **Loading the file destroys any existing `Library` database.** There is no
  guard and no prompt.
- **The cascades are aggressive.** Because every foreign key cascades on
  delete, removing one book removes its copies, which removes every loan ever
  made against them — the borrowing history disappears with the title.
- **`UNIQUE(copyID, borrowDate)` does not prevent double lending.** It only
  blocks two loans of the same copy starting on the same date, not two
  overlapping loans. The seed data already contains a copy on two simultaneously
  active loans.

## License

[MIT](LICENSE)
