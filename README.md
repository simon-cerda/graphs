MATCH (n)
DETACH DELETE n;
LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/simon-cerda/graphs/main/graph_employees.csv' AS row
WITH row WHERE row.EmployeeId IS NOT NULL
MERGE (e:Employee {employeeName: row.Name, employeeId: row.EmployeeId, Role: row.Role})
MERGE (b:Employee {employeeName: coalesce(row.RM_Name, "Unknown")})
MERGE (s:Skill {skill: row.programming_skill})
MERGE (h:Hobbies {hobbies: row.hobby})
MERGE (e)-[:works_for]->(b)
MERGE (e)-[:skillset]->(s)
MERGE (e)-[:hobby] -> (h)
return *;

https://cloud.google.com/architecture/ml-on-gcp-best-practices#use-tensorflow-extended-when-leveraging-tensorflow-ecosystem
