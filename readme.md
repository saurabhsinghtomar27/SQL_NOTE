 # SQL NOTE

 ## 2nd Highest Salary
 ```sql
 select max(salary) from emp where salary not in (Select max(salary) from emp); 
 ```
 ```sql
 select max(salary) from emp where salary < (Select max(salary) from emp);
 ```

 ## Department wise highest Salary
 ```sql
 select max(sal),depno from emp group by depno;
 ```

 ## NO Of Employee in Each Department
 ```sql 
 select count(*),deptno from emp
 group by deptno;
 ```
## Display Alternate Records


## Display Duplicate of a Column and in asc order
```sql
select ename ,count(*) from emp order by count(*) having count(*)>1;
```

## Display epname whose name start white 'm'
```sql
select ename from emp where ename like 'M%';
```
## Display ename Ends with 'n'
```sql
select ename from emp where ename like '%m';
```
## Name contain 'm'
```sql
select ename from emp where ename like '%m%';
```

## M does not contain in name
```sql
select ename from emp where ename not like '%m%';
```
## Pattern 
only four character - like '____';
<br>
second letter 'L' and Fourth letter 'M' - like '_L_M';

## Display nth row in SQL
```sql
select *from (select rownum r ,ename,sal from emp) where r=6;
```
## Display 2th ,3rd row in SQL
```sql
select *from (select rownum r ,ename,sal from emp) where r in(2,3,7);
```
## Display Employee details getting more salary than their manager
### Self Join comes in Picture
```sql
select e1.name "employes",e2.name "manager" from emp e1 emp e2 where e2.empno=e1.mgr and e1.sal>e2.sal;
```

## Print Employee Manager both attribute are present in same table
```sql
select e1.name "employes",e2.name "manager" from emp e1 emp e2 where e2.empno=e1.mgr;
```
## Display 1st or last row
```sql
select * from (select rownum r,ename,sal from emp) where r=1 or r=(select count(*) from emp);
```
## Display last two row or first two
```sql 
select *from (Select rownum r,enmae,sal from emp) where r>(select count(*)-2 from emp) r in (1,2);
``` 
## Nth highest salary
```sql
select * from Employee ORDER BY sal 
DESC limit N-1,1;
```
### TOP 6th salary
```sql
select * from ((select * from Employee 
       ORDER BY `sal` DESC limit 6 ) AS T) 
       ORDER BY T.`sal` ASC limit 1;
```       

## Schema for LPU MYCLASS
### 1 Lpu will have multiple batches
### 2 Each batch will have multiple students
### 3 Each batch will have multiple classes
### 4 For Each class , we store info about name , date ,time ,instructor
### 5 For each student we store name email grad_year student_id
### 6 For every student has a buddy who is also a student
### 7 A student may more from one batch to another
### 8 for each batch change by student ,this record should be maintained havinf shifting date and batch details
### 9 student is assigned a mentor
### 10 For every mentor their name and company
### 11 store info about mentor session ,time ,duration student,mentor,rating
### 12 every batch we store if it online or offline
## Cardinality M:M Relationship Create a Mapping Table
## creating index in sql for fast access 
```sql
CREATE INDEX idx_pname
ON Persons (LastName, FirstName);
```
## Rank

### Rank() -> It will assign the rank and if same rank occurs it will give same rank and miss the the next rank number
### Dense_Rank() -> it will not miss the next rank number
### Row_Number()-> it will give rank differently no same rank
```sql 
select * Rank() over(order by salary desc) from employess
```
### if we partition rank by some groups
```sql 
select * Rank() over(partiton by level order by salary desc) from employess
```
## Row Between
### suppose i want a calculate sum of sales of n previous and m next days and showcase it at same day
```sql
select *, sum(sales) over(order by date rows between n preceding and m following) from sales;
```
### sum of all above rows abn below
```sql
select *, sum(sales) over(order by date rows between unbounded preceding and unbounded following) from sales;
```
### calculate previous days sales
```sql
select *, sum(sales) over(order by date rows between unbounded preceding and current row) from sales;
```
## First Value and Last Value
### calculate the first day sale value
```sql 
select *,First_Value(sales) over (partition by state order by date ) first_daysale,
Last_value(sales) over (partition by state order by date rows between unbounded preceding and unbounded following) last_day_sale from sales;
```
## Moving Average
### it is used to see some trends and pattern in dataset
### it is used to remove the noise in graph example stock market price
```sql
select date,price ,avg(price) over(order by date row between 2 preceding and current row) as three_day_moving_average from stock;
```
## lead and lag
### lead- dealing with the below row
### lag- dealing with the above row
```sql
lag(run) take the previous 1 row
lead(run) take the next 1 row
```
## String AGG
### it is used to merge or combine many rows into 1 
### eg - combine customer all orders in one row
```sql 
select custid, string_agg(detail,',') from (select custid,concat(item,'-',quantity)detail from details)a
group by custid;
```
 ## CTE Common Table Expression
 ```sql
 with newtablename(columns) as
 (
       sql query
 )
 ```
## recursive cte
```sql
with recursive cte_numbers(n) as (
select 1 union All
  select n+1 from cte_numbers where n<10
  ) select n, concat(n,' x ','2'), n*2 from cte_numbers;
  ```


