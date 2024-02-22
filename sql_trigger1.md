create table sys.passenger(
	id int(10),
    name varchar(20),
    address varchar(20),
    charges int(10),
    primary key(id));
    
select * from sys.passenger;  

insert into sys.passenger values(1, "Rebeca", "Tasnad", 3000);  
insert into sys.passenger values(2, "Paula", "Cluj", 6700);  
insert into sys.passenger values(3, "Ana", "SM", 23000);  
    
select * from sys.passenger;  



CREATE TRIGGER before_trigger
BEFORE INSERT
ON sys.passenger
FOR EACH ROW
SET NEW.charges = 2000;



INSERT INTO sys.passenger VALUES (9, 'Bogdan', 'Bucuresti', 2001);

SELECT * FROM sys.passenger;
