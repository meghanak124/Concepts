list vs tuple
list is mutable and tuple is immutable

mutable vs immutable
mutability is we can add/delete/change the values
and immutability is we cannot modify the data

generators
generators are special functions that give output like one-at-a-time. They use a specil keyword called yield which yields the output 

decorators basics
decorator are special functions that extend the features of other functions without changing/modifying that function

multithreading vs multiprocessing
The core difference is that Multithreading shares the same memory space within a single process, making it ideal for I/O-bound tasks, while Multiprocessing uses completely separate memory spaces for each process, making it ideal for CPU-bound tasks.

async vs sync
synchronous is running tasks one-after-one. Asynchronous runs tasks not waiting for any other task to complete.

GIL basics
GIL is a special feature of python which isolates threads. As threads share memory. GIL(Global Interpreter Lock) applies a lock, so that only single thread can make changes to memory and no two threads run parallely. However, context swiitching takes and the user feels like the threads are run prarallely

request lifecycle
request goes from the browser to web server. WSGI/ASGI bridges webserver and django by converting http request to python dictionary.  Middlewares like sessions, security, authentication takes action. URL routing routes to views. Views has the business logic and interacts with database using ORM and returns a API/HTTP response or renders a template. Which again go thorugh middleware back and to browser

middleware
Middleware is a framework of hooks that acts as a centralized gatekeeper, processing every incoming HTTP request before it reaches a view, and modifying every outgoing HTTP response before it returns to the user.Example , we have authentication middleware, session middleware. security middlewares like XSS, clickjacking

ORM
ORM stands for Object-Relational Mapping. It is a programming technique that lets you interact with a relational database using python objects instead of writing raw SQL queries

authentication vs authorization
authentication is who you are and authorization is what are you allowed to do
we have decorators for authorization in django like login_required, permission_required etc
Django also provided authentication middleware also login form. 

migrations
migrations are the chnages in models. we can makes changes in models and do makemigrations to reflect them in the database. 

class-based vs function-based views
we can write views using classes as well as functions. 
use Class-Based Views (CBVs) for standard, repeatable operations, and Function-Based Views (FBVs) for unique, custom logic.

sessions/cookies
django manages session using session middleware. When a user logs in, session is created and session id is stored in cookies. All the user activity is stored in the session.
and the session id is verified using the session id in cookies

CSRF
CSRF is an attack. Cross site request forgery, this happens when the request is sent from a malicious site to the server. If the server doesnot know it is malicious, the data can be forgered. Django prevents using CSRF token which are sent with unsafe methods like POST, PUT, PATCH, DELETE which actually modify the data.

joins
we have 4 primary joins:inner, left, right and full join
inner join gives common values from both tables
left join gives common and all values from left table
right join gives common and all values from right table
full join gives all the values from both the tables
In django, we use select_related and prefetch_related for joins

indexing basics
A database index works exactly like the index at the back of a textbook. Instead of flipping through every single page from start to finish to find a specific keyword, you look up the keyword in the index alphabetically and jump straight to the exact page number.

normalization
normalization is a process of structuring a relational database schema to eliminate data redundancy and prevent data anomalies (insertion, update, and deletion anomalies) by breaking down large tables into smaller, well-related tables.

primary key vs foreign key
primary key is unique key of the table which identifies each row uniquely. It cannot be null or duplicate
whereas foreign key is a key that links that references a Primary Key in another table.

transactions
a database transaction as a single unit of work that bundles multiple SQL operations together.Transactions need to ACID properties.

ACID properties 
ACID properties are atomicity, Consistency, Isolation and Durability. Atomicity is that All or nothing. Consistency, each transaction need to move the database from one valid state to another valid state without any inconsistencies. Isolation is that the transaction need to be isolated from each othe such no 2 transactions change database at the same time. Durability is the data is stored permanently once the transaction is commited even if the system crashes

explain your project
My project is bookmyshow clone. Frontend was built using HTML, CSS, and JavaScript for rendering movie listings, seat layouts, booking flow, and user interactions. Backend was built using Django following the MVC/MVT architecture. Django handled authentication, APIs, booking workflows, business logic, and database operations. For seat booking consistency, I used atomic transactions and select_for_update() row-level locking to prevent race conditions during simultaneous booking attempts. I integrated external APIs to fetch movie and IPL match data dynamically. I have deployed the project on render

biggest challenge
Biggest challenge was to handle seat selection concurrency issue. What if 2 users select the same seat. so For seat booking consistency, I used atomic transactions and select_for_update() row-level locking to prevent race conditions during simultaneous booking attempts
and other issue was, I first used default db on production. But with each redepolyment, the db was being refreshed and all the data was going off. So i shifted to postgresql on prodcution and continued with sqlite3 locally

how booking consistency handled
means??

why PostgreSQL
becuase it was free, consistent, secure, open-source and flexible also fast

why Redis
Redis is used as cache technology. Which is fast , in-memory architecture, data persistence, atomicity, high availability and scalability

why Docker
docker is an open-source platform that uses containerization to package an application and all of its dependencies into a single, isolated unit called a container

deployment issues
and other issue was, I first used default db on production. But with each redepolyment, the db was being refreshed and all the data was going off. So i shifted to postgresql on prodcution and continued with sqlite3 locally

race condition
Biggest challenge was to handle seat selection concurrency issue. What if 2 users select the same seat may lead to race condition. so For seat booking consistency, I used atomic transactions and select_for_update() row-level locking to prevent race conditions during simultaneous booking attempts

What is Docker?
Docker is a containerization platform that allows developer to package the whole application, its dependencies, run time, configurations into a docker container. So that the docker container can be run with same environment on any machine. 

Why use containers?
Containers are running environment created from a docker image. This is where your code executes in isolation from rest of the host computer

Difference between VM and Docker
Virtual Machine creates the whole virtual OS, kernel which costs higher. But Docker is lightweight as it creates an environment including the application code, dependencies, runtime, libraries etc that can actual run the application on any machine.

What is Dockerfile?
Docker file is a plain-text script containing sequential instructions that Docker reads to automatically build a layered, reproducible container image

What is image vs container
 Docker Image is the compiled, immutable blueprint package generated via the docker build command. Docker Container is the live, running, sandboxed instance of that image generated via the docker run command

Why Redis
Redis is used as cache technology. Which is fast , in-memory architecture, data persistence, atomicity, high availability and scalability

Why Caching?
Cache is used to store data. This reduces the number of hits to database. Caching reduces the latency. Avoids database bottlenecks.

What is in-memory DB?
in-memory DB is a database system that stores data directly in a computer's main memory (RAM) instead of a traditional hard drive (HDD) or solid-state drive (SSD)

What happens if Redis fails?
If redis goes down completely, All the request hit databse this may lead to databse bottlenecks and my application may become terribly slow. Although follower redis server takes the request even if the leader server goes down due to server replication

props vs state
Props act like arguments passed to a function. They allow you to pass data from a parent component down to a child component, making your components reusable
State acts like local variables declared inside a function. It represents the local memory of a component that can change over time, usually due to user interactions.

useEffect
useEffect is a built-in React Hook that lets you synchronize a functional component with an external system by running code in response to rendering.

virtual DOM
The Virtual DOM (VDOM) is a lightweight, in-memory programming concept where an idealized or "virtual" representation of a user interface is kept in system memory and synced with the "real" DOM by a library such as React.

why Redux
Redux is brought as solution to Prop Drilling by providing a single, centralized and predcitable state container(Redux store) for your entire application

component lifecycle basics
Mounting -> updating -> unmounting

What is RAG?
RAG means Retrieval Augmented Generation which means unlike traditional AI which work on given input and generate next token. RAG refers to the documents and find the answer to the input using embeddings in vector DB

What is vector DB?
Vector DB is used in RAG to store Embeddings which group words with similar meaning

What is LangChain?
LangChain is a class which gives us all classes and function to implement RAG
like converting embedding, a default vector Db etc It ensures we dont implement it from scratch

What is prompt engineering?
Refining the prompt to be clearly, specific and structured so that AI can find the best possible output

difference between fine-tuning and RAG
fine-tuning is refining the input so that the output from AI is as perfect as possible
RAG is going through the documents and find the solution to the input and give the accurate answer

1. Django is a python framework which allows developers to build secure, scalable and maintainable web applications faster. As It provides so many functionalities such as ORM, admin panel, Security features, form handling by deafult so is called batteries included

2. MVT architecture is similar to MVC architecture. Model View and Template where Model defines the structure of the data. View has the business logic and Template defines the User interface. 

3. Django is heavy, batteies included framework while flask is lightweight microframework that gives you only the bare essentials and lets your own tools

4. All these are HTTP methods 
GET - fetch data
POST - create data
PUT - change all the values else over rides
PATCH - changes only particular values
DELETE - deletes values

5. What are Django middlewares?
Can you name some commonly used middlewares?
Django middlewares like bridges between request view function and response. Every request and response is interferred with some middleware process.
some commonly used middlewares are Authentication, Clickjacking, XSS, etc

6. Authentication is the identity of the user and atuhorization is what resources an authenticated user can access. Authentication is implemented with authenticate() and authroization is implemented using decorators like login_required or permission_required

7. ORM stands for Object Relation Mapping which allows django to represent tables using python objects. It prevents sql injection as it sanitizes and parameteries the user inputs. It is cleaner, simple and secure than sql queries.

8. Both are solutions of N+1 Query Performance issue. Select_related it used when point to single object like one-to-one or many-to-one and prefetch_related is used when pointing to many objects like many-to-many and one-to-many

9. Migrations are changes in the structure of data. When we run makemigrations, these migrations are reflected on the database. These are files that are created when we make changes in structure of data and run migrate command. 

10. Charfiled allows short, single line text and textfield allows long, multi line text

11. on_delete=models.CASCADE means that if a referenced row in the parent table is deleted, the entire corresponding row in the child table is automatically deleted as well

12. CSRF is an attack where server gets a request from malicious site and server doesnot if it is from autorized site. Cross site request forgery can be prevented by django using CSRF tokens. Where django generates a csrf token using secretkey and sends with every PUT, POST, PATCH, DELETE(unsafe methods as they change data) to authorize the origin of the request

13. sessions are stored in servers and are created when a user logs in. The session id is stored in cookies which are in user system. Whenever user sends a request, the session of the user is used to get his previous activity. 

14. When a request hits django, it first goes to WSGI/ASGI based sync/async which converts http raw data to python/event dictionaries. Then the request passes through the middlewares. Then url routing in urls route the request to corresponding view function. View function fetches data from models usig ORM if required. Then response is sent back as HTTP response or renders template. then this response is passed through middlewares backward and then sent to browser.

15. Function based views are the views written in python functions and class based views are views wrapped in python classes. Function based views are like standard scripts whereas CBV hide underlying logic inside inherited class methods. CBV use mixins and inheritence to reuse code. 

16. A- Atomicity. All or nothing. If one query in a transaction fails, entire transaction is aborted
C - Consistency- each transaction must lead the database from one consistent state to other consistent state
I- Isolation - Each transaction need to be isolated from other because race condition may occur and corrupt the data
D - Durability - Once a transaction is commited, data should be durable even if the system crashes
ACID properties make the database consistent, secure and presistant

17. Indexing is a technique for fast retrieval from database. Instead for parsing all the rows in the database. Indexing helps find the row faster. It is like primary key of the table. However, it makes select queries drastically speed but insert, delete and update queries become slower because of updating indexes and table when a change occurs

18. Primary key is the unique not null element of the table which uniquely identifies each row of the table And Foreign key is a reference key linked to primary key of another table

19. Normalization is a technique to reduce the redundancy, anomalies by dividing the table into smaller tables

20. Race condition happens when multiple concurrent transactions access and modify the same data at the same time and end up with corrupting the data or incorret data

21. I used atomicity and row-level locking using select_for_update().
I wrapper the seat selection logic in with transaction.atomic() and locked the seat when selected. This makes no 2 user select a single seat at a time. 

22. transaction.atomic() makes the transaction atomic. Suppose if the any query in the transaction failed like payment or selection of seats etc, the whole transaction is failed. 
You cannot book tickets without payment or you cannot make payment without selecting seats. All or nothing.

23. select_for_update() is a django function that implements row_level_locking, select_for_update() is a Django QuerySet method used to lock database rows until the current transaction ends. It generates a SELECT ... FOR UPDATE SQL statement, which prevents other concurrent database transactions from modifying or locking those specific rows until your changes are saved.

24. SQL is a relational database that stores data in rows and columns example mysql 
NoSQL is non-relational database that stores in flexible data structures like key-values, documents etc example: Mongodb

25. Postgresql is sql db which is faster, secure, scalable, consistent, open-source, reliable. 

26. Redis is a in-memory database serving as cache. It stores data in JSON format

27. Redis is fast becuase it stores data in-memory and is faster to retrieve the data from server's RAM

28. Caching is storing frequently used data in cache to retrieve faster the next time. For example for a e-commerce website, the home page doesnot have hit the database always

29. I would cache generic data instead of user specific data or sensitive data. Example I would keep movies data in cache because each time user logins in, movies commonly appear to all the users.

30. If redis goes down completely, All the request hit databse this may lead to databse bottlenecks and my application may become terribly slow. Although follower redis server takes the request even if the leader server goes down due to server replication

31. Docker is containerization platform that containers the whole application code, runtime, dependencies, libraries to create the same environment on any system to run the application without actually creating whole operating system, kernal etc

32. Docker Image is created with build command. It is a blueprint of the application and Docker container is running instance of docker image created with run command

33. Docker containerizes only the dependencies, application code, runtime whereas virtual machine creates whole operating, harware, kernel virtually which is heavier than docker

34. Docker file is text-scripted file that contains the instructions to create docker image

35. Docker solves a most common problem "It runs on my machine" by containerizing the application and dependencies. This container can be shared and set up the same environment anywhere so that the application runs seamlessly on any system.

36. List is mutable datastructure which allows to add/delete/modify the values after creation. Tuple immutable data structure that cannot be changed once created

37. generators are special functions that gives lazy output using keyword called "yield". It doesnot return the entire output once. It yields the output, and we need to loop throught the output to get one-at-a-time

38. decorator are special functions that extend the features of other functions without changing/modifying that function

39. mutltithreading is running multiple execution contexts or threads of a single process which share memory and multiprocessing is running independent process on different CPU cores which has separate memory to each process

40. GIL is a special feature of Cpython where it applies a lock to allow only single thread to run the python byte code. When multiple threads do CPU-based task, race condition may occur. So Global interpreter Lock makes one thread to run the python byte, Due to context switching, user feels like threads are running in parallel.

41. Synchronous is runing the tasks one-after-one. The next task waits for the previous task to finish and only then it is going to start executing. Ashynchronous is a Tasks happen independently without waiting for previous ones to finish.

42. virtual DOM is in-memory tree sturcture of the structure of the page. Frameworks like React or redux create a virtual DOM when page renders. It doesnot render whole new page when event occurs, instead event triggers a component that needs to be changed and rest of the DOM remains same. 

43. Props are features that come from the parent to child components like user.username etc and state is the value that keep updating with the events

44. useEffect() is a hook in react which shows the side effects of the event.

45. Redux is the frontend technology that solves prop drilling issue using centralized store that stores all the data so that any component that need data can directly access it without being transferred from parent component

46. Database replicas for read operations, messaging queues  like rabbitmq/celery, caching, caching replicas, rate limiting, Containerizing using docker, moving from gunicorn to nginx, I would use CDN. Make the project split into microservices for individual management

47. Database replicas for read operations, use cache like redis

48. idontknow, alert()? or popups??

49. kafka is event streaming that works on events like booking etc. then split it to booking done, cancel booking etc. Whereas rabbitmq is a message broker that stores the tasks for routes to respective consumer/microservice. Celery is a task queue framework specifically designed to offload time-consuming functions into background workers. It requires a message broker (like Redis or RabbitMQ) underneath it to pass the messages.It is not that which we can use, they are used together to make the application efficiently

50. Load balancing is balancing the number of requests to a server. Based algorithms like round robin or server with least number of request gets the server so that any ONE server doesnot higher load and other server is hanging free

52. RAG is a Ai technology where the LLM refers to the documents and retrieve the data according to the input. It uses embeddings, vectordb to get the accurate answer frm the AI
