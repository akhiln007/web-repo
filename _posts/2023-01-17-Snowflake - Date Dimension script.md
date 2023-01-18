---
layout: post

title: Snowflake - Date Dimension
---



{{ page.title }}

================

create or replace sequence dim_date_date_key_seq start = 1 increment = 1;

create or replace TABLE EUS_SO_PUB.SO_MART.DIM_DATE (

    DATE_KEY NUMBER(38,0),
    
	  REPORTING_DATE DATE NOT NULL,
  
	  DAY_NAME VARCHAR(100) NOT NULL,
    
    WEEK_NUMBER NUMBER(38,0) NOT NULL,
    
	  WEEK_NAME VARCHAR(100) NOT NULL,
    
    WEEK_BEGIN_DATE DATE NOT NULL,
    
    WEEK_END_DATE DATE NOT NULL,
    
    MONTH_NUMBER NUMBER(38,0) NOT NULL,
    
	  MONTH_NAME VARCHAR(100) NOT NULL,
    
	  MONTH_BEGIN_DATE DATE NOT NULL,
    
	  MONTH_END_DATE DATE NOT NULL,
    
	  QUARTER_NUMBER NUMBER(38,0) NOT NULL,
    
	  QUARTER_NAME VARCHAR(100) NOT NULL,
    
	  QUARTER_BEGIN_DATE DATE NOT NULL,
    
	  QUARTER_END_DATE DATE NOT NULL,
    
	  YEAR_NUMBER NUMBER(38,0) NOT NULL,
    
	  YEAR_BEGIN_DATE DATE NOT NULL,
    
	  YEAR_END_DATE DATE NOT NULL,
    
    DAY_OF_WEEK NUMBER(38,0) NOT NULL,
    
	  DAY_OF_MONTH NUMBER(38,0) NOT NULL,
    
	  DAY_OF_QUARTER NUMBER(38,0) NOT NULL,
    
	  DAY_OF_YEAR NUMBER(38,0) NOT NULL,
    
    WEEK_END_IND BOOLEAN NOT NULL,
    
    MONTH_END_IND BOOLEAN NOT NULL,
    
    YEAR_MONTH_NUMBER NUMBER(38,0) NOT NULL,
    
	  MONTH_YEAR_NAME VARCHAR(100) NOT NULL,
    
    ETL_IS_DELETED_IND BOOLEAN NOT NULL DEFAULT FALSE,
    
	  ETL_IS_SKELETON_IND BOOLEAN NOT NULL DEFAULT FALSE,
    
	  ETL_DATA_SOURCE_CODE VARCHAR(16777216) NOT NULL DEFAULT 'missing',
    
	  ETL_MD5_CHECKSUM VARCHAR(16777216) NOT NULL DEFAULT 'missing',
    
	  ETL_LAST_UPDATED_DATE TIMESTAMP_NTZ(9) NOT NULL
    
    )
    
AS

WITH gen_data AS

(

  select
  
  dateadd(day, '-' || seq4(), '2030-12-31'::date) as date_value
  
from

  table
  
    (generator(rowcount => 6095))
    
) 

SELECT

    dim_date_date_key_seq.NEXTVAL                                                               AS date_key
    
   ,date_value                                                                                  AS reporting_date
   
   ,DAYNAME(date_value)                                                                         AS day_name
   
   ,WEEK(date_value)                                                                            AS week_number
   
   ,'Week '|| WEEK(date_value)                                                                  AS week_name
   
   ,date_value - dayofweek(date_value)                                                          AS week_begin_date
   
   ,last_day(date_value, 'week')                                                                AS week_end_date
   
   ,month(date_value)                                                                           AS month_number   
   
   ,monthname(date_value)                                                                       AS month_name
   
   ,date_trunc('month',date_value)::DATE                                                        AS month_begin_date   
   
   ,last_day(date_value, 'month')                                                               AS month_end_date
   
   ,quarter(date_value)                                                                         AS quarter_number   
   
   ,'Q'||quarter(date_value)                                                                    AS quarter_name
   
   ,date_trunc('quarter',date_value)::DATE                                                      AS quarter_begin_date   
   
   ,last_day(date_value, 'quarter')                                                             AS quarter_end_date
   
   ,year(date_value)                                                                            AS year_number   
   
   ,date_trunc('year',date_value)::DATE                                                         AS year_begin_date   
   
   ,last_day(date_value, 'year')                                                                AS year_end_date
   
   ,dayofweek(date_value)                                                                       AS day_of_week
   
   ,dayofmonth(date_value)                                                                      AS day_of_month
   
   ,row_number() OVER
   
        ( PARTITION BY quarter_number
        
          ORDER BY date_value)                                                                   AS day_of_quarter--rework
          
   ,dayofyear(date_value)                                                                       AS day_of_year
   
   ,CASE WHEN DAYNAME(date_value) in('Sat','Sun') THEN True ELSE False END                      AS week_end_ind
   
   ,CASE WHEN
   
          date_value = (date_trunc('month', date_value) + INTERVAL '1 month' - INTERVAL '1 day')::date
          
           THEN True
           
           ELSE False
           
           END                                                                                   AS  month_end_ind
           
   ,to_char( date_value,'YYYYMM')::int                                                           AS  year_month_number
   
   ,trim(to_char( date_value , 'Mon')||chr(39)||to_char( date_value , 'YYYY')  )                   AS  month_year_name
   
   ,false                                                                                        AS etl_is_deleted_ind
   
   ,false                                                                                        AS etl_is_skeleton_ind
   
   ,'dim_date_insert_proc'                                                                       AS etl_data_source_code
   
   ,''                                                                                           AS etl_md5_checksum
   
   , CURRENT_DATE                                                                                AS etl_last_updated_date
   
 FROM gen_data;
