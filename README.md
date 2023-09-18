# Segundo projeto em PowerBI para o Bootcamp da dio

queries do Mysql usadas:

//Para atualizar a tabela employee com o nome dos departamentos associados aos colaboradores//

ALTER TABLE employee
ADD COLUMN Dname varchar(15);
UPDATE employee e
JOIN departament d ON e.Dno = d.Dnumber
SET e.Dname = d.Dname;

//para criar uma coluna na tabela de employees com o nome e sobrenome do gestor//

ALTER TABLE employee
ADD COLUMN ManagerFullName VARCHAR(30);
UPDATE employee e
LEFT JOIN employee m ON e.Super_ssn = m.Ssn
SET e.ManagerFullName = CONCAT(m.Fname, ' ', m.Lname)
WHERE e.Super_ssn IS NOT NULL;

//para criar coluna com nome completo do empregado//

ALTER TABLE employee
ADD COLUMN FullName VARCHAR(30);
UPDATE employee
SET Fullname = CONCAT(Fname, ' ', Lname)
ALTER TABLE employee
DROP COLUMN Fname,
DROP COLUMN Lname;

//mesclando a localização e o numero do departamento//

ALTER TABLE dept_locations
ADD COLUMN MergedLocation VARCHAR(20);
UPDATE dept_locations
SET MergedLocation = CONCAT(Dnumber, ' - ', Dlocation);

A razão pela qual você pode simplesmente mesclar os valores e não precisa atribuir os valores originais a uma nova coluna é que a mesclagem desses valores é uma operação não destrutiva e não afeta a integridade dos dados originais.
Neste caso existe uma constraint no Dnumber, ela é necessária em uma restrição da chave estrangeira 'fk_dept_locations'.

