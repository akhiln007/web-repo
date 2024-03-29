---
layout: post

title: Snowflake - Time Dimension
---



{{ page.title }}

================

create or replace sequence dim_time_time_key_seq start = 1 increment = 1;

create or replace TABLE EUS_SO_PUB.SO_MART.DIM_TIME (

	TIME_KEY NUMBER(38,0),
	
        D_TIME TIME(9) NOT NULL,
	
	D_TIME_OF_DAY VARCHAR(2),
	
	D_HOUR NUMBER(38,0),
	
	D_MINUTE NUMBER(38,0),
	
	D_TIME_30 TIME(9),
	
	D_TIME_60 TIME(9),
	
	ETL_IS_DELETED_IND BOOLEAN NOT NULL DEFAULT FALSE,
	
	ETL_IS_SKELETON_IND BOOLEAN NOT NULL DEFAULT FALSE,
	
	ETL_DATA_SOURCE_CODE VARCHAR(16777216) NOT NULL DEFAULT 'missing',
	
	ETL_MD5_CHECKSUM VARCHAR(16777216) NOT NULL DEFAULT 'missing',
	
	ETL_LAST_UPDATED_DATE TIMESTAMP_NTZ(9) NOT NULL
	
) AS   

  WITH gen_data AS 
  
  (
  
select

  dateadd(minute, '-' || seq4(), current_date()::date) as time_value
  
from

  table (generator(rowcount => 1440))      
  
) 

  SELECT
  
        dim_time_time_key_seq.NEXTVAL                                                                       AS time_key
	
       ,to_time(time_value)                                                                                 AS d_time
       
       ,CASE 
       
         WHEN substring(time_value,12,2)::int >= 12
	 
         THEN 'PM' ELSE 'AM'
	 
       END                                                                                                  AS d_time_of_day
       
       ,hour(time_value)                                                                                    AS d_hour
       
       ,minute(time_value)                                                                                  AS d_minute
       
       ,CASE 
       
         WHEN substring(time_value,15,2)::int >= 30
	 
         THEN ( substring(time_value,12,2)||':'||'30' )::time
	 
         ELSE ( substring(time_value,12,2)||':'||'00' )::time
	 
       END                                                                                                  AS d_time_30
       
       ,(substring(time_value,12,2)||':'||'00')::time                                                       AS d_time_60
       
       ,false                                                                                               AS etl_is_deleted_ind
       
       ,false                                                                                               AS etl_is_skeleton_ind
       
       ,'dim_time_insert_proc'                                                                              AS etl_data_source_code
       
       ,''                                                                                                  AS etl_md5_checksum
       
       ,CURRENT_DATE                                                                                        AS etl_last_updated_date
       
  FROM gen_data;
