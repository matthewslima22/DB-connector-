
# DB Connector
DB V2 is a component used with the `code` attribute of the request to retrieve the client record in a database (MySQL, SQL server...)
you don't need to worry about downloading plug-ins and external drivers, it is responsible for abstracting the complexity, you just need to do some minor configuration to use it.

### Authentication:
1. Create a pipeline as an API.

2. Open the DB v2 configuration component.

3. Select the operation.

4. Authenticate an account in the database.
![Figure 3  User and password](https://user-images.githubusercontent.com/61173495/174700074-146318f4-75ba-49c0-8cce-7fcd6e25f87c.png "Figure 1. Authenticate")

5. Select the URL.
![Figure 4  URL](https://user-images.githubusercontent.com/61173495/174700119-c00d5c38-5091-4d80-b18a-961e68f19cac.png "Figure 2. URL")


6. Set instruction.
![Figure 5  Query table](https://user-images.githubusercontent.com/61173495/174700145-824100b4-6a5f-46e7-b39a-a5ea4fe9c742.png "Figure 3. Query table")

7. Click Play.


8. Connect the trigger to DB v2.

![Figure 7, Connector pipeline trigger](https://user-images.githubusercontent.com/61173495/174700238-0c378dfc-bb04-453d-af81-d511a0ddbeba.png "Figure 4. Connect the trigger")



9. Execute the pipeline.
![Figure 6  Response](https://user-images.githubusercontent.com/61173495/174700268-b0a6ce11-7451-4409-9cb3-37ed0fbbf4ad.png "Figure 5. Response")



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

![db_connector](https://user-images.githubusercontent.com/61173495/174700733-73f8d171-2358-4377-8788-1becdf9737dc.png "Figure 6. Flow")


> #### NOTE:
>When using a value that does not exist in the database we will get an empty list.

---

#### See also:
Conditional branching with Choice.
- Used to check if the response is valid.
- Route messages to a specific flow.
- Apply different treatments to a given dataset based on business functions and others.
