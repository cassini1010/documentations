# SQL

## ALTER TABLE

```sql
ALTER TABLE testing
ADD COLUMN test_age INTEGER;
```

Remove a column

```sql
ALTER TABLE testing
DROP COLUMN test_age;
```

## SELECT

If `hero` is a table, then below command can be used to select hero_age column from it.

```sql
SELECT hero_age from hero;

OR

SELECT hero.hero_age from hero;
```

To select distinct items from a column,

```sql
SELECT DISTINCT hero_age from hero;
```

## Interview Questions

1. Difference between `where` and `having` 
   
   Both the clauses are used to apply conditions on data. Where is used to applu conditions on a table like data, on the other hand Having is used to apply conditoins on data returned by aggregate functions like count(), avg(), max(), min() etc... These functions return a scalar value and not set of values(table like structure).
