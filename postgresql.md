-------------------------  DATA TYPES  ------------------------
https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-data-types/

boolean
character ( char, varchar, text )
numeric ( smallint, integer, bigint, decimal, numeric, real, double precision, smallserial, serial, bigserial )
temporal ( date, time, timestamp, interval )
uuid
array
json
hstore
-------------------------  SEQUENCE  ------------------------
https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-sequences/

CREATE SEQUENCE [ IF NOT EXISTS ] sequence_name
    [ AS { SMALLINT | INT | BIGINT } ]
    [ INCREMENT [ BY ] increment ]
    [ MINVALUE minvalue | NO MINVALUE ] 
    [ MAXVALUE maxvalue | NO MAXVALUE ]
    [ START [ WITH ] start ] 
    [ CACHE cache ] 
    [ [ NO ] CYCLE ]
    [ OWNED BY { table_name.column_name | NONE } ]
    
    nextval('sequence_name');
    curval('sequence_name');
    
-------------------------  CONSTRAINT CHECK  ------------------------
https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-check-constraint/
    
CREATE TABLE prices_list (
	  id          serial PRIMARY KEY,
	  product_id  INT NOT NULL,
	  price       NUMERIC NOT NULL,
    discount    NUMERIC NOT NULL,
    exists      VARCHAR(1) NOT NULL,
    valid_from  DATE NOT NULL,
	  valid_to    DATE NOT NULL
    comment on exists is "(Y)es, (N)o, (U)nknown"
);
ALTER TABLE prices_list 
ADD CONSTRAINT price_discount_check 
CHECK (
	price > 0
	AND discount >= 0
	AND price > discount
  AND exists in ('Y', 'N')
  OR exists = 'U'
);

-------------------------  CONSTRAINT UNIQUE  ------------------------
https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-unique-constraint/

CREATE TABLE person (
	id            SERIAL PRIMARY KEY,
	first_name    VARCHAR (50),
	last_name     VARCHAR (50),
	email         VARCHAR (50) UNIQUE,
  phone_number  VARCHAR (13),
  UNIQUE(phone_number)
);
