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
    
  ##### dbcontext calss : 
    It is the primary class that is responsible for interacting with data as object. It often referred to as context.
     It is a wrapper around ObjectContext which is useful in all the development models: Code First, Model First and Database First.
  - Role: 
    - **Querying** : converts database values into entity objects and vice versa.
    - **Change Tracking** : It keeps track of changes occurred in the entities after it has been querying from the database.
    - **Persisting Data** : It also performs the Insert, update and delete operations to the database, based on the entity states.

###### Example 
```C#
public class ForumContext : DbContext
{ public DbSet<Category> Categories { get; set; }
public DbSet<Post> Posts { get; set; }
public DbSet<PostAnswer> PostAnswer { get; set; }
public DbSet<Tag> Tags { get; set; }
}
```
###### Methods Of DBContext : 
|Entry|Entry\<TEntity\>|Set(Type)|Set\<TEntity\>()|SaveChanges()|
|---|---|---|---|---|

###### Methods Of DBSet : 
|Add|Attach(Entity)|Create|Find(int)|Include|Remove|SqlQuery|
|---|---|---|---|---|---|---|

    
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

### EDM  

 - EDM Structure : 
    -  **EntityContainer** : EntityContainer EntityContainer is a wrapper for EntitySets and AssociationSets . It is an entry point for querying the model.
    -  **EntitySet** : Container for EntityType (like the db table)
    -  **EntityType** : datatype in the model
    -  **AssociationSet** : Defines the relation between each entityset
#### Quering with EDM
- LinQ to Entity 
   - LinQ Method 
   ```C#
   //Student is a model 
   using( var context = new SchoolDBStudents() ) {
   
    var query = context.Students.Where(s=>s.StudentName ==  "Bill").FirstOrDefault<Student>();
   }
  
   
   ```
   - LinQ Query
    ```C#
   
   using( var context = new SchoolDBStudents() ) {
   
    var query = from st in context.Students
                where st.StudentName = "Bill"
                select st;
    var student = query.FirstOrDefault<Student>();
   }
  
   
   ``` 
    -Projection
    
|First/FirstOrDefault|Single/SingleOrDefault|ToList|GroupBy|OrderBy|
|---|---|---|---|---|
|Returns the first row from the query result <br/>The difference = First() will throw an exception and FirstOrDefault () returns default value (null) if there is no result data|when we are sure that the result would contain only one element <br/> Single or SingleOrDefault will throw  anexception, if the result contains more than one element.|Converts the result to a list|Groups the result by a creteria|Sort the result by a criteria|
       
- Entity SQL : It returns ObjectQuery instead of Iqueryable
   ```C#
   //You need ObjectContext to create a query using Entity SQL.
     string command = " select VALUE st from SchoolDBEntities.Students " +
                        "AS st WHERE st.StudentName ==  'Bill'";
   
   var obj = (ctx as IObjectContextAdapter).ObjectContext;
   
   ObjectQuery<Student> student = obj.CreateQuery<Student>(command);
   }
  
   
   ```
- Native SQL
    ```C#
   
   using( var ctx = new SchoolDBEntities() ) {
   
    var student = ctx.Students.SqlQuery("Select * from Students where StudentId=@id", new SqlParameter('@id',1)).FirstOrDefault();
   }
  
   
   ``` 
   
  CRUD Operations
  
  
