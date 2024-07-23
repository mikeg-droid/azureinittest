SELECT SUM(amount) AS Rental_Income, convert_store_address(staff.store_id) AS store 
FROM payment 
RIGHT JOIN staff ON payment.staff_id = staff.staff_id 
WHERE payment_date >= '2007-02-01 00:00:00.000000' AND payment_date <= '2007-03-01 00:00:00.000000' 
GROUP BY staff.store_id; 

 

SELECT rental_id AS transact_nr, amount, payment_date AS date, first_name AS Staff, convert_store_address(staff.store_id) AS store 
FROM payment 
RIGHT JOIN staff ON payment.staff_id = staff.staff_id 
WHERE payment_date >= '2007-02-01 00:00:00.000000' AND payment_date <= '2007-03-01 00:00:00.000000' 
ORDER BY payment_date ASC; 

 

CREATE FUNCTION convert_store_address(store_id INT)  
RETURNS VARCHAR(255) 
BEGIN 
    DECLARE address VARCHAR(255); 
    CASE  
        WHEN store_id = 1 THEN SET address = 'MySakila Dr, Lethbridge'; 
        WHEN store_id = 2 THEN SET address = 'MySQL Blvd, Woodridge'; 
        ELSE SET address = 'Unknown Store'; 
    END CASE; 
    RETURN address; 
END; 

 
