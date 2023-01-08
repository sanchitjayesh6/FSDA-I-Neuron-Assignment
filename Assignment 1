# Task - 1

create table shopping_history(
product varchar(50) not null,
quantity int not null,
unit_price int not null);

insert into shopping_history values 
('milk' , 3 , 10), 
('bread' , 7 , 3),
('bread' , 5 , 2);

select * from shopping_history;

select product , sum(quantity * unit_price) as Total_Amount
 from shopping_history group by product order by product desc;
 
 -----------------------------------------------End------------------------------------------------------------------------------------------------------
 # Task - 2
 
 CREATE TABLE PHONES(
`NAME` VARCHAR (50) NOT NULL UNIQUE,
PHONE_NUMBER INT NOT NULL UNIQUE);

INSERT INTO PHONES VALUES ('JACK' , 1234 ),
('LENA' , 3333) ,
('MARK' , 9999) ,
('ANNA' , 7582);

SELECT * FROM PHONES;

CREATE TABLE CALLS (
ID INT NOT NULL UNIQUE,
CALLER INT NOT NULL,
CALLEE INT NOT NULL,
DURATION INT NOT NULL);

INSERT INTO CALLS VALUES (27 , 1234 , 7582 , 8),
(7 , 9999 , 7582 , 1),
(18 , 9999 , 3333 , 4),
(2 , 7582 , 3333 , 3),
(3 , 3333 , 1234 , 1),
(21 , 3333 , 1234 , 1);

SELECT * FROM CALLS;

# Method : 1

create temporary table temp_table (
select phones.`name` , phones.PHONE_NUMBER, sum(calls.DURATION) as Total_duration from
phones join calls on phones.PHONE_NUMBER = calls.CALLER
group by phones.`NAME`
union
select phones.`name` , phones.PHONE_NUMBER, sum(calls.DURATION) as Total_duration from
phones join calls on phones.PHONE_NUMBER = calls.CALLEE
group by phones.`NAME`);

create temporary table temp_table_1(
select `name` , sum(total_duration) as Total_call_duration
from temp_table
group by `name`);

select `name` , Total_call_duration 
from temp_table_1 
where total_call_duration >= 10;

# Method : 2

with call_list as
(
select CALLER as clr,DURATION from CALLS
union all
select CALLEE as cle,DURATION from CALLS
)
select p.name
from call_list as cl
join PHONES as p on p.PHONE_NUMBER=cl.clr
group by cl.clr,p.name
having sum(cl.duration)>=10;

-----------------------------------------------------End--------------------------------------------------------------------------
# Task - 3

create table transactions (
amount integer not null,
date date not null
);

insert into transactions values (1000 ,'2020-01-06'),
(-10 ,'2020-01-14'),
(-75 ,'2020-01-20'),
(-5 ,'2020-01-25'),
(-4 ,'2020-01-29'),
(2000 ,'2020-03-10'),
(-75 ,'2020-03-12'),
(-20 ,'2020-03-15'),
(40 ,'2020-03-15'),
(-50 ,'2020-03-17'),
(200 ,'2020-10-10'),
(-200 ,'2020-10-10');

select * from transactions;


WITH ANSWER AS(
with cte as (
select * ,
sum(amount) over (partition by month (`date`))
 as Total_Amount ,
count(amount) over ( partition by month(`date`)) as No_of_tnx from transactions
where amount like '-%')
select * from
cte where Total_Amount < -100
 and No_of_tnx >= 3
 group by Total_Amount)

(select sum(amount) - ( 12 -(select distinct( count(*))  from ANSWER)) * (5) AS Balance
from transactions) ;
