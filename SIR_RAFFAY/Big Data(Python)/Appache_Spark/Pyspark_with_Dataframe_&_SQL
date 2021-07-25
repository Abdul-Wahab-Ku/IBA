#Assignment No.04

# File location and type
file_location = "/FileStore/tables/employee.csv"
file_type = "csv"

# CSV options
infer_schema = "true"
first_row_is_header = "true"
delimiter = ","

# The applied options are for CSV files. For other file types, these will be ignored.
df = spark.read.format(file_type) \
  .option("inferSchema", infer_schema) \
  .option("header", first_row_is_header) \
  .option("sep", delimiter) \
  .load(file_location)

display(df)

df.createOrReplaceTempView("Employee")

%sql
SELECT  Department_Name, Count(Gender) as Total_Male_Female,
count(case when gender='M' THEN 1  END) as Male ,
count(case when gender='F' THEN 1  END) as Female
FROM Employee 
Group By Department_Name;

SELECT   Postal as Most_Repeated_Postal_Code ,  count(Postal) as Counter
FROM employee
Group by Postal
ORDER BY count(Postal) DESC
limit 3 

SELECT   DEPARTMENT_NAME as NAME_OF_DEPART,   TITLE as PROFESSION   
FROM employee
Group by DEPARTMENT_NAME, TITLE
Order BY  DEPARTMENT_NAME Desc

from pyspark.sql.functions import desc, col
df2 = df.groupBy('DEPARTMENT_NAME', 'Gender').count().sort(desc("DEPARTMENT_NAME"))            
display(df2)
df2 = df.groupBy('Department_name','Title').max().sort(desc("Department_name")).withColumnRenamed("Title", "Profession")\
.withColumnRenamed("Department_name", "Department")
display(df2)
df2 = df.groupBy('Postal').count().sort(desc('count')).withColumnRenamed('Postal', "Most Repeated Postal Cod")\
.withColumnRenamed('count', "Counter ").take(3)
display(df2)


