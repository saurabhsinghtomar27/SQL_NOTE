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



