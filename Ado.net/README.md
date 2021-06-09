# ADO.NET

**ADO** Stands for : **A**ctiveX **D**ata **O**bject

    It is a module of .Net Framework which is used to establish connection between application and data sources.
  
  ADO.NET has two main components that are used for accessing and manipulating data are:
  
  |Data provider | DataSet|
  | --- | --- |
  |It is used to connect to the database, execute commands and retrieve the record. |It is a collection of data tables that contain the data. It is used to fetch data without interacting with a Data Source that's why, it also known as disconnected data access method.|
    
## Connected Mode 


``SqlConnection`` : It is used to establish a connection to a specific data source


 ``SqlCommand`` : It is used to execute queries to perform database operations
 

 ``SqlDataReader``: It is used to read data from data source
 



|``SqlDataAdapter``: It works as a bridge between a DataSet and a data source to retrieve data.It can be used to fill the DataSet and update the data source|
|---|

## Disconnected Mode


 ``DataSet``: It is used to initialize a new instance of the DataSet class
 
 

## Architecture
<img src="https://www.researchgate.net/profile/Syed-Rahman-5/publication/228997568/figure/fig1/AS:393865853980679@1470916345540/ADONET-Architecture.png" alt="archi" width="480" height="300"/>


## Stored Procedures 

After adding stored procedure in the sql server our SqlCommand becomes: 

```C#
                SqlCommand cmd = new SqlCommand()
                {
                    CommandText = "<stored procedure namme>",
                    Connection = connection_var,
                    CommandType = CommandType.StoredProcedure
                  
                };
                
                //with parameters : 
                
                  SqlParameter param = new SqlParameter
                {
                    ParameterName = "@paramname", 
                    SqlDbType = SqlDbType.<type>, 
                    Value = "<VALUE>",
                    Direction = ParameterDirection.Input (or output)
                };
                
                cmd.Parameters.Add(param);
```
# Entity Framework 

      Entity Framework (EF) is an open source object-relational mapping (ORM) framework for Ado.NET
      
 |<img src="https://static.javatpoint.com/tutorial/entity-framework/images/entity-framework-architecture.png" alt="archi" />|**EDM (Entity Data Model)**: It is a set of concepts that describe the structure of data Conceptual model<br/> Mapping <br/>  Storage model.<br/>**LINQ** to Entities: is a query language used to write queries against the object model. It returns entities, which are defined in the conceptual model. <br/>**Entity SQL**:  is another query language just like LINQ to Entities.|
|---|---|
      
 ## Workflow: 
 
 |ModelFirst|DatabaseFirst| CodeFirst |
 | --- | --- | --- |
 |Working on a visual diagram using the EF Designer and letting the Entity Framework create/update the rest accordingly|building the Database and letting Entity Framework create/update the rest accordingly|writing the Data Model entity classes and let Entity Framework generate the Database accordingly|



###  Code First : 

 #### 1- Create Models 
  - Annotions : ... 
  - Sql relation : 
  
|One To One |One to Many |Many to Many | Many to One |
|---|---|---|---|
|||||
 
####  2- Create a DBcontext for your database 
    ! you should first create a database in the sql server  than add the connectionString to your dbcontext class
    
   dbcontext calss : ...
    
#### 3- Migrations 
  In your package manager tap those cmd: 
  <br />
      `` > enable- migrations``
   <br />
   ``> add-migration <migration name>``
   
     this will create a migration for you that has 2 methods : 
  
        - up() contains all the sql queries of the changes that you made 
        - down() : contains the opposite of the up() method 
    
   
 
 
``> update-database ``
<br />
This helps you add all the updates to your server 


### Operation on database 

- EDM  ..
- LinQ to Entity ..
