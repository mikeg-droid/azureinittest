SELECT SUM(amount) AS Rental_Income, staff.store_id 

FROM payment 

RIGHT JOIN staff ON payment.staff_id = staff.staff_id 

WHERE payment_date >= '2007-02-01 00:00:00.000000' AND payment_date <= '2007-03-01 00:00:00.000000' 

GROUP BY staff.store_id; 



 

SELECT rental_id AS transact_nr, amount, payment_date AS date, first_name AS Staff, staff.store_id AS store 

FROM payment 

RIGHT JOIN staff ON payment.staff_id = staff.staff_id 

WHERE payment_date >= '2007-02-01 00:00:00.000000' AND payment_date <= '2007-03-01 00:00:00.000000' 

ORDER BY payment_date ASC; 
