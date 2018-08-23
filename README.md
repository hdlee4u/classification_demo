# Modeling Workflow Example - Greenplum Database

## classification_demo
Classification of Credit Card Approval

## Reference : [Jarrod Vawdrey's GitHub](https://github.com/jvawdrey/gpdb5-demo/blob/master/docker-jupyter/notebooks/Modeling%20Workflow%20Example%20-%20Greenplum%20Database.ipynb)

## Data Set Information:
This file concerns credit card applications. All attribute names and values have been changed to meaningless symbols to protect confidentiality of the data.

This dataset is interesting because there is a good mix of attributes -- continuous, nominal with small numbers of values, and nominal with larger numbers of values. There are also a few missing values.

### Attribute Information:
A1: b, a. <\n>
A2: continuous. 
A3: continuous. 
A4: u, y, l, t. 
A5: g, p, gg. 
A6: c, d, cc, i, j, k, m, r, q, w, x, e, aa, ff. 
A7: v, h, bb, j, n, z, dd, ff, o. 
A8: continuous. 
A9: t, f. 
A10: t, f. 
A11: continuous. 
A12: t, f. 
A13: g, p, s. 
A14: continuous. 
A15: continuous. 
A16: +,- (class attribute) 


## Docker image of Greenplum Database on CentOS with Pivotal Data Science Tool Kits, such as MADlib, PL/R and PL/Python
https://hub.docker.com/r/hdlee2u/gpdb-analytics/

CentOS : release 7.4
Greenplum Database : ver 5.10.2
MADlib : ver 1.15
PL/R : 2.3.2
DataScienceR : 1.0.1
DataSciencePython : 1.1.1

### (1) Docker Image Pull
$ docker pull hdlee2u/gpdb-analytics
$ docker images

### (2) Docker Image Run(port 5432) -> Docker Container Creation
$ docker run -i -d -p 5432:5432 -p 28080:28080 --name gpdb-ds --hostname mdw hdlee2u/gpdb-analytics /usr/sbin/sshd -D
$ docker ps -a

### (3) To Start Greenplum Database and Use psql
$ docker exec -it gpdb-ds /bin/bash
[root@mdw /]# su - gpadmin
[gpadmin@mdw ~]$ gpstart -a
[gpadmin@mdw ~]$ psql
psql (8.3.23)
Type "help" for help.

gpadmin=# \dn
List of schemas
Name | Owner
--------------------+---------
gp_toolkit | gpadmin
information_schema | gpadmin
madlib | gpadmin
pg_aoseg | gpadmin
pg_bitmapindex | gpadmin
pg_catalog | gpadmin
pg_toast | gpadmin
public | gpadmin
(8 rows)

gpadmin=# \q

### (4) PGAdmin IV configuration for SQL query
Host : localhost
Port : 5432
Maintenance DB : gpadmin
Username : gpadmin
Password : pivotal
Group: Servers
Ternel port: 22

PGAdmin 4 download: https://www.pgadmin.org/download/

### (5) Docker Container Stop, Restart
$ docker stop gpdb-ds
$ docker start gpdb-ds
$ docker ps


### For more information on Greenplum Database
https://greenplum.org/
https://network.pivotal.io/
http://rfriend.tistory.com/377

### For more information on Apache MADlib (Big Data Machine Learning in SQL)
http://madlib.apache.org/

### For more information on Greenplum PL/R Language Extension
https://gpdb.docs.pivotal.io/590/ref_guide/extensions/pl_r.html

### For more information on Greenplum PL/Python Language Extension
https://gpdb.docs.pivotal.io/590/ref_guide/extensions/pl_python.html

### For more information on Docker Install, GPDB start, PGAdmin setup, Jupyter Notebook setup
http://rfriend.tistory.com/379
