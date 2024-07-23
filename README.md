CREATE OR REPLACE FUNCTION convert_store_address(store_id INT) 
RETURNS VARCHAR AS $$
BEGIN
    CASE 
        WHEN store_id = 1 THEN
            RETURN 'MySakila Dr, Lethbridge';
        WHEN store_id = 2 THEN
            RETURN 'MySQL Blvd, Woodridge';
        ELSE
            RETURN 'Store not configured';
    END CASE;
END;
$$ LANGUAGE plpgsql;


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

 
Section C 

CREATE TABLE rental_summary( 
rental_income DECIMAL(10, 2), 
store VARCHAR(255) 
); 

CREATE TABLE detailed_rentals_report ( 
transact_nr INT PRIMARY KEY, 
amount DECIMAL(5, 2), 
date TIMESTAMP, 
staff VARCHAR(50), 
store VARCHAR(255) 
); 

Section D

INSERT INTO detailed_rentals_report (transact_nr, amount, date, staff, store) 
SELECT rental_id AS transact_nr, amount, payment_date AS date, first_name AS staff, convert_store_address(staff.store_id) AS store   
FROM payment   
RIGHT JOIN staff ON payment.staff_id = staff.staff_id  WHERE payment_date >= '2007-02-01 00:00:00' AND payment_date <= '2007-03-01 00:00:00'   
ORDER BY payment_date ASC; 


