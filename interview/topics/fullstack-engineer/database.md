# Fullstack Engineer - Database Questions

**1. What is the difference between a relational database and a NoSQL database?**

- **Relational Database:** Structured, uses tables with rows/columns, enforces schema (e.g., MySQL, PostgreSQL). Relies on SQL and relationships (foreign keys).
- **NoSQL Database:** Flexible, schema-less, supports various data models (e.g., key-value, document, graph) like MongoDB, Redis. Scales horizontally, suits unstructured data.

**2. How do you optimize a slow-performing SQL query?**

- Analyze: Run EXPLAIN or EXPLAIN ANALYZE to see the query execution plan and identify bottlenecks (e.g., full table scans).
- Indexes: Add indexes on columns used in WHERE, JOIN, or ORDER BY clauses to speed up lookups.
- Selectivity: Avoid SELECT \*; specify only needed columns to reduce data transfer.
- Joins: Ensure proper indexing on join keys and use INNER JOIN over LEFT JOIN when possible.
- Filters: Apply WHERE clauses early and use LIMIT to reduce row processing.
- Caching: Cache frequent queries (e.g., with Redis) or use materialized views for complex aggregations.
- Rewrite: Break complex queries into simpler subqueries or CTEs if the optimizer struggles.

**3. What are indexes in a database, and how do they impact performance?**

- Indexes:
  - Data structures (e.g., B-trees, hash tables) that store a subset of a table’s data (e.g., a column) for faster retrieval.
  - Created with CREATE INDEX on columns like user_id or email.
- Impact: Faster reads/queries; slower writes (inserts/updates) due to index maintenance. Over-indexing wastes space and slows performance.
  - Pros: Speeds up SELECT, WHERE, JOIN, and ORDER BY by avoiding full table scans (e.g., O(log n) vs. O(n)).
  - Cons: Slows down INSERT, UPDATE, and DELETE because the index must be updated too. Uses extra disk space.

**4. Explain the concept of database normalization and when you might denormalize.**

- Normalization:
  - Process of structuring data to eliminate redundancy and anomalies (insertion, update, deletion).
  - Follows rules like 1NF (atomic values), 2NF (no partial dependency), 3NF (no transitive dependency).
  - Example: Split orders with customer_name into orders and customers tables linked by customer_id.
- Denormalization:
  - Intentionally adding redundancy to improve read performance (e.g., fewer joins, faster queries).
  - Use cases: Read-heavy applications, reporting, caching, or when normalization slows down queries.

**5. How would you design a database schema for a social media application?**

- Tables:

  - users: id (PK), username, email, password_hash, created_at
  - posts: id (PK), user_id (FK), content, timestamp, likes_count
  - comments: id (PK), post_id (FK), user_id (FK), content, timestamp
  - follows: follower_id (FK), followee_id (FK), created_at (junction table for followers)
  - likes: user_id (FK), post_id (FK), timestamp (junction table for likes)

- Indexes:

  - user_id in posts, comments for user-specific queries.
  - post_id in comments, likes for post-related queries.

Considerations: Use sharding by user_id for scale; add timestamp indexes for timeline sorting.

**6. What is ACID compliance, and why is it important for transactions?**

- ACID: Atomicity (all or nothing), Consistency (valid state), Isolation (independent transactions), Durability (committed data persists).
  Importance: Ensures reliable, predictable transactions (e.g., money transfers), preventing data corruption or partial updates.

**7. How do you handle database migrations in a team environment?**

- Tools: Use migration frameworks like `Flyway`, `Liquibase`, or `Rails` migrations.
- Version Control: Store migration scripts (e.g., 20250327_add_column.sql) in Git with clear naming.
- Scripts: Write up (apply changes) and down (rollback) for each migration.
- Process:
  - Test locally, then push to staging/production.
  - Lock the DB during migration to avoid conflicts.
  - Use CI/CD pipelines for automation.
- Team Coordination: Document changes, communicate schema updates, and review scripts.

**8. What are the trade-offs between using MongoDB and PostgreSQL?**

- MongoDB (NoSQL):

  - Pros: Flexible schema (JSON-like documents), easy horizontal scaling, fast for unstructured data.
  - Cons: Weak ACID (eventual consistency), limited joins, harder complex queries.
  - Use Case: Rapid prototyping, big data (e.g., logs, content management).

- PostgreSQL (Relational):

  - Pros: Full ACID, rich SQL (e.g., CTEs, window functions), strong data integrity.
  - Cons: Vertical scaling, rigid schema, slower for unstructured data.
  - Use Case: Financial systems, structured data apps.

**9. How would you implement a many-to-many relationship in a relational database?**

Steps:

    Create two main tables (e.g., students: student_id, name and courses: course_id, title).
    Add a junction table (e.g., enrollments: student_id (FK), course_id (FK), enrollment_date).
    Set student_id and course_id as a composite primary key or unique index.

Example SQL:

    ```SQL
    CREATE TABLE students (student_id INT PRIMARY KEY, name VARCHAR(50));
    CREATE TABLE courses (course_id INT PRIMARY KEY, title VARCHAR(50));
    CREATE TABLE enrollments (
        student_id INT,
        course_id INT,
        enrollment_date DATE,
        FOREIGN KEY (student_id) REFERENCES students(student_id),
        FOREIGN KEY (course_id) REFERENCES courses(course_id),
        PRIMARY KEY (student_id, course_id)
    );
    ```

Purpose: Links students to multiple courses and vice versa efficiently.

**10. What is sharding, and when would you use it in a database?**

Sharding:

    Divides a database into smaller, independent pieces (shards) based on a shard key (e.g., user_id % 4 for 4 shards).
    Each shard lives on a separate server, holding a subset of data.

When to Use:

    When a single server can’t handle data size, write load, or query volume (e.g., millions of users in a social app).
    Example: Shard by geographic region for a global e-commerce site.

Trade-offs:

    Pros: Scales horizontally, distributes load.
    Cons: Complex queries across shards, harder maintenance.

## Extra Questions

**1. All the joins in SQL:**

SQL joins combine rows from two or more tables based on a related column.

- **INNER JOIN:** Returns rows when there is a match in both tables.

  - Definition: Returns only the rows where there’s a match in both tables.
  - Syntax: SELECT \* FROM table1 INNER JOIN table2 ON table1.id = table2.id;
  - Example:
    - users (id, name) and orders (order_id, user_id):
    - SELECT name, order_id FROM users INNER JOIN orders ON users.id = orders.user_id;
    - Result: Only users with orders.
  - Use Case: When you need matching records only.

- **LEFT JOIN (or LEFT OUTER JOIN):** Returns all rows from the left table and matched rows from the right table.

Definition: Returns all rows from the left table and matching rows from the right table. Non-matching rows from the right get NULL.
Syntax: SELECT \* FROM table1 LEFT JOIN table2 ON table1.id = table2.id;
Example:

    All users, even those without orders:
    SELECT name, order_id FROM users LEFT JOIN orders ON users.id = orders.user_id;
    Result: All users; order_id is NULL for users with no orders.

Use Case: Include all records from the left table regardless of matches.

- **RIGHT JOIN (or RIGHT OUTER JOIN):** Returns all rows from the right table and matched rows from the left table.

Definition: Returns all rows from the right table and matching rows from the left table. Non-matching rows from the left get NULL.
Syntax: SELECT \* FROM table1 RIGHT JOIN table2 ON table1.id = table2.id;
Example:

    All orders, even if no user exists:
    SELECT name, order_id FROM users RIGHT JOIN orders ON users.id = orders.user_id;
    Result: All orders; name is NULL for orders without users.

Use Case: Include all records from the right table.

- **FULL JOIN (or FULL OUTER JOIN):** Returns rows when there is a match in one of the tables.

Definition: Returns all rows from both tables, with NULL in places where there’s no match.
Syntax: SELECT \* FROM table1 FULL JOIN table2 ON table1.id = table2.id;
Example:

    All users and orders, matched or not:
    SELECT name, order_id FROM users FULL JOIN orders ON users.id = orders.user_id;
    Result: All users and orders; NULL for unmatched rows.

Use Case: When you need all data from both tables.

- **CROSS JOIN:** Returns the Cartesian product of the two tables (all possible combinations).

Definition: Produces a Cartesian product—every row from the first table paired with every row from the second table (no condition needed).
Syntax: SELECT \* FROM table1 CROSS JOIN table2;
Example:

    colors (red, blue) and sizes (S, M):
    SELECT color, size FROM colors CROSS JOIN sizes;
    Result: red-S, red-M, blue-S, blue-M.

Use Case: Generate combinations (e.g., all possible product variants).

- **SELF JOIN:** Joins a table with itself (e.g., for hierarchical data like employees and managers).

Definition: A table joined with itself, typically using aliases, to compare rows within the same table.
Syntax: SELECT a.col, b.col FROM table a, table b WHERE a.id = b.parent_id;
Example:

    employees (id, name, manager_id):
    SELECT e1.name, e2.name FROM employees e1 INNER JOIN employees e2 ON e1.manager_id = e2.id;
    Result: Employee and their manager’s name.

Use Case: Hierarchical data (e.g., org charts).
