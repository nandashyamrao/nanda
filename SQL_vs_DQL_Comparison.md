
# **SQL vs DQL Command Comparison**

Dynatrace Query Language (DQL) is designed for querying and analyzing observability data, focusing on entities rather than traditional database tables. While DQL shares similarities with SQL in functionality, its syntax and purpose are aligned with Dynatrace's monitoring capabilities. This guide compares common SQL commands with their DQL counterparts.

---

## **Comparison Table**

| **Functionality**        | **SQL Command**                                                                                   | **DQL Command**                                                                                                                                                                      |
|--------------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Select Data**          | `SELECT column1, column2 FROM table_name;`                                                       | `fetch dt.entity.<entity_type> \| fields column1, column2`                                                                                                                           |
| **Filter Data**          | `SELECT * FROM table_name WHERE condition;`                                                      | `fetch dt.entity.<entity_type> \| filter condition`                                                                                                                                  |
| **Aggregate Functions**  | `SELECT COUNT(*), AVG(column) FROM table_name;`                                                  | `fetch dt.entity.<entity_type> \| summarize count = count(), average = avg(column)`                                                                                                  |
| **Group By**             | `SELECT column, COUNT(*) FROM table_name GROUP BY column;`                                       | `fetch dt.entity.<entity_type> \| summarize count = count(), by: {column}`                                                                                                           |
| **Order By**             | `SELECT * FROM table_name ORDER BY column ASC/DESC;`                                             | `fetch dt.entity.<entity_type> \| sort column asc/desc`                                                                                                                              |
| **Join Entities**        | `SELECT * FROM table1 INNER JOIN table2 ON table1.id = table2.id;`                               | `fetch dt.entity.<entity_type_1> \| join [fetch dt.entity.<entity_type_2>], on: {left[field] == right[field]}`                                                                        |
| **Combine Results**      | `SELECT * FROM table1 UNION SELECT * FROM table2;`                                               | `fetch dt.entity.<entity_type_1> \| append [fetch dt.entity.<entity_type_2>]`                                                                                                        |
| **Limit Results**        | `SELECT * FROM table_name LIMIT 10;`                                                             | `fetch dt.entity.<entity_type> \| limit 10`                                                                                                                                          |
| **Rename Columns**       | `SELECT column1 AS new_name FROM table_name;`                                                    | `fetch dt.entity.<entity_type> \| fieldsRename column1, alias: new_name`                                                                                                             |
| **Calculate New Fields** | `SELECT column1, (column2 * 2) AS calculated_field FROM table_name;`                             | `fetch dt.entity.<entity_type> \| fieldsAdd calculated_field = column2 * 2`                                                                                                          |
| **Remove Duplicates**    | `SELECT DISTINCT column1 FROM table_name;`                                                       | `fetch dt.entity.<entity_type> \| unique column1`                                                                                                                                    |
| **String Matching**      | `SELECT * FROM table_name WHERE column LIKE '%value%';`                                          | `fetch dt.entity.<entity_type> \| filter contains(column, 'value')`                                                                                                                  |
| **Date Filtering**       | `SELECT * FROM table_name WHERE DATE(column) = '2024-12-21';`                                    | `fetch dt.entity.<entity_type> \| filter column == '2024-12-21'`                                                                                                                     |
| **Mathematical Operations**| `SELECT column1, (column2 + column3) AS sum FROM table_name;`                                  | `fetch dt.entity.<entity_type> \| fieldsAdd sum = column2 + column3`                                                                                                                 |
| **Conditional Statements**| `SELECT column1, CASE WHEN condition THEN 'value1' ELSE 'value2' END AS new_column FROM table;` | `fetch dt.entity.<entity_type> \| fieldsAdd new_column = if(condition, 'value1', else: 'value2')`                                                                                    |

---

## **Key Differences Between SQL and DQL**

1. **Entity-Based Queries**:
   - **SQL** queries operate on database tables, requiring predefined schemas and structured data.
   - **DQL** focuses on **entities**, such as `dt.entity.service`, `dt.entity.host`, and `dt.entity.process`, which represent monitored resources in Dynatrace.

2. **Dynamic Attribute Retrieval**:
   - In DQL, attributes (e.g., `host.name`, `service.responseTime`) are dynamically detected and available based on the entity type.

3. **No Schema Requirements**:
   - Unlike SQL, which relies on rigid schemas for tables, DQL operates on real-time entity data without needing predefined schemas.

4. **Pipeline Processing**:
   - DQL uses a pipeline (`|`) to chain commands, where the output of one step serves as the input for the next, enabling more intuitive data transformation.

---

## **Entity-Centric Query Example in DQL**
**Goal**: Find all services running Java with response times greater than 500ms, grouped by service name.
```dql
fetch dt.entity.service
| fieldsAdd service.name, service.technology, service.responseTime
| filter service.technology == "JAVA"
| filter service.responseTime > 500
| summarize count() by service.name
```

**Explanation**:
- `dt.entity.service`: Represents all services in the environment.
- `fieldsAdd`: Extracts specific attributes for analysis.
- `filter`: Narrows results to services meeting specified conditions.
- `summarize`: Groups results by service name and calculates a count for each group.

---

## **Conclusion**
Understanding the differences between SQL and DQL enables effective usage of Dynatrace's query language for monitoring and observability analysis. By focusing on entities and leveraging pipeline processing, DQL provides a streamlined approach to querying real-time monitoring data.

For more details, refer to the [Dynatrace Documentation on DQL](https://www.dynatrace.com/support/help/).
