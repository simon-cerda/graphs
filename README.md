LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/simon-cerda/graphs/main/graph_employees.csv' AS row
WITH row WHERE row.EmployeeId IS NOT NULL
MERGE (m1:Employee {employeeName: row.Name, Role:row.Role}) 
MERGE (m2:Employee {employeeName: coalesce(row.RM_Name, "Unknown")})
MERGE (m1)-[:works_for]->(m2) return *;
