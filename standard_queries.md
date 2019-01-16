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
