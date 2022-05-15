# Movie-Data-base-using-sqlite-and-eclipse

Here we have created a database, store our interesting movie names with the names of lead actor, actress, year of release and the director name. Once we have stored the details, then use any programming language of our choice to retrieve the details.

Pre-requisite:
1.Java
2.Eclipse
3.sqlite-jdbc connector

#Goals:

1).Connect to the SQLite database(or any Database you know):
Learn how to download SQLiteJDBC driver and connect to an existing SQLite database using JDBC.

2).Creating a new SQLite database – Learn how to create a new SQLite database from a Java (any language) program using SQLiteJDBC driver or related driver.

3).Creating a new table (Movies) using JDBC / Other Languages – before working with data, you need to create a table called Movies. Learn how to create a new table in an SQLite database from a Java (any language) program.

4).Inserting data into Movies table from a Java (any language) program

5).Querying data from Movies table with or without parameters – after having the movies data in the table, you need to query the movie details (name, actor, actress, director, year of release) using a SELECT statement. You will need to write a program to issue a simple SELECT statement to query all rows from the Movies table, as well as use a query with parameter like actor name to select movies based on the actor's name.

In order to work with the SQLite database, we should have an SQLite-driver as a library in the IDE.
Libraries/packages needed:
import java.sql.Connection; //needed for connection
import java.sql.DriverManager; // for establishing connection and loading
import java.sql.PreparedStatement; //this represents a precompiled SQL statement.
import java.sql.ResultSet; //representing a database result set, which is usually generated by executing a statement.
import java.sql.SQLException; //database access error or other errors represented using the getMessage().
import java.sql.Statement; //executing a SQL statement.

or we can just,
import java.sql.*; // here by which we can import all the modules needed.
Connect to SQLite Database
Use the following code to connect to SQLite database using Java programming language:
public class Movies {  
private Connection connect() {   
Connection conn=null;     
try        
{            
Class.forName("org.sqlite.JDBC");            conn=DriverManager.getConnection("jdbc:sqlite:movies.db");           conn.setAutoCommit(false);        
}        
catch(SQLException | ClassNotFoundException e)        {            System.err.println(e.getClass().getName()+":"+e.getMessage());           System.exit(0);        
}        
return conn; 
}
Create a table using java
Let's create a table named "Movies" having columns "ID"."NAME","ACTOR","ACTRESS","DIRECTOR" and "YEAROFRELEASE". Create a class name "CreateTable", having the following code:
public void createTable() 
{  
String sql= "CREATE TABLE MOVIES " +                
"(ID INT PRIMARY KEY     NOT NULL," +                
" NAME           TEXT    NOT NULL, " +                 
" ACTOR          TEXT     NOT NULL, " +                
" ACTRESS        TEXT     NOT NULL, " +                 
" DIRECTOR        TEXT     NOT NULL),"+                
" YEAROFRELEASE CHAR(4))";      
try     
{      
Connection conn=this.connect();      
Statement st=conn.createStatement();      
st.execute(sql);     
}     
catch (SQLException e) {      
System.out.println(e.getMessage());    
   }  
}
Insert Record in the table
After the creation of the table, use the following code to insert some records in the table and assign some variable to be as reference. Create a new class "insert", having the following code:
public void insert (int id,String name,String actor,String actress,String director,String year) 
{  
String info ="INSERT INTO MOVIES(ID, NAME,ACTOR,ACTRESS,DIRECTOR,YEAROFRELEASE) VALUES(?,?,?,?,?,?)";   
try {   
Connection conn =this.connect();      
PreparedStatement pst=conn.prepareStatement(info);            pst.setInt(1, id);            
pst.setString(2, name);            
pst.setString(3, actor);            
pst.setString(4, actress);            
pst.setString(5, name);            
pst.setString(6, year);            
pst.executeUpdate();  
}  
catch (SQLException e)  
{   
System.out.println(e.getMessage());  
  } 
}
Select Records
1). To select records from the table, use the following code. Create a new class "selectAll()", having the following data.
"Querying data from Movies table with or without parameters - after having the movies data in the table, you need to query the movie details (name, actor, actress, director, year of release) using a SELECT statement."
SQL query:
SELECT * FROM MOVIES;
Below is the code for the following,
public void selectAll()     
{         
try        
{            
Connection conn =this.connect();            
Statement st = conn.createStatement();            
ResultSet rs= st.executeQuery("SELECT * FROM MOVIES;");           while(rs.next())            
{                
int id=rs.getInt("ID");                
String name=rs.getString("NAME");                
String actor=rs.getString("ACTOR");                
String actress=rs.getString("ACTRESS");                
String year=rs.getString("YEAROFRELEASE");                
String director=rs.getString("DIRECTOR");
                                
System.out.println("MOVIE ID = "+id);            System.out.println("MOVIE NAME = "+name);           System.out.println("ACTOR NAME = "+actor);             System.out.println("ACTRESS NAME = "+actress);             System.out.println("DIRECTOR NAME = "+director);             System.out.println("YEAR OF RELEASE = "+year);             System.out.println();
            }            
rs.close();            
st.close();        
     }        
catch (SQLException e)        
  {            
System.out.println(e.getMessage());       
    }     
}
2. To select records from the table, use the following code. Create a new class "selectparam()", having the following data.
"You will need to write a program to issue a simple SELECT statement to query all rows from the Movies table, as well as use a query with parameter like actor name to select movies based on the actor's name."
here we have used the actor Yash name to show the details,
SQL query:
SELECT NAME FROM MOVIES WHERE ACTOR='YASH';
Below is the code for the following,
public void selectparam()     
{         
try        
{            
Connection conn =this.connect();            
Statement st = conn.createStatement();            
ResultSet rs= st.executeQuery("SELECT NAME FROM MOVIES WHERE ACTOR='YASH':");            
System.out.println("The movies in which Yash is a Actor: ");           while(rs.next())            
{                
String name=rs.getString("NAME");               System.out.println(name);            
}            
rs.close();            
st.close();        
}        
catch (SQLException e)        
{           
System.out.println(e.getMessage());        
}     
}
Insert Values into table:
After the creation of the table, use the following code to insert some value into table called "Movies". Create a new object for the class Movies, having the following code:
public static void main (String[] args) {  
Movies list =new Movies(); //creating an object of the class Movies        list.createTable();        list.insert(1,"SAAHO","PRABHAS","SHRADDHA","SUJEETH","2019");       list.insert(2,"URI","VICKY","YAMI","ADITYA","2019");       list.insert(3,"KGF2","YASH","SRINIDHI","PRASHANTH","2022");        list.insert(4,"SPIDER MAN NO WAY HOME","TOM HOLLAND","ZENDAYA","JOHN WATTS","2021");        
list.selectAll();        
list.selectparam(); 
  } 
}
Thanks for reading ………
For the whole code visit my GitHub account:
Movie-Data-base-using-sqlite-and-eclipse/Movies.java at master · HarishB-23/Movie-Data-base-using-sqlite-and-eclipse (github.com)
