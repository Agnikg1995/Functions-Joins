1. Adding a new column called DOB in Persons table
--To add the DOB column to the Persons table:
ALTER TABLE Persons
ADD COLUMN DOB DATE;
2. Writing a user-defined function to calculate age using DOB
DELIMITER //

CREATE FUNCTION CalculateAge(dateOfBirth DATE)
RETURNS INT
BEGIN
    DECLARE age INT;
    SET age = YEAR(CURRENT_DATE()) - YEAR(dateOfBirth);
    IF (MONTH(CURRENT_DATE()) < MONTH(dateOfBirth)) OR
       (MONTH(CURRENT_DATE()) = MONTH(dateOfBirth) AND DAYOFMONTH(CURRENT_DATE()) < DAYOFMONTH(dateOfBirth)) THEN
        SET age = age - 1;
    END IF;
    RETURN age;
END //

DELIMITER ;
3. Writing a select query to fetch the Age of all persons using the function
SELECT
    P.Id,
    P.Fname,
    P.Lname,
    P.DOB,
    CalculateAge(P.DOB) AS Age,
    P.Country_name
FROM
    Persons P;
4. Performing inner join, left join, and right join on the tables

Inner Join:
SELECT
    P.Id,
    P.Fname,
    P.Lname,
    P.DOB,
    CalculateAge(P.DOB) AS Age,
    P.Country_name,
    C.Country_name AS Country_Name
FROM
    Persons P
INNER JOIN
    Country C ON P.Country_Id = C.Id;
Left Join:
SELECT
    P.Id,
    P.Fname,
    P.Lname,
    P.DOB,
    CalculateAge(P.DOB) AS Age,
    P.Country_name,
    C.Country_name AS Country_Name
FROM
    Persons P
LEFT JOIN
    Country C ON P.Country_Id = C.Id;
Right Join:
SELECT
    P.Id,
    P.Fname,
    P.Lname,
    P.DOB,
    CalculateAge(P.DOB) AS Age,
    P.Country_name,
    C.Country_name AS Country_Name
FROM
    Persons P
RIGHT JOIN
    Country C ON P.Country_Id = C.Id;
