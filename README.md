# Security Tips

Below have some security tips.

## Ip by country

To list ip by country you have to access one of below sites:
 
 * https://db-ip.com
 * http://www.ip2nation.com/
 
### db-ip

Have a free list of IP by country. 
Accessing the https://db-ip.com/db/ link you can see "IP address to city". At the time I wrote this the database had 8,899,987 registers. The format are CSV and with below command you can import into postgresql:

<pre>
 copy locality("from","to",country, state, locality) FROM 'C:/temp\dbip-city-2016-11.csv' DELIMITER ',' CSV
</pre>

The database schema is:
<pre>

CREATE TABLE locality
(
  "from" character varying,
  "to" character varying,
  country character(2),
  state character varying,
  locality character varying,
  id serial NOT NULL,
  CONSTRAINT locality_pk PRIMARY KEY (id)
);
-- Index: locality_from_idx

CREATE INDEX locality_from_idx
  ON locality
  USING btree
  ("from" COLLATE pg_catalog."default");
</pre>

### ip2nation

Accessing the link http://www.ip2nation.com/ip2nation/Download, you can download the database schema that contains relationship between country and ip.
