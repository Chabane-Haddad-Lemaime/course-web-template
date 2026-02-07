# SAS PROC SQL Tutorial

This tutorial is a practical introduction to `PROC SQL` in SAS. It covers the core syntax, common query patterns, and a few advanced techniques.

## 1) What is PROC SQL?

`PROC SQL` lets you query and manipulate SAS data sets using SQL syntax.

- Read/filter data (`SELECT`, `WHERE`)
- Sort and summarize (`ORDER BY`, aggregate functions)
- Join tables (`INNER`, `LEFT`, etc.)
- Create new tables/views (`CREATE TABLE`, `CREATE VIEW`)
- Update/delete rows (`UPDATE`, `DELETE`, `INSERT`)

---

## 2) Basic PROC SQL Structure

```sas
proc sql;
   /* SQL statements */
quit;
```

You can run multiple SQL statements inside one `proc sql; ... quit;` block.

---

## 3) SELECT Columns

```sas
proc sql;
   select id, name, salary
   from work.employees;
quit;
```

Use `*` to select all columns:

```sas
proc sql;
   select *
   from work.employees;
quit;
```

---

## 4) Filter Rows with WHERE

```sas
proc sql;
   select id, name, dept, salary
   from work.employees
   where dept = 'IT' and salary > 70000;
quit;
```

Useful operators:

- `=` `^=` (or `ne`) `>` `<` `>=` `<=`
- `between ... and ...`
- `in (...)`
- `like 'A%'`
- `is null` / `is not null`

---

## 5) Create Computed Columns

```sas
proc sql;
   select name,
          salary,
          salary * 0.10 as bonus,
          salary + calculated bonus as total_comp
   from work.employees;
quit;
```

`calculated` lets you reuse a column alias from earlier in the same `SELECT` list.

---

## 6) Remove Duplicates with DISTINCT

```sas
proc sql;
   select distinct dept
   from work.employees;
quit;
```

---

## 7) Sort Output with ORDER BY

```sas
proc sql;
   select name, dept, salary
   from work.employees
   order by dept asc, salary desc;
quit;
```

---

## 8) Group and Summarize

```sas
proc sql;
   select dept,
          count(*) as n_emp,
          avg(salary) as avg_salary format=dollar10.2,
          min(salary) as min_salary,
          max(salary) as max_salary
   from work.employees
   group by dept;
quit;
```

Use `having` to filter aggregated results:

```sas
proc sql;
   select dept,
          avg(salary) as avg_salary
   from work.employees
   group by dept
   having avg(salary) > 80000;
quit;
```

---

## 9) Join Tables

Assume:

- `work.employees(emp_id, name, dept_id, salary)`
- `work.departments(dept_id, dept_name)`

### Inner Join

```sas
proc sql;
   select e.emp_id,
          e.name,
          d.dept_name,
          e.salary
   from work.employees as e
   inner join work.departments as d
      on e.dept_id = d.dept_id;
quit;
```

### Left Join

```sas
proc sql;
   select e.emp_id,
          e.name,
          d.dept_name
   from work.employees as e
   left join work.departments as d
      on e.dept_id = d.dept_id;
quit;
```

---

## 10) Create a New Table

```sas
proc sql;
   create table work.high_paid as
   select emp_id, name, salary
   from work.employees
   where salary >= 100000;
quit;
```

Create a view instead of a physical table:

```sas
proc sql;
   create view work.v_high_paid as
   select emp_id, name, salary
   from work.employees
   where salary >= 100000;
quit;
```

---

## 11) Insert, Update, Delete

### Insert

```sas
proc sql;
   insert into work.departments
      (dept_id, dept_name)
   values
      (50, 'Analytics');
quit;
```

### Update

```sas
proc sql;
   update work.employees
      set salary = salary * 1.05
   where dept_id = 50;
quit;
```

### Delete

```sas
proc sql;
   delete from work.employees
   where emp_id = 9999;
quit;
```

---

## 12) Use Macro Variables in PROC SQL

Store query result in a macro variable:

```sas
proc sql noprint;
   select count(*)
   into :n_employees
   from work.employees;
quit;

%put Number of employees = &n_employees.;
```

Multiple values into one macro variable:

```sas
proc sql noprint;
   select dept_name
   into :dept_list separated by ', '
   from work.departments;
quit;

%put Departments: &dept_list.;
```

---

## 13) Useful PROC SQL Options

- `noprint` — suppress printed output
- `outobs=` — limit output rows
- `inobs=` — limit input rows read
- `feedback` — expand `*` and show resolved query in log
- `stimer` — timing statistics

Example:

```sas
proc sql feedback outobs=10;
   select *
   from work.employees;
quit;
```

---

## 14) Performance Tips

1. Keep only needed columns (`select col1, col2` instead of `select *`).
2. Filter early (`where`) before joins/aggregations when possible.
3. Index frequently filtered/joined columns.
4. Avoid functions on indexed columns in `where` when possible.
5. Use views for reusable logic; tables for repeated heavy workloads.

---

## 15) End-to-End Example

```sas
proc sql;
   create table work.dept_summary as
   select d.dept_name,
          count(e.emp_id) as n_emp,
          avg(e.salary) as avg_salary format=dollar10.2,
          sum(e.salary) as total_salary format=dollar12.2
   from work.departments as d
   left join work.employees as e
      on d.dept_id = e.dept_id
   group by d.dept_name
   having calculated total_salary > 100000
   order by calculated total_salary desc;
quit;
```

---

## 16) Quick Practice Tasks

1. Return the top 5 highest-paid employees.
2. Count employees by department.
3. Find departments with average salary above 90,000.
4. Create a table of employees hired this year.
5. Left join employees to departments and show employees without a matched department.

---

If you want, I can also provide:

- A beginner exercise set with solutions,
- A `PROC SQL` cheat sheet (one-page), or
- A comparison of `DATA step` vs `PROC SQL` for common tasks.
