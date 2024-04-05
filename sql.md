## Clustered and Non-Clustered Index

In the context of databases, clustered and non-clustered indexes are two different ways of organizing and accessing data within a table efficiently.

**Clustered Index:**

- A clustered index is an index structure in which the data rows in the table are physically sorted according to the order of the index key.
- In a clustered index, the actual data rows are stored in the leaf nodes of the index's B-tree structure. This means that the leaf nodes of the index contain the actual data pages of the table.
- A table can have only one clustered index because the physical order of the data can only be sorted in one way.
- When you create a clustered index on a table, you are essentially reordering the data in the table based on the key columns of the index.
- Because the data is physically sorted, accessing rows based on the clustered index is usually faster, especially for range queries or queries that involve sorting.

**Non-Clustered Index:**

- A non-clustered index is an index structure in which the order of the index key does not match the physical order of the data rows in the table.
- In a non-clustered index, the leaf nodes of the index's B-tree structure contain pointers to the actual data rows rather than the data rows themselves.
- A table can have multiple non-clustered indexes, allowing for different access paths to the data.
- When you create a non-clustered index on a table, it does not change the physical order of the data in the table; instead, it creates a separate structure that allows for efficient access to the data based on the indexed columns.
- Non-clustered indexes are useful for queries that frequently filter, sort, or group data based on columns other than those in the clustered index, as well as for covering queries (queries that can be satisfied entirely from the index without accessing the actual data rows).

In summary, a clustered index physically orders the data rows in the table based on the index key, while a non-clustered index provides an additional structure for efficient access to the data rows without 
changing their physical order. Each type of index has its own advantages and use cases, and the choice between them depends on the specific requirements and characteristics of the database and the queries it needs to support.

Let's consider a simple example with a hypothetical table called `Employees` with the following structure:

```
| EmployeeID | FirstName | LastName | DepartmentID | Salary |
|------------|-----------|----------|--------------|--------|
| 1          | Alice     | Smith    | 101          | 50000  |
| 2          | Bob       | Johnson  | 102          | 60000  |
| 3          | Charlie   | Brown    | 101          | 55000  |
```

Now, let's discuss how clustered and non-clustered indexes would work in this scenario:

**Clustered Index Example:**

Let's say we create a clustered index on the `EmployeeID` column, which uniquely identifies each employee. In this case, the data in the `Employees` table will be physically sorted by the `EmployeeID`.

```sql
CREATE CLUSTERED INDEX IX_EmployeeID ON Employees (EmployeeID);
```

After creating the clustered index, the physical order of the rows in the `Employees` table will be rearranged based on the `EmployeeID`. This means that if you query the `Employees` table based on `EmployeeID`, the database engine can quickly locate the corresponding rows because they are physically sorted according to the index key.

**Non-Clustered Index Example:**

Now, let's create a non-clustered index on the `DepartmentID` column, which specifies the department to which each employee belongs.

```sql
CREATE NONCLUSTERED INDEX IX_DepartmentID ON Employees (DepartmentID);
```

or

```sql
CREATE INDEX IX_DepartmentID ON Employees (DepartmentID);
```

In this case, the data in the `Employees` table remains physically sorted by the `EmployeeID`, as the non-clustered index does not affect the physical order of the data. However, the database engine creates a separate index structure that contains pointers to the data rows based on the `DepartmentID`. This index allows for efficient access to the data rows when querying based on `DepartmentID`, even though the physical order of the rows in the table remains unchanged.

In summary, the clustered index physically sorts the data rows in the table based on the index key, while the non-clustered index provides an additional structure for efficient access to the data rows without changing their physical order.****
