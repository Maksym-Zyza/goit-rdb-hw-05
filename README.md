# goit-rdb-hw-05

## task 1

```sql
Select *,
(select customer_id from orders o
where od.order_id = o.id) as customer_id
from order_details od;
```

## task 2

```sql
Select od.*, o.shipper_id as shipper_id
from order_details od
join orders o on o.id = od.order_id
where shipper_id in (
select shipper_id from orders where shipper_id = 3
);
```

## task 3

```sql
Select order_id, avg(quantity) as avg_quantity from (
select * from order_details od
where quantity > 10 
) as temp_table
group by order_id;
```

## task 4

```sql
With temp_table as (
select * from order_details od
where quantity > 10 
)
Select order_id, avg(quantity) as avg_quantity from temp_table 
group by order_id;
```

## task 5

```sql
Drop function if exists getDivisionOfParams;

Delimiter //
Create function getDivisionOfParams(first_num float, second_num float)
returns float
deterministic
no sql
begin
declare result float;
set result = first_num / second_num;
return result;
end //
Delimiter ;

select order_id, quantity, getDivisionOfParams(quantity, 3) as newQuantity
from order_details;
```
