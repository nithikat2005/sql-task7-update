
SQL TASK7:
✅ Create Database
✅ Create Tables
✅ Insert Sample Data
✅ Create Complex Views using JOIN, WHERE, GROUP BY, AGGREGATE
✅ Example SELECT from the views




-- Create Database
CREATE DATABASE CompanyDB;
USE CompanyDB;

-- Create Tables
CREATE TABLE Employees (
    emp_id INT PRIMARY KEY AUTO_INCREMENT,
    emp_name VARCHAR(100),
    department VARCHAR(50),
    salary DECIMAL(10,2)
);

CREATE TABLE Projects (
    project_id INT PRIMARY KEY AUTO_INCREMENT,
    project_name VARCHAR(100),
    emp_id INT,
    hours_worked INT,
    FOREIGN KEY (emp_id) REFERENCES Employees(emp_id)
);

-- Insert Sample Data
INSERT INTO Employees (emp_name, department, salary) VALUES
('Arun', 'IT', 50000),
('Bala', 'HR', 40000),
('Kumar', 'IT', 55000),
('Divya', 'Finance', 45000);

INSERT INTO Projects (project_name, emp_id, hours_worked) VALUES
('Website Dev', 1, 40),
('Recruitment', 2, 30),
('App Dev', 1, 50),
('Audit', 4, 20),
('Cloud Setup', 3, 45);

----------------------------------------
-- 1️⃣ CREATE VIEW WITH COMPLEX SELECT
----------------------------------------

-- View: Employee and their project details
CREATE VIEW EmpProjectView AS
SELECT 
    e.emp_id,
    e.emp_name,
    e.department,
    p.project_name,
    p.hours_worked,
    e.salary,
    (p.hours_worked * 500) AS project_value
FROM Employees e
LEFT JOIN Projects p
ON e.emp_id = p.emp_id
WHERE e.salary > 40000
ORDER BY e.emp_name;

----------------------------------------
-- 2️⃣ VIEW FOR ABSTRACTION & SECURITY
----------------------------------------

-- Hide salary, show only basic info
CREATE VIEW EmpPublicView AS
SELECT 
    emp_name,
    department
FROM Employees;

----------------------------------------
-- 3️⃣ VIEW WITH GROUP BY & AGGREGATE
----------------------------------------

CREATE VIEW DepartmentSalaryStats AS
SELECT 
    department,
    COUNT(*) AS total_employees,
    AVG(salary) AS avg_salary,
    MAX(salary) AS max_salary
FROM Employees
GROUP BY department;

----------------------------------------
-- 4️⃣ USING THE VIEWS
----------------------------------------

-- Fetch employee project details
SELECT * FROM EmpProjectView;

-- Fetch public employee data (for security)
SELECT * FROM EmpPublicView;

-- Fetch department salary statistics
SELECT * FROM DepartmentSalaryStats;

OUTPUT:
<img width="1656" height="861" alt="Screenshot 2025-11-24 185201" src="https://github.com/user-attachments/assets/18e355e9-d5b0-4fb8-ba0e-fc7eeaefa66d" />
<img width="1004" height="332" alt="Screenshot 2025-11-24 185354" src="https://github.com/user-attachments/assets/631e574a-a3d2-4a95-b8b9-df7ad19a20fd" />
<img width="992" height="448" alt="Screenshot 2025-11-24 185413" src="https://github.com/user-attachments/assets/40941974-4e03-481c-b04a-22c09ea1b59d" />
<img width="1291" height="494" alt="Screenshot 2025-11-24 185433" src="https://github.com/user-attachments/assets/cd83f936-d8aa-43cf-a343-752d790c6fc6" />


