# Exercise: Design Pattern Implementation Challenge

## Selected Pattern
**Factory Pattern (Python)**


# Step 1: Analyze the Code for Pattern Opportunities
The original `DatabaseConnection` class uses conditional statements inside the `connect()` method to determine how to connect to different database types.

### Problems Identified

- Large `if-elif-else` block.
- Violates the **Open/Closed Principle** because adding a new database requires modifying existing code.
- Difficult to maintain as more database types are introduced.
- Object creation and connection logic are tightly coupled.

This makes the code a good candidate for the **Factory Pattern**.


# Step 2: AI Prompt Used
> Analyze this Python code for design pattern opportunities. If appropriate, refactor it using the Factory Pattern while preserving its original functionality. Create separate classes for each database type and use a factory class to instantiate the correct object.


# Step 3: Refactored Implementation

```python
from abc import ABC, abstractmethod


# Abstract Base Class
class DatabaseConnection(ABC):

    def __init__(
        self,
        host,
        port,
        username,
        password,
        database,
        use_ssl=False,
        connection_timeout=30,
        retry_attempts=3,
        pool_size=5,
        charset="utf8",
    ):
        self.host = host
        self.port = port
        self.username = username
        self.password = password
        self.database = database
        self.use_ssl = use_ssl
        self.connection_timeout = connection_timeout
        self.retry_attempts = retry_attempts
        self.pool_size = pool_size
        self.charset = charset

    @abstractmethod
    def connect(self):
        pass


class MySQLConnection(DatabaseConnection):

    def connect(self):
        connection_string = (
            f"mysql://{self.username}:{self.password}"
            f"@{self.host}:{self.port}/{self.database}"
        )

        connection_string += f"?charset={self.charset}"
        connection_string += (
            f"&connectionTimeout={self.connection_timeout}"
        )

        if self.use_ssl:
            connection_string += "&useSSL=true"

        print("Connecting to MySQL...")
        print(connection_string)


class PostgreSQLConnection(DatabaseConnection):

    def connect(self):
        connection_string = (
            f"postgresql://{self.username}:{self.password}"
            f"@{self.host}:{self.port}/{self.database}"
        )

        if self.use_ssl:
            connection_string += "?sslmode=require"

        print("Connecting to PostgreSQL...")
        print(connection_string)


class MongoDBConnection(DatabaseConnection):

    def connect(self):
        connection_string = (
            f"mongodb://{self.username}:{self.password}"
            f"@{self.host}:{self.port}/{self.database}"
        )

        connection_string += (
            f"?retryAttempts={self.retry_attempts}"
        )

        connection_string += (
            f"&poolSize={self.pool_size}"
        )

        if self.use_ssl:
            connection_string += "&ssl=true"

        print("Connecting to MongoDB...")
        print(connection_string)


class RedisConnection(DatabaseConnection):

    def connect(self):
        print(
            f"Redis Connection: {self.host}:{self.port}/{self.database}"
        )


class DatabaseFactory:

    @staticmethod
    def create_connection(db_type, **kwargs):

        if db_type == "mysql":
            return MySQLConnection(**kwargs)

        elif db_type == "postgresql":
            return PostgreSQLConnection(**kwargs)

        elif db_type == "mongodb":
            return MongoDBConnection(**kwargs)

        elif db_type == "redis":
            return RedisConnection(**kwargs)

        else:
            raise ValueError(
                f"Unsupported database type: {db_type}"
            )
```

---

# Example Usage

```python
mysql = DatabaseFactory.create_connection(
    "mysql",
    host="localhost",
    port=3306,
    username="db_user",
    password="password123",
    database="app_db",
    use_ssl=True,
)

mysql.connect()


mongodb = DatabaseFactory.create_connection(
    "mongodb",
    host="mongodb.example.com",
    port=27017,
    username="mongo_user",
    password="mongo123",
    database="analytics",
    pool_size=10,
    retry_attempts=5,
)

mongodb.connect()
```

# Step 4: Unit Tests

```python
import unittest


class TestDatabaseFactory(unittest.TestCase):

    def test_mysql_creation(self):
        db = DatabaseFactory.create_connection(
            "mysql",
            host="localhost",
            port=3306,
            username="user",
            password="pass",
            database="test",
        )

        self.assertIsInstance(db, MySQLConnection)

    def test_postgresql_creation(self):
        db = DatabaseFactory.create_connection(
            "postgresql",
            host="localhost",
            port=5432,
            username="user",
            password="pass",
            database="test",
        )

        self.assertIsInstance(db, PostgreSQLConnection)

    def test_mongodb_creation(self):
        db = DatabaseFactory.create_connection(
            "mongodb",
            host="localhost",
            port=27017,
            username="user",
            password="pass",
            database="test",
        )

        self.assertIsInstance(db, MongoDBConnection)

    def test_redis_creation(self):
        db = DatabaseFactory.create_connection(
            "redis",
            host="localhost",
            port=6379,
            username="",
            password="",
            database="0",
        )

        self.assertIsInstance(db, RedisConnection)

    def test_invalid_database(self):

        with self.assertRaises(ValueError):
            DatabaseFactory.create_connection(
                "oracle",
                host="localhost",
                port=1521,
                username="user",
                password="pass",
                database="test",
            )


if __name__ == "__main__":
    unittest.main()
```

# Test Results

| Test | Result |
|------|--------|
| Create MySQL Connection | Passed |
| Create PostgreSQL Connection | Passed |
| Create MongoDB Connection | Passed |
| Create Redis Connection | Passed |
| Invalid Database Type | Passed |

**Overall Result:** All tests passed successfully.


# Benefits of the Factory Pattern
The Factory Pattern provided several improvements:
- Removed the large conditional block from the connection logic.
- Each database now has its own dedicated class.
- Improved code organization.
- Easier to maintain and extend.
- Better adherence to the Single Responsibility Principle.
- Follows the Open/Closed Principle.


# Future Changes Made Easier
Using the Factory Pattern makes future development much simpler.

Examples include:
- Adding Oracle support.
- Adding SQL Server support.
- Supporting SQLite.
- Creating cloud database connectors.
- Modifying one database implementation without affecting others.

Only a new connection class and one factory entry would be required.



# Reflection Questions

## 1. How did implementing the pattern improve the code's maintainability?
The Factory Pattern separated object creation from object usage. Each database type is now responsible only for its own connection logic, making the code easier to read, maintain, and debug.

## 2. What future changes will be easier because of this pattern?
Future enhancements are much simpler because new database types can be added without modifying existing connection classes. This reduces the risk of introducing bugs into working code

## 3. Were there any unexpected challenges in implementing the pattern?
The main challenge was deciding which responsibilities belonged in the abstract base class and which belonged in the concrete subclasses. Once the common configuration was identified, the implementation became straightforward.


# Conclusion

The Factory Pattern successfully refactored the original implementation by separating object creation from business logic. The resulting design is cleaner, easier to extend, and more maintainable while preserving the original functionality.

**Final Status:** Factory Pattern implemented successfully and all unit tests pass.
