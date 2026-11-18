# Periodic Table Database

A command-line tool that looks up chemical elements in a **PostgreSQL** database by atomic number, symbol or name, written in **Bash**. Built as part of the freeCodeCamp Relational Database certification.

## What it does

Give the script an element in any of three forms and it prints that element's details:

```bash
./element.sh 1
./element.sh H
./element.sh Hydrogen
```

Output:

```
The element with atomic number 1 is Hydrogen (H). It's a nonmetal, with a mass of 1.008 amu. Hydrogen has a melting point of -259.1 celsius and a boiling point of -252.9 celsius.
```

It also handles bad input:

| Input | Output |
|---|---|
| No argument | `Please provide an element as an argument.` |
| Element not in the database | `I could not find that element in the database.` |

## What I fixed in the database

The project started with a database that had mistakes in it. I:

- Renamed columns to clearer names (`weight` → `atomic_mass`, `melting_point` → `melting_point_celsius`, `boiling_point` → `boiling_point_celsius`)
- Added `NOT NULL` and `UNIQUE` constraints to protect the data
- Added foreign keys linking `properties` to `elements` and `types`
- Moved element types into their own `types` table (normalisation)
- Capitalised element symbols and removed trailing zeros from atomic masses
- Deleted an invalid element (atomic number 1000)
- Added Fluorine and Neon
- Found and removed duplicate constraints using `\d elements`

## Database design

| Table | Columns |
|---|---|
| `elements` | `atomic_number` (primary key), `symbol` (unique, not null), `name` (unique, not null) |
| `properties` | `atomic_number` (foreign key → elements), `atomic_mass`, `melting_point_celsius`, `boiling_point_celsius`, `type_id` (foreign key → types) |
| `types` | `type_id` (primary key), `type` |

## How to run it

1. Rebuild the database from the dump:
   ```bash
   psql -U postgres < periodic_table.sql
   ```
2. Make the script executable:
   ```bash
   chmod +x element.sh
   ```
3. Run it:
   ```bash
   ./element.sh Ne
   ```

## Files

- `element.sh`: the lookup script
- `periodic_table.sql`: database dump that rebuilds the `periodic_table` database

## Tech used

- **Bash**: scripting, input validation, string parsing
- **PostgreSQL**: schema changes, constraints, joins, data cleaning
- **Git**: version control with conventional commit messages (`feat:`, `fix:`, `chore:`)

## What I learned

- Fixing and restructuring an existing database without losing data
- Using constraints and foreign keys to keep data valid
- Joining multiple tables in a query from a Bash script
- Debugging a database by inspecting its structure
- Working with Git branches and meaningful commit history
