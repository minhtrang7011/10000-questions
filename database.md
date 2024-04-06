## What is "Data integrity"

Data integrity refers to the accuracy, consistency, and reliability of data stored in a database or information system. It ensures that data remains unchanged and reliable throughout its lifecycle, from creation to deletion. Data integrity is crucial for ensuring the quality and trustworthiness of data and is maintained through various mechanisms, including constraints, validations, and error detection and correction techniques.

Here are some key aspects of data integrity:

1. **Accuracy**: Data accuracy ensures that the data reflects the real-world entities or events it represents. It involves ensuring that data values are correct and free from errors or inconsistencies.

2. **Completeness**: Data completeness ensures that all required data is present and no essential information is missing. It involves ensuring that all necessary fields are populated with valid data.

3. **Consistency**: Data consistency ensures that data remains uniform and coherent across the database. It involves maintaining data relationships and dependencies, such as referential integrity between related tables.

4. **Validity**: Data validity ensures that data conforms to predefined rules or constraints. It involves enforcing data validation rules, such as data type constraints, range constraints, and format constraints.

5. **Reliability**: Data reliability ensures that data can be trusted and relied upon for decision-making and other purposes. It involves preventing data corruption, unauthorized access, and other threats to data integrity.

Maintaining data integrity is essential for ensuring the effectiveness and reliability of database systems. It is achieved through the implementation of various measures, including:

- **Constraints**: Such as primary key constraints, foreign key constraints, unique constraints, and check constraints, which enforce data integrity rules at the database level.
  
- **Transactions**: Using transactions to ensure the atomicity, consistency, isolation, and durability (ACID properties) of database operations, thereby preventing data corruption and ensuring data integrity.
  
- **Data validation**: Performing data validation checks at the application level to ensure that only valid data is entered into the database.
  
- **Backup and recovery**: Implementing backup and recovery mechanisms to protect against data loss or corruption and to restore data to a consistent state in case of failures or disasters.

Overall, data integrity is essential for maintaining the quality, reliability, and trustworthiness of data in databases and information systems. It is a fundamental aspect of data management and plays a critical role in supporting business operations, decision-making, and regulatory compliance.

## ACID properties

ACID is an acronym that stands for Atomicity, Consistency, Isolation, and Durability. It is a set of properties that ensures the reliability and integrity of transactions in database systems. These properties are fundamental for maintaining data integrity and ensuring that database transactions are processed reliably, even in the presence of failures.

Let's break down each component of ACID:

1. **Atomicity**:
   - Atomicity ensures that a transaction is treated as a single, indivisible unit of work. Either all of the operations within the transaction are successfully completed and the changes are committed to the database, or none of the operations are performed and the database remains unchanged. There is no partial execution of transactions. If any part of the transaction fails, the entire transaction is rolled back to its initial state.

2. **Consistency**:
   - Consistency ensures that the database remains in a consistent state before and after the transaction. It guarantees that the integrity constraints, data validation rules, and relationships defined in the database schema are preserved during transaction execution. In other words, the database transitions from one consistent state to another consistent state after each successful transaction.

3. **Isolation**:
   - Isolation ensures that the concurrent execution of multiple transactions does not interfere with each other. Each transaction is isolated from other transactions until it is completed and committed. Transactions should appear to execute serially, even if they are executed concurrently. Isolation prevents issues such as dirty reads, non-repeatable reads, and phantom reads.

4. **Durability**:
   - Durability guarantees that once a transaction is committed, its changes are permanently saved and will not be lost, even in the event of a system failure or crash. The committed changes are stored in non-volatile storage (such as disk) and remain intact even if the system crashes or power is lost. Durability ensures that the database can recover to a consistent state after a failure without losing committed data.

ACID properties are essential for ensuring the reliability, consistency, and integrity of database transactions. They provide a framework for designing and implementing robust database systems that can maintain data integrity and withstand various types of failures and concurrency issues. Transaction processing systems in relational databases typically adhere to the ACID properties to ensure data reliability and consistency.

## Dirty reads, non-repeatable reads, and phantom reads

Dirty reads, non-repeatable reads, and phantom reads are phenomena that can occur in a database system when multiple transactions are executed concurrently, and the isolation level of the transactions allows certain types of inconsistencies between them. These phenomena are related to the Isolation property of the ACID (Atomicity, Consistency, Isolation, Durability) properties.

1. **Dirty Reads**:
   - A dirty read occurs when one transaction reads data that has been modified by another transaction but has not yet been committed. In other words, a transaction reads data that may be rolled back later by the modifying transaction. Dirty reads can lead to inconsistencies if the modifying transaction is eventually rolled back. 

2. **Non-Repeatable Reads**:
   - A non-repeatable read occurs when a transaction reads the same data multiple times during its execution, but the data changes between each read due to the committed changes made by other transactions. This inconsistency results in different values being read for the same data within the same transaction. Non-repeatable reads can occur when transactions read data without acquiring proper locks or when using lower isolation levels that allow this phenomenon.

3. **Phantom Reads**:
   - A phantom read occurs when a transaction executes a query multiple times within its scope, and the result set changes between the executions due to the committed insert or delete operations performed by other transactions. This inconsistency results in different sets of rows being returned for the same query within the same transaction. Phantom reads can occur when transactions are allowed to see changes to the result set of a query made by other transactions that have committed their changes.

These phenomena are typically associated with lower isolation levels in database systems, such as READ UNCOMMITTED or READ COMMITTED. Higher isolation levels, such as REPEATABLE READ or SERIALIZABLE, aim to prevent or minimize these inconsistencies by providing stronger guarantees about the visibility and consistency of data during transaction execution.

It's important for database designers and developers to understand these phenomena and choose appropriate isolation levels based on the requirements of their applications to balance data consistency and performance.

## Normalization and  Denormalization

Normalization and denormalization are two techniques used in database design to optimize the structure and performance of a database.

1. **Normalization**:

Normalization is the process of organizing the attributes and tables of a relational database to minimize redundancy and dependency. The main goal of normalization is to reduce data redundancy and improve data integrity by ensuring that each piece of information is stored in only one place. This is achieved by breaking down large tables into smaller ones and establishing relationships between them.

Normalization typically involves several normal forms, each addressing specific types of data redundancy. The most commonly discussed normal forms are:

- First Normal Form (1NF): Ensures that each column contains atomic values and that each column has a unique name.
- Second Normal Form (2NF): Ensures that non-key attributes are fully functional dependent on the primary key.
- Third Normal Form (3NF): Ensures that non-key attributes are not transitively dependent on the primary key.

Normalization helps in maintaining data consistency and integrity, making it easier to update and modify the database schema. However, it may lead to increased complexity in querying the database, especially when dealing with complex relationships.

2. **Denormalization**:

Denormalization is the process of intentionally introducing redundancy into a database design to improve performance by reducing the number of joins needed for typical queries. It involves adding redundant data or grouping data in ways that were not present in the normalized schema.

Denormalization is typically done in cases where:

- There's a need for improved query performance, especially in read-heavy systems.
- The database schema is overly normalized, leading to complex joins and decreased performance.
- The application requires faster access to data at the cost of increased storage space and potential data inconsistency.

By denormalizing the database, queries can often be simplified, resulting in faster response times. However, denormalization may lead to data redundancy, which can potentially introduce anomalies during data modification operations (insert, update, delete). Therefore, careful consideration is required when denormalizing a database to ensure that data integrity is not compromised.

In summary, normalization and denormalization are two complementary techniques used in database design to achieve different goals: normalization to reduce redundancy and maintain data integrity, and denormalization to improve query performance at the expense of redundancy. The choice between the two depends on the specific requirements and constraints of the application.
