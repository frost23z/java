# JDBC (Java Database Connectivity)

## Overview
JDBC is an API in Java that allows interaction with databases. It provides methods to query and update data in a database.

???+ info "Key Features"
    - **Database Independence**: JDBC allows Java applications to interact with any database that has a JDBC driver.
    - **Support for Multiple Databases**: It supports various databases like MySQL, PostgreSQL, Oracle, etc.
    - **Connection Pooling**: Improves performance by reusing connections.

## Key Components

???+ info "Components"
    - **JDBC Driver**: Implements the JDBC API for a specific database.
    - **DriverManager**: Manages database drivers and establishes connections.
    - **Connection**: Represents a connection to a database.
    - **Statement**: Executes SQL queries.
    - **PreparedStatement**: Precompiled SQL statement for parameterized queries.
    - **CallableStatement**: Executes stored procedures.
    - **ResultSet**: Represents query results, allowing iteration over data.
    - **SQLException**: Handles database access errors.
    - **Batch Processing**: Executes multiple SQL statements in a single batch.
    - **Transaction Management**: Groups multiple operations into a single unit of work.
    - **RowSet**: Flexible wrapper around ResultSet.
    - **DataSource**: Alternative to DriverManager, often used in enterprise applications for connection pooling and distributed transactions.

## Steps to Connect to a Database

???+ info "Connection Steps"
    1. **Load the JDBC Driver**:

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
    // Close the ResultSet
    resultSet.close();
    // Close the Statement
    statement.close();
    // Close the Connection
    connection.close();
    ```

## Best Practices

???+ tip "Best Practices"
    - Use `try-with-resources` to automatically close resources.
    - Use `PreparedStatement` to prevent SQL injection.
    - Handle exceptions properly to avoid crashes.
    - Use connection pooling for better performance.
    - Avoid `Statement` for dynamic queries; prefer `PreparedStatement`.
    - Always close `Connection`, `Statement`, and `ResultSet` objects.

## Additional Concepts

### Transaction Management
- **Start a Transaction**: Use `connection.setAutoCommit(false);`.
- **Commit Changes**: Use `connection.commit();`.
- **Rollback Changes**: Use `connection.rollback();`.

### Error Handling
- Catch `SQLException` for database-related errors.
- Use `getMessage()`, `getSQLState()`, and `getErrorCode()` for debugging.

### Connection Pooling
- Use libraries like **HikariCP** or **Apache DBCP** for efficient connection management.

### Batch Processing
- Use `addBatch()` and `executeBatch()` for executing multiple queries efficiently.

### Metadata Handling
- Use `DatabaseMetaData` and `ResultSetMetaData` to retrieve database and result set information.

## Example Code

???+ example "JDBC Example"

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
            } catch (Exception e) {
                e.printStackTrace();
            } finally {
                try {
                    if (resultSet != null) resultSet.close();
                    if (statement != null) statement.close();
                    if (connection != null) connection.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
    ```