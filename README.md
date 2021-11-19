
LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/simon-cerda/graphs/main/graph_employees.csv' AS row
WITH row WHERE row.EmployeeId IS NOT NULL
MERGE (m1:Employee {employeeId: row.EmployeeId})
MERGE (m2:Employee {employeeId: coalesce(row.RM_id, "Unknown")})
MERGE (m1)-[:works_for]->(m2)
return *;

MERGE (:Employee {employeeId: row.EmployeeId, employeName: row.Name,Role: row.Role})
