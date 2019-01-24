1. ###### To import tables from Athena in Redshift
```sql
create external schema schema_name from data catalog 
database 'glue_db' 
iam_role 'arn:aws:iam::account_id:role/myRedshiftRole' 
region 'region';
```
Replace schema_name, glue_db, account_id,myRedshiftRole, region with your values

2. ###### To delete schema 
```sql
drop schema schema_name
```
Replace schema_name with your value
3. To get diskstyle of table
```sql
select "schema", "table", diststyle from SVV_TABLE_INFO
where "table" like 'dist%';
```
Replace 'dist%' with your table prefix

4. ###### To determine how many 1 MB blocks of disk space are used for each table
```sql
select stv_tbl_perm.name as table, count(*) as mb
from stv_blocklist, stv_tbl_perm
where stv_blocklist.tbl = stv_tbl_perm.id
and stv_blocklist.slice = stv_tbl_perm.slice
and stv_tbl_perm.name in ('payment','lineorder')
group by stv_tbl_perm.name
order by 1 asc;
```
5. ###### To find the number of 1 MB blocks each column uses for first 17 columns
```sql
select col, max(blocknum)
from stv_blocklist b, stv_tbl_perm p
where (b.tbl=p.id) and name ='lineorder'
and col < 17
group by name, col
order by col;
```

6. ###### To get all temp tables
```sql
select distinct(name) from stv_tbl_perm where temp = 1;
```
