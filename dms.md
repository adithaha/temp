#dms here

```
sudo apt-get update
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql@11-main
sudo systemctl status postgresql@11-main
```

```
sudo -u postgres psql
\l
CREATE USER adit WITH PASSWORD 'adit';

CREATE DATABASE dsemployee
  WITH OWNER = adit
       ENCODING = 'UTF8'
       TABLESPACE = pg_default
       CONNECTION LIMIT = -1;

\c dsemployee;

CREATE TABLE employee
(
  id serial NOT NULL,
  address character varying(255),
  name character varying(255),
  CONSTRAINT employee_pkey PRIMARY KEY (id )
);

CREATE TABLE phone
(
  id serial NOT NULL,
  employee_id integer,
  phone character varying(255),
  type character varying(255),
  CONSTRAINT phone_pkey PRIMARY KEY (id ),
  CONSTRAINT fk_hbvecruwjtpc6u53ujlmjpvtw FOREIGN KEY (employee_id)
      REFERENCES employee (id) MATCH SIMPLE
      ON UPDATE NO ACTION ON DELETE NO ACTION
);

exit
```
```
sudo -u postgres psql -U adit -W -h localhost -d dsemployee

insert into employee (name,address)values ('adit','jakarta');
insert into employee (name,address)values ('adit2','jawa barat');

insert into phone (employee_id,phone,type)values (1,'081111111','hp');
insert into phone (employee_id,phone,type)values (1,'081111112','office');
insert into phone (employee_id,phone,type)values (2,'081211111','hp');
insert into phone (employee_id,phone,type)values (2,'081211112','home');

exit
```



