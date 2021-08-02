Code and System Review Checklist:

Reviewer & reviewee’s  behaviour and  attitude when review other’s code:
Be kind
Accept that many programming decisions are opinions. Discuss trade offs, which you prefer, and reach a resolution quickly.
Ask questions; don’t make demands. (“What do you think about naming this :user_id?”)
Ask for clarification. (“I didn’t understand. Can you clarify?”)
Avoid selective ownership of code. (“mine”, “not mine”, “yours”)
Avoid using terms that could be seen as referring to personal traits. (“dumb”, “stupid”). Assume everyone is intelligent and well-meaning.
Be explicit. Remember people don’t always understand your intentions online.
Be humble. (“I’m not sure - let’s look it up.”)
Don’t use hyperbole. (“always”, “never”, “endlessly”, “nothing”)
Be careful about the use of sarcasm. Everything we do is public; what seems like good-natured ribbing to you and a long-time colleague might come off as mean and unwelcoming to a person new to the project.
Consider one-on-one chats or video calls if there are too many “I didn’t understand” or “Alternative solution:” comments. Post a follow-up comment summarizing one-on-one discussion.
If you ask a question to a specific person, always start the comment by mentioning them; this ensures they see it if their notification level is set to “mentioned” and other people understand they don’t have to respond.
 

Category/Area of Code Review:
General
Clean Code & Code style 
Secure Coding
Performance 
Logging and Tracing
Concurrency 
Application Security
Error Handling
Maintainability & Testability
Domain(Business Logic)
Design and Architecture
Scalability 
Reliability & Availability
Design pattern
PCI DSS(FinTech)
API design

Clean Code:
Use Intention-Revealing Names
Pick one word per concept
Use Solution/Problem Domain Names
Classes should be small!
Functions should be small!
Do one Thing in a function.
Don't Repeat Yourself (Avoid code Duplication).
Explain yourself in code(write why in code not what)
Make sure the code formatting is applied(Can us tools)
Throw Exceptions rather than Return codes in case of business and technical error.
Don’t return null from the method.
 Each method should do a single task. Don’t mix business logic and network calls with the same method. Try to make the method unit testable.


General:
Use checked exceptions for recoverable conditions and runtime exceptions for programming errors
Try to use global exception handling and common Business and technical error response
Never ignore exceptions. Don’t overlook the catch block.
Return empty arrays or collections, not nulls.
Minimize scope of local variables. For earlier GC.
Avoid finalize
Always override hashcode when override equal.
Always override toString
Use marker interface to define type
Use an executor for tasks and thread.
Use the BigDecimal value of the method for string to big decimal/double.
Never use string literals at business logic check. Use enum or constant.

Secure Code:
Use password as array of characters instead of String
Make class final if not being used for inheritance
Restrict privileges: Application to run with the least privilege mode required for functioning
Check access control or authorization .
Input into a system should be checked for valid data size and range and check mandatory input fields(boundary conditions)
Avoid sensitive  data logging(like pin,password, card info)
Purge sensitive information from exceptions (exposing file path, internals of the system, configuration)
Consider purging(Call GC in case of java) highly sensitive from memory after use
Be careful about SQL injection when DB queries.
Check the api response fields. Is there any extra data or sensitive data shared to public client.
Define wrappers around native methods (not declare a native method public).
Make public static fields final (to avoid caller changing the value)
Performance:
Avoid excessive synchronization for thread safety. Try to avoid sharing resources in case of a multithreaded environment.  
Try to keep Synchronized section small operation(cpu/network/memory)
Avoid string literal concatenation. Try to use a string builder.
Avoid creating unnecessary objects.
Incase of network calls try to use connection pool, thread pool, socket pool.
Profine DB query and check search query happen on indexed field
Release resources (Streams, Connections, etc) in all cases
Careful about ORM N+1 query
Cache, distributed cache, Asynchronous Process(RabitMQ/Kafka)
Think about IO latency and CPU usage. 
Check if any unused library goes into production build.
Incase of in memory store avoid full object serialization and use custom serialization to save memory

Concurrency:
Avoid member variables when we use spring singleton beans.
Always sychoronze share resource
Use concurrentHashMap instead of Synchronize HashMap
Use HashMap or HashSet instead if TreeMap/Set when ordering is not important. 
Error Handling:
Reply consistent error response to client.
Handle proper error code(401,404,400 and 500)
Use custom error code for business logic.
Use Language map for error messages. 
Categories
 Business logic error
Technical Error
Upstream Service Error
Common Error

Logging & Tracing:
Maintain proper level
Use {} to pass variables at SLF4j, when concat string.
Don’t trace excessive logs.
Distributed tracing (Spring cloud sleuth, Zipkin,ELK)
Sensitive Info
Log User Context
In case of centralized log Use common trace id and service name. 
Application Security:
Proper authentication and authorization
Any insecure operation or api
Separate public and private/internal api
Incase of micro service try to use central auth server
Check about authentication and authorization network overhead
Never use default credentials at production. Specially for system/infrastructure related services.(DB,Cache,Auth,API GW, Http server,3rd party library)
Store password hash using salt
Encrypt or one way hash for OTP and other party credentials.
Do you ensure security of your rest api(https://betterprogramming.pub/10-essential-tips-for-writing-secure-rest-api-e297990d48c5)
Architecture:
Does yous system follow all good system design and architecture pattern
Does it follow twelve factor app(https://12factor.net)
Do you follow distributed system fallacy (https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing)
For the Data layer follow lambda architecture.
Do you follow only request response or event based architecture.
Do you follow 12 architecture principle
1.N+1 Design. Never less than two of anything and remember the rule of three
2.Design for Rollback. Ensure you can roll back any release of functionality 
3.Design to be disabled. Be able to turn off anything you released
4.Design to be monitored. Think about monitoring during design. Not after.
5.Design for multiple Live sites. Don’t box yourself into one site solution
6.Use mature technology. Use thing you know work well
7.Asynchronous design. Communicate synchronously only when absolutely necessary 
8.Stateless Design. Use state only when the business return justifies it .
9.Scale Out NOT Up. Never rely on a bigger or faster system.
10.Design for at least two axes. Think one step ahead of your scale beads.
11.Bue when Non Core. If you aren’t the best at building it and it doesn’t offer competitive differentiation, buy it.
12.Commodity Hardware. Cheaper is better most of the time.  


Design Pattern:
SOLID
DRY
KISS
Creational Pattern(Singleton,Factory,Builder,Adapter)
Behavioral Pattern(Strategy,Chain Responsibility,Observer)
Scalability:
Can system easily scalable 
Is your service elastic
Use stateless service for horizontal scalability.
DB Sharding
DB Partition 
DB replication
Use read replica to independent read operation
Cache high read and low write operation
Check and monitor DB read and write query ration.
Use fail first and circuit breaker mechanism
Network call overhead (use socket pool or grpc)
Check alway DB network call round trip. Alway try to reduce it.
Did you address c10K problem for network communication?
Reliability & Availability:
Handle Timeout
Implement Circuit Breaker Pattern
Implement Bulkhead pattern
Implement idempotent operation  
Maintainability & Testability:
How much test coverage 
Unit, Integration and System Testing
Proper CI/CD pipeline
Any option for canary deployment



Monitoring:
Can you monitor your system health and resources?


Can you monitor your business performance?
Domain:
Business Logic implemented properly at code base
Service properly isolated against domain and bounded context.
Try to follow domain driven design.


PCI DSS:(For FinTech):
12 requirements:
Install and maintain a firewall configuration to protect cardholder data
Do not use vendor-supplied defaults for system passwords and other security parameters
Protect stored cardholder data
Encrypt transmission of cardholder data across open, public networks
Use and regularly update anti-virus software or programs
Develop and maintain secure systems and applications
Restrict access to cardholder data by business need to know
Assign a unique ID to each person with computer access
Restrict physical access to cardholder data
Track and monitor all access to network resources and cardholder data
Regularly test security systems and processes
Maintain a policy that addresses information security for all personnel


API Design:
Use kebab-case for URLs
Bad:
/systemOrders or /system_orders
Good:
/system-orders


Use camelCase for Parameters
Bad:
/system-orders/{order_id} or /system-orders/{OrderId}
Good:
/system-orders/{orderId}
Plural Name to Point to a Collection
Bad:
GET /user or GET /User
Good:
GET /users
URL Starts With a Collection and Ends With an Identifier
Bad:
GET /shops/:shopId/category/:categoryId/price
This is bad because it’s pointing to a property instead of a resource.
Good:
GET /shops/:shopId/ or GET /category/:categoryId
Keep Verbs Out of Your Resource URL
Bad:
POST /updateuser/{userId} or GET /getusers
Good:
PUT /user/{userId}
Use Verbs for Non-Resource URL
POST /alerts/245743/resend
Keep in mind that these are not our CRUD operations. Rather, these are considered functions that do a specific job in our system.
Use camelCase for JSON property
Bad
{
   user_name: "Mohammad Faisal"
   user_id: "1"
}
Good
{
   userName: "Mohammad Faisal"
   userId: "1"
}
Monitoring
RESTful HTTP services MUST implement the /health and /version and /metrics API endpoints. They will provide the following info.
/health
Respond to requests to /health with a 200 OK status code.
/version
Respond to request to /version with the version number.
/metrics
This endpoint will provide various metrics like average response time.
/debug and /status endpoints are also highly recommended.
Don’t Use table_name for the Resource Name
Don’t just use the table name as your resource name. In the long run, this kind of laziness can be harmful.
Bad: product_order
Good: product-orders
This is because exposing the underlying architecture is not your purpose.
Use API Design Tools
Use Simple Ordinal Number as Version
Good:
http://api.domain.com/v1/shops/3/products
Always use versioning in your API because if the API is being used by external entities, changing the endpoint can break their functionality.
 Include Total Number of Resources in Your Response
Bad:
{
  users: [ 
     ...
  ]
}
Good:
{
  users: [ 
     ...
  ],
  total: 34
}
Accept limit and offset Parameters
GET /shops?offset=5&limit=5
Take fields Query Parameter
The amount of data being returned should also be taken into consideration. Add a fields parameter to expose only the required fields from your API.
Example:
Only return the name, address, and contact of the shops.
GET /shops?fields=id,name,address,contact
It also helps to reduce the response size in some cases.
Don’t Pass Authentication Tokens in URL
Bad
GET /shops/123?token=some_kind_of_authenticaiton_token
Good
Instead, pass them with the header:
Authorization: Bearer xxxxxx, Extra yyyyy
Validate the Content-Type
The server should not assume the content type. For example, if you accept application/x-www-form-urlencoded then an attacker can create a form and trigger a simple POST request.
So, always validate the content-type and if you want to go with a default one use content-type: application/json
Use the Relation in the URL For Nested Resources
GET /shops/2/products : Get the list of all products from shop 2.
GET /shops/2/products/31: Get the details of product 31, which belongs to shop 2.
DELETE /shops/2/products/31 , should delete product 31, which belongs to shop 2.
PUT /shops/2/products/31 , should update the info of product 31, Use PUT on resource-URL only, not the collection.
POST /shops , should create a new shop and return the details of the new shop created. Use POST on collection-URLs.
CORS
Do support CORS (Cross-Origin Resource Sharing) headers for all public-facing APIs.
Consider supporting a CORS allowed origin of “*”, and enforcing authorization through valid OAuth tokens.
Avoid combining user credentials with origin validation.


Security
Enforce HTTPS (TLS-encrypted) across all endpoints, resources, and services.
Enforce and require HTTPS for all callback URLs, push notification endpoints, and webhooks.


Errors
Errors, or more specifically service errors, occur when a client makes an invalid or incorrect request to a service or passes invalid or incorrect data to a service, and the service rejects the request.
Examples include invalid authentication credentials, incorrect parameters, unknown version IDs, etc.
Do return 4xx HTTP error codes when rejecting a client request due to one or more Service Errors.
Consider processing all attributes and then returning multiple validation problems in a single response.
Golden Rules
If you are ever in doubt about an API formatting decision, these golden rules can help guide us to making the right decision.
Flat is better than nested.
Simple is better than complex.
Strings are better than numbers.
Consistency is better than customization.
