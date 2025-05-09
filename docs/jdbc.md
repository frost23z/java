# JDBC (Java Database Connectivity)

## Overview
JDBC is an API in Java that allows interaction with databases. It provides methods to query and update data in a database.

## Key Components
1. **DriverManager**: Manages a list of database drivers.
2. **Connection**: Represents a connection to a database.
3. **Statement**: Used to execute SQL queries.
4. **ResultSet**: Represents the result of a query.
5. **PreparedStatement**: A precompiled SQL statement for parameterized queries.
6. **CallableStatement**: Used to execute stored procedures.

## Steps to Connect to a Database

1. **Load the Driver**:
   ```java
   Class.forName("com.mysql.cj.jdbc.Driver");
   ```
2. **Establish a Connection**:
   ```java
   Connection connection = DriverManager.getConnection(
       "jdbc:mysql://localhost:3306/dbname", "username", "password");
   ```
3. **Create a Statement**:
   ```java
   Statement statement = connection.createStatement();
   ```
4. **Execute a Query**:
   ```java
   ResultSet resultSet = statement.executeQuery("SELECT * FROM table_name");
   ```
5. **Process the Results**:
   ```java
   while (resultSet.next()) {
       System.out.println(resultSet.getString("column_name"));
   }
   ```
6. **Close the Connection**:
   ```java
   connection.close();
   ```

## Best Practices
- Always close `Connection`, `Statement`, and `ResultSet` objects to free resources.
- Use `PreparedStatement` to prevent SQL injection.
- Use connection pooling for better performance.

## Example Code
```java
import java.sql.*;

public class JDBCDemo {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/dbname";
        String user = "username";
        String password = "password";

        try {
            // Load the driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // Establish a connection
            Connection connection = DriverManager.getConnection(url, user, password);

            // Create a statement
            Statement statement = connection.createStatement();

            // Execute a query
            ResultSet resultSet = statement.executeQuery("SELECT * FROM table_name");

            // Process the results
            while (resultSet.next()) {
                System.out.println(resultSet.getString("column_name"));
            }

            // Close the connection
            connection.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```