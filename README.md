# Periodic Table Database

A Bash script that looks up chemical elements in a PostgreSQL database by atomic number, symbol or name. Built for the freeCodeCamp Relational Database certification.

## Usage
./element.sh 1
./element.sh H
./element.sh Hydrogen

## Files
- element.sh: the lookup script
- periodic_table.sql: database dump (rebuild with `psql -U postgres < periodic_table.sql`)
