# Docker Note

## Run image(s)

Create a new container from a PostgreSQL image

	> docker run --name sgobain_db -it -p 5433:5432 -d postgres:9.6
	
Create database (Optional)

	> docker exec -it sgobain_db createdb -U postgres saint-gobain
	
Connect to the database in the container

	> psql -h localhost -p 5433 -U postgres

Create table for the referendum data

	CREATE TABLE referendum (
	code_departement char(3),
	name_departement varchar(40) NOT NULL,
	code_commune char(3),
	name_commune text NOT NULL,
	inscrits integer,
	absentions integer,
	blancs integer,
	choix_a integer,
	choix_b integer);

Copy the data to database

	psql=# \copy referendum from /Users/icshih/Data/Saint-Gobain/Referendum.csv with DELIMITER ';' CSV HEADER
	
Create table for the population data (partial)

	CREATE TABLE pop_departement (
	code_departement char(3),
	name_commune text NOT NULL,
	P13_H2064 integer,
	P13_H65P integer,
	P13_F2064 integer,
	P13_F65P integer);
	
Copy the population data to database

	 psql=#  \copy pop_departement from /Users/icshih/Data/Saint-Gobain/Pop2013HommeFemme20plus.csv with DELIMITER ',' CSV HEADER