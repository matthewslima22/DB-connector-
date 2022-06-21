---
stoplight-id: 9v77usjg8xnh7
---

# DB Connector
DB V2 is a component used with the `code` attribute of the request to retrieve the client record in a database (MySQL, SQL server...)
you don't need to worry about downloading plug-ins and external drivers, it is responsible for abstracting the complexity, you just need to do some minor configuration to use it.

### Authentication:
1. Create a pipeline as an API.

2. Open the DB v2 configuration component.

3. Select the operation.

4. Authenticate an account in the database.
![Figure 1. User and password.png](https://stoplight.io/api/v1/projects/cHJqOjE0MDAyOA/images/SsNxk9jIl58 "Figure 1. Authenticate")

5. Select the URL.
![Figure 2. URL.png](https://stoplight.io/api/v1/projects/cHJqOjE0MDAyOA/images/WKRdPFvuyaY "Figure 2. URL")


6. Set instruction.
![Figure 3. Query table.png](https://stoplight.io/api/v1/projects/cHJqOjE0MDAyOA/images/Ec0NaStgyik "Figure 3. Query table")

7. Click Play.

8. Connect the trigger to DB v2.
![Figure 4, Connector pipeline trigger.png](https://stoplight.io/api/v1/projects/cHJqOjE0MDAyOA/images/jcGGtlpMK7Y "Figure 4. Connect the trigger")


9. Execute the pipeline.
![Figure 5. Response.png](https://stoplight.io/api/v1/projects/cHJqOjE0MDAyOA/images/KEHqIVjh7Tw "Figure 5. Response")



The result will return a structure in JSON format with 3 properties:

`data`: Array of objects that represents the rows returned from the database according to the defined query.

`updateCount`: Indicates how many table rows were affected by the executed query.

`rowCount`: Indicates how many rows were returned by the query.  

---

### Double braces

However if the goal is to retrieve only the record whose code was equal to the `code` attribute passed as parameter to the service,
digibee offers an expression language that can be used in pipeline development, especially when we need to access values from a json structure.
This language is **Double braces**.

**Double braces** allows you to access values from global pipeline metadata and JSON attribute values.
To access it should be done like this:

`select = from customers where code = {{ message.queryAndPath.code }}`

- Message indicates that we are accessing the component's input payload.


Double braces also serve to check if the code field returned an empty string if it didn't exist in the payload we are using. 
After the configuration is done let's test the logic one more time, so that the database returns the record linked to the `code` that was passed as a parameter instead of a list with all the data.
See the flow below for a better understanding.

![db_connector.png](https://stoplight.io/api/v1/projects/cHJqOjE0MDAyOA/images/FRGEtzPU0Ko "Figure 6. Flow")


> #### NOTE:
>When using a value that does not exist in the database we will get an empty list.

---

#### See also:
Conditional branching with Choice.
- Used to check if the response is valid.
- Route messages to a specific flow.
- Apply different treatments to a given dataset based on business functions and others.
