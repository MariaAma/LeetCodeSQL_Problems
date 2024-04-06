# 1378. Replace Employee ID With The Unique Identifier

SELECT name, unique_id
FROM Employees
LEFT JOIN EmployeeUNI ON Employees.id = EmployeeUNI.id;

# 1068. Product Sales Analysis I

SELECT Product.product_name, Sales.year, Sales.price
FROM Sales
INNER JOIN Product
ON Sales.product_id  = Product.product_id;

# 1581. Customer Who Visited but Did Not Make Any Transactions

SELECT customer_id, COUNT(visit_id) AS count_no_trans 
FROM Visits
WHERE visit_id NOT IN (SELECT visit_id FROM Transactions)
GROUP BY customer_id;

# 197. Rising Temperature

SELECT id
FROM (SELECT *, LAG (temperature) OVER (ORDER BY recordDate ASC) AS prTemp,
      LAG (recordDate) OVER (ORDER BY recordDate ASC) AS D
FROM Weather) AS W
WHERE temperature > prTemp AND DATEDIFF(recordDate, D)=1;

# 1661. Average Time of Process per Machine

SELECT machine_id, ROUND(AVG(end_timestamp - start_timestamp),3) AS processing_time
FROM (SELECT st.machine_id, st.process_id, st.timestamp AS start_timestamp, end.timestamp AS end_timestamp
FROM Activity AS st
LEFT JOIN Activity AS end
ON end.process_id= st.process_id AND end.machine_id= st.machine_id
WHERE st.activity_type ="start" AND end.activity_type ="end") AS T
GROUP BY machine_id;

# 577. Employee Bonus

SELECT Employee.name, Bonus.bonus 
FROM Employee 
LEFT JOIN Bonus ON Employee.empId = Bonus.empId
WHERE Bonus.bonus < 1000 OR Bonus.bonus IS NULL;

# 1280. Students and Examinations

SELECT A.student_id, student_name, A.subject_name, IFNULL(times, 0) AS attended_exams
FROM (SELECT student_id, student_name, subject_name 
      FROM Students
      CROSS JOIN Subjects) A
LEFT JOIN (SELECT student_id, subject_name, COUNT(*) AS times
           FROM Examinations 
           GROUP BY student_id, subject_name) B
ON A.student_id = B.student_id AND A.subject_name = B.subject_name
ORDER BY A.student_id, A.subject_name;

# 570. Managers with at Least 5 Direct Reports

SELECT name
FROM Employee E
JOIN (SELECT managerId
           FROM Employee
           GROUP BY managerId
           HAVING COUNT(managerId) >= 5) A
ON E.id =A.managerId;

# 1934. Confirmation Rate

SELECT S.user_id, ROUND(AVG(IF(C.action="confirmed",1,0)),2) AS confirmation_rate
FROM Signups S 
LEFT JOIN Confirmations C 
ON S.user_id = C.user_id 
GROUP BY S.user_id;

# 620. Not Boring Movies

SELECT id, movie, description, rating
FROM Cinema
WHERE mod(id,2) != 0 AND description != "boring"
ORDER BY rating DESC;

# 1251. Average Selling Price

SELECT P.product_id, IFNULL(ROUND(SUM(P.price*US.units)/SUM(US.units),2),0) AS average_price 
FROM Prices P
LEFT JOIN UnitsSold US
ON P.product_id = US.product_id 
AND US.purchase_date BETWEEN P.start_date AND P.end_date
GROUP BY P.product_id;

# 1075. Project Employees I

SELECT P.project_id, ROUND(AVG(E.experience_years),2) AS average_years  
FROM Project P
LEFT JOIN Employee E
ON P.employee_id  = E.employee_id  
GROUP BY P.project_id;

# 1633. Percentage of Users Attended a Contest

SELECT contest_id, 
ROUND((COUNT(R.user_id)*100 / (SELECT COUNT(user_id) FROM Users)) ,2) AS percentage
FROM Register R
LEFT JOIN Users U 
ON U.user_id = R.user_id
GROUP BY contest_id
ORDER BY percentage DESC, contest_id ASC;

# 1211. Queries Quality and Percentage

SELECT query_name, ROUND(AVG(rating/position),2) AS quality, 
ROUND(AVG(rating<3)*100,2) AS poor_query_percentage 
FROM Queries
WHERE query_name IS NOT NULL
GROUP BY query_name; 

# 1193. Monthly Transactions I

SELECT DATE_FORMAT(trans_date, '%Y-%m') AS month, country, COUNT(trans_date) AS trans_count,
SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END) AS approved_count,
SUM(amount) AS trans_total_amount ,
SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END) AS approved_total_amount 
FROM Transactions 
GROUP BY DATE_FORMAT(trans_date, '%Y-%m'), country;

# 1174. Immediate Food Delivery II

SELECT ROUND(SUM(customers)*100/COUNT(DISTINCT customer_id),2) AS immediate_percentage 
FROM (SELECT customer_id, IF(MIN(order_date) = MIN(customer_pref_delivery_date), 1, 0) AS customers
FROM Delivery
GROUP BY customer_id) AS D;

# 550. Game Play Analysis IV

SELECT ROUND(COUNT(player_id)/(SELECT COUNT(DISTINCT player_id) FROM Activity),2) AS fraction 
FROM Activity 
WHERE (player_id, DATE_ADD(event_date, INTERVAL -1 DAY))
    IN (
        SELECT player_id, MIN(event_date) AS first_login FROM Activity GROUP BY player_id
    );

# 2356. Number of Unique Subjects Taught by Each Teacher

SELECT teacher_id, COUNT(DISTINCT subject_id) AS cnt 
FROM Teacher
GROUP BY teacher_id;

# 1141. User Activity for the Past 30 Days I

SELECT activity_date AS day, COUNT(DISTINCT user_id) AS active_users  
FROM Activity
WHERE (activity_date > "2019-06-27" AND activity_date <= "2019-07-27")
GROUP BY activity_date;

# 1070. Product Sales Analysis III

SELECT product_id, year AS first_year, quantity, price
FROM Sales 
WHERE (product_id, year)
    IN (SELECT product_id, MIN(year) FROM Sales group by product_id);

# 596. Classes More Than 5 Students

SELECT class
FROM Courses
GROUP BY class
HAVING COUNT(DISTINCT student) >= 5;

# 1729. Find Followers Count

SELECT user_id, COUNT(follower_id) AS followers_count
FROM Followers 
GROUP BY user_id
ORDER BY user_id ASC;

# 619. Biggest Single Number

SELECT MAX(num) AS num
FROM MyNumbers 
WHERE num IN (SELECT num FROM MyNumbers GROUP BY num HAVING COUNT(*)=1);

# 1045. Customers Who Bought All Products

SELECT customer_id 
FROM Customer 
GROUP BY customer_id
HAVING COUNT(distinct product_key) = (SELECT COUNT(DISTINCT product_key) FROM Product);

# 1731. The Number of Employees Which Report to Each Employee

SELECT E.employee_id, E.name, COUNT(M.reports_to) AS reports_count, ROUND(AVG(M.age),0) AS average_age 
FROM Employees E
JOIN Employees M
ON E.employee_id = M.reports_to
WHERE E.employee_id IN 
    (
    SELECT reports_to 
    FROM Employees
)
GROUP BY E.employee_id
ORDER BY E.employee_id;

# 1789. Primary Department for Each Employee

SELECT employee_id, department_id
FROM Employee
WHERE (employee_id, department_id) IN
    (
    SELECT employee_id, department_id
    FROM Employee
    GROUP BY employee_id 
    HAVING COUNT(DISTINCT department_id)=1
    UNION
    SELECT employee_id, department_id
    FROM Employee
    WHERE primary_flag = 'Y'    
    );

# 610. Triangle Judgement

SELECT x,y,z, 
    CASE 
        WHEN x+y>z AND x+z>y AND y+z>x
        THEN 'Yes' 
        ELSE 'No' 
    END AS triangle 
FROM Triangle;

# 180. Consecutive Numbers






