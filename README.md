# Lecture Notes for Data Engineering in Spring 2015

## Lecture 1

- Created a repository for writing notes
- Data Engineering: What is it?
  - Social Networks
  - Data Analytics 
    - Sampling 
    - Machine learning
  - Storage
    - NoSQL
    - Document databases
    - Graph databases
    - Key-value stores
    - Colomner stores (not key-values; different)
  - Big data
  - Data collection and cleaning
    - How to access it?
    - Has to clean before it can be stored
    - Example
      - Twitter --> clients
      - Tweetbot --> IOS
  - Infoviz
    - Huge data sets, how do you view them to the user?
    - D3 (JS framework)
    - Tablo
    - R
  - Data engineering
    - Data life cycle
    - Question -> curation triage --> prioritization [DATA SCIENTIST]. Collection generation [SOFTWARE ENGINEERS] --> clean up     [SOFTWARE ENGINEERS] --> storage [SOFTWARE ENGINEERS] <-- --> processing/analysis [DATA SCIENTISTS] --> query + visualize + act [DATA SCIENTISTS]
- Big Data
  - Request response cycle 
  - Type http:// --> access HTML file. HTTP request. Network protocol. --> Get --> POST --> PUT --> DEL

## Lecture 2

Web browser --> web server (HTTP server) --> handler
Example: ebay.come/product/10
GET --> POST --> DELETE --> PUT
Until handler returns something, we're stuck in request cycle. 
Example: any web page, no requests. It'll say: index.html (service)

REST
Representational State Transfer
URL are a subtype of URI:
	- Resources 
CRUD
	- Create
	- Read
	- Update
	- Destroy
How to operate it on service?
	- Ex: service that has information on users. You'll have a URI which references a particular resource. REST will apply HTTP methods to it (GET/POST/PUT/DELETE). Call get on /users, so, get --> read (gets back the current state of the resource). Post --> create (data). Put --> update . If it's /users/{ID} --> it's an update on a user id. Update the user so that the next time I'll do a get, all of the information will be there. Delete --> destroy.

In Class Coding
In VIM:

::

	require 'sinatra'
	require 'sinatra/relaoder' if development?
	
	configure do
		Set :port, 3000
	end
	
	get '/api/1.0/whattimeisit' do
		"Hello World"
	end

Then in ANOTHER window:

$ curl http://localhost:3000/api/1.0/whattimeisit  full request response cycle

In VIM again:

require 'sinatra'
require 'sinatra/relaoder' if development?

require 'json'

configure do
	Set :port, 3000
end

get '/api/1.0/whattimeisit' do
	{ status: true, message: "Hello World" }.to_json
end

Then do curl again. 

In VIM again:

require 'sinatra'
require 'sinatra/relaoder' if development?

require 'json'

configure do
	Set :port, 3000
end

get '/api/1.0/whattimeisit' do
	{ status: true, message: Time.now }.to_json + "\n"
end

To run it:

ruby service.rb

Database?
Id 
--> input
<-- output
Errors

## Lecture 3

*REST*
- Architectural style for web services 
	- Invented by Roy Fielding at UC Irvine 
	- REST is an approach to developing web services that mimics the design of the Web itself
	- Your service provides access to a linked set of resources 
	- For each resource, you can perform operations on it similar to the main operations (aka methods) of the HTTP specification. 
	- CRUD
	- Post, get, put, delete 
	- Examples 
		○ GET /api/1.0/users --> retrieve a list of all users
		○ GET /api/1.0/users/0  --> retrieve the details of User 0
		○ POST /api/1.0/users --> create a new user
	- Examples (updating a user)
		○ PUT /api/1.0/users/0 --> update User 0
		○ DELETE /api/1.0/users/0 --> delete User 0
		○ GET /api/1.0/search?q=tattersail --> perform a search with the query tattersail (%20 = space)
	- Each operation may produce a result
		○ With RESTful services, JSON format is king
			§ Keys and values = strings
			§ Highly compressible 
		○ POST and PUT methods typically send data
			§ Also in JSON format
			§ May be in the URL or in the body of the HTTP Request 
				□ For GET, the data may appear as query params 
		○ Other formats are possible: HTML and XML are typical 
		○ If a request needs to be authenticated 
			§ The authentication data appears in HTTP headers 
			§ HTTP: how to log into websites, authentication, cookies
			§ Basic authentication: particular header you need to populate with user info

*How do you think operations on two resources are handled?*
- Two different relative path: /users/0 and /possessions/1 (users that can have possessions; can create possessions independently and individually create users).
	- /users/0/possessions (possessions owned by user 0)
	- GET /api/1.0/posts/0/comments/1 --> get first comment on post 0
	- POST /api/1.0/posts/0/comments --> create a new comment on post 0

*Issues*
- Security: How do you authenticate users?
- Identity: How are ids assigned to resources?
- Failure: How do we handle failure situations?
- Persistence: How are resources stored?

*Example*
- Contacts web service
- Implemented in both Ruby and JS
- Technologies used:
	- Sinatra (handling HTTP request)
	- Rspec (testing)
	- Typhoeus (Ruby library to do HTTP request on client side)
	- Node (wrapper around chrome JS engine (VS) & embedded around the chrome)
	- Express (Ruby side for node)

## Lecture 4

Presentations over git and github.

## Lecture 5

Node.js

- http core module
- require function
- create server
- "If user click here, do this."
- Add to work to the event queue
- Callbacks: Event emitters 
- Node = single threaded
- Demo in class with curl

## Lecture 6

- Went over student links

Express
- Web applicatoin framework written in JS for use in Node.js
- Influenced by Sinata
- Middleware
- Developed web servce in Express: demo

## Lecture 7

Angular JS
- Client-side web application 
- MVC
- Javascript

Core Concepts
- Data bindings
	- Value of HTML tag can be associated with a model object 
- Controllers
	- Modularize web app
- Services
	- Services are created when an Angular app is initialized
- Directives
	- Ubiquitous in Angular
	- Their primary use is to allow Angular to integrate into HTML in a natural way 
- Embeddable
	- Easy to embed a small Angular component into an existing page and then incrementally add new functionality over time 
- Injectable
	- Dependency injection 
	- Controllers and services declare their dependencies up front

Modules
- Primary way to package up a set of controllers into an Angular application

Controllers
-  Declared using the controller function of an Angular module 

## Lecture 8

- Go over angular js app

## Lecture 9

- Javascript
	- Default binding
		- This
			- Don't have to declare it
			- Can't assign a value to it
			- If you assign a property to this in a function, then that property is created in the global context
	- Blocks don't create scope; functions do
- Went through contacts web app

## Lecture 10

- Consumer keys, access tokens
	- Access to Twitter's APIs are secured by OAuth
	- A consumer key identifies a particular application (and developer)
	- An access token identifies a particular user
	- OAuth allows an application to act on behalf of many users

OAuth.Properties 

- First step in accessing Twitter data via the REST, Search, and Streaming APIs is to create a file called oauth.properties
- Single JSON object inside with these properties

# Utilities 
- To sign the request, we have to pass the method, url, params, and our tokens (get, post, put, delete)

## Lecture 11

- Highlights of framework
	- Five REST API endpoints and two Streaming API endpoints 
	- Automatically handles Twitter Rate Limits
	- Provides implementations of the techniques described in Working with Timelines and Working with Cursors
- Understanding framwork
	- Property File with Consumer Key and Access Token
	- URI Escape HTTP Request Parameters
	- Use of SimpleOAuth to create an Authorization Header
	- Use of Typhoeus to create a request and send it
- High level view of framework
- Class hierarchy  
- Twitter Request
	- Standardized Constructor
	- Expects an args hash with up to three entries
		- params: the parameters that go on the request
		- data: the data needed by the request
		- data MUST contain a :props key that points at the location of the properties file
	- log: an instance of a Ruby logger
		- If not supplied, a default one is used
	- Sets the contract required by all sub-classes 
- Contract
	- A TwitterRequest has a public collect method that yields collected data back to its caller
	- Subclasses must provide implementations of:
		- url: the URL of the Twitter endpoint they access
		- request_name: the name used in the log for this request
		- twitter_endpoint: the endpoint used to look up rate limits for this request
		- success: a method that handles the response.body of a successful request
	- Subclasses may provide implementations of:
		- error: a method that handles failed requests; the default prints out information about the failure and then throws a runtime exception
		- authorization, options, make_request, and collect can also be overridden but they must preserve the semantics of the default operations
- Helpers
	- Params and Props
		- Only two new features in the Params helper
		- The ability to control if a parameter is included in a request
		- The ability to display the parameters that are being sent with a request 
	- Logging
		- The logging helper consists of a custom class definition and a method to create a default logger
	- Rates 
		- The Rates helper allows the framework to automatically keep track of rate limits for a given Twitter endpoint
		- If you run out of invocations, it will block your next call and automatically sleep until the current Twitter window is over
		- The default make_request ensures that rates are checked on each request
		- The Rates helper invokes a Twitter endpoint to get the application's current set of rate limits
		- These rates are stored in a class variable so that they are shared across all TwitterRequest instances created by an application
		- These global rates are only refreshed when needed
		- The frameworks features three Request sub-classes
		- MaxIdRequest
			- A subclass for endpoints that need to traverse timelines with the max_id parameter
			-It defines a new contract consisting of:
			- init_condition: set-up a variable to track our progress traversing the timeline
			- condition: check the variable to see if we should continue traversing the timeline
			- update_condition: update the variable after a request has been made and progress on the timeline has occurred
		- CursorRequest
			- CursorRequest is similar to MaxIdRequest
			- However, it does not need to define a contract for subclasses
			- It can implement all of the required functionality directly 
		- StreamingRequest
			- StreamingTwitterRequest is different in that its collect method is designed to run forever
			- We use Typhoeus differently to do a streaming request
				- We create a request and then define a series of event handlers on the request.
				- These handlers get called when appropriate as data streams in 
			- The handlers are:
				- on_headers: The response has started to stream back to us; we can check the headers to make sure everything is okay
				- on_body: Some data has been received from the server; we need to process it
				- on_complete: The response has finished; this can happen if the server decides to terminate the connection
		- One request, RateLimits, is also a direct subclass of TwitterRequest but it's not a new type of request, it just customizes TwitterRequest to hit the rate_limit_status endpoint
	
## Lecture 12

- No SQL
- Web Analytics Application
	- Scaling problems
	- Can't keep up with write demand 
- Types of NoSQL DBs
	- Key value
	- Graphs
	- Columnar
	- Documents

## Lecture 13

- Couch DB
	- Document NoSQL Database
		- Stores docs
		- Each doc contains everythign that might be needed by an app
		- No schema is enforced: each doc can have different attributes 
			- Allows for natural modeling of domains
- CAP Theorem
	- Consistency
	- Availability
	- Partition Tolerance

## Lecture 14

- MongoDB
	- Indexes: B-Trees
	- CAP Theorem
		- Consistency
		- Availability
- Documents order hierarchically 
- Type and case sensitive 

## Lecture 15

- Worked in class over HW questions

## Lecture 16

- Import tweets into MongoDB
	- Construct a program for importing tweets into MongoDB 
	- Assumptions
		- Input file
		- Name of Database: data
		- Name of Collection: tweets
		- Use mongo Ruby gem for accessing MongoDB
	- Get started
		- Create gemfile  
	- Initial version
		- Reads its input file = import.rb 
	- Connecting to Mongo
		- Using the 'mongo' Ruby Gem 
		- Back to import.rb
- Running/Checking MongoDB
	- MongoDB needs to be running
	- mongo --config /usr/local/etc/mongod.conf
	- OR: mongo --dbpath <path to data directory>
	- To launch the mongo client: mongo
- Before We Import 
	- 4 places where created_at can be found on a tweet
		- tweet['created_at']
		- tweet['user']['created_at']
		- tweet['retweeted_status
	
- Perform queries with no indexes 
- Create indexes
- Perform queries with indexes to compare 
- Advanced indexes
	- Compound indexes 

## Lecture 17

- Indexes
	- Can greatly reduce the number of documents that need to be examined to satisfy a query
	- Index Cardinality
	- Number of possible values for an indexed field
	- A field like employment status has low cardinality since it has two values yes/no
	- Whereas name has high carnality
	- In general you only want indexes on high cardinality fields
	- Compound indexes can be difficult
	- Enable different queries: Point Queries: search for a single value, then traverse index (either direction)
	- Multi-Value Queries: search for a range of values
	- Full-Text Indexes
	- Support for a full text search
	- Only one full-text index per collection
	- Geospatial Indexes
	- Cartesian Index
	- Spherical Index: 2Dsphere
	- GeoJSON format
	- Supports points, lines, and polygons 
- MapReduce 

## Lecture 18

- Apache Solr
	- Lucene
	- CU FCQ
	- Solr: RestAPI
- Redis
	- Key value store "Data-structure server"
	- Not a DB replacement
	- Real-time data apps
- Kafka
	- Data in real-time 
	- Distributed
	- Fault-tolerant
	- High-thoughput
	- Publish-subscribe
	- Message system

## Lecture 19

- Kafka demo
- Memcached
	- Distributed memory object caching system
	- Large hash table
	- Data = disposable 
	- Clust is flat
- Document DB (Azure)
	- Schema-free
	- Indexing database

## Lecture 20

- Neo4J
	- Graph based database
	- NoSQL
	- Whiteboard friendly
	- Java based
	- Fast for associative data sets
- HBase
	- Hadoop database 
	- Provides big table capabilities on top of Hadoop
	- Table schema defines only column families
	- Each cell value of the table has a timestamp 

## Lecture 21

- Riak
	- Key value store database
	- NoSQL
	- Written in Erleng
	- No master node
- Cassandra
	- Scaled NoSQL database
	- Always on architecture
	- Fast linear-scale performance
	- Elastic scalability 
	- Rarely fails
- Indexing: Cassandra
	- Insert rows similar to SQL
	- Composite columns with primary key
	- Clustering column sorts the data 
	- Secondary indexes

## Lecture 22

- Javascript Closures and Design Patterns
	- Scope
	- Closure
	- Module design patter
	- Inheritance vs prototype
	- this
- Ruby on Rails
	- Ruby
	- Rails framework
	- Demo
- Flask
	- Python
	- Micro framework

## Lecture 23

- Hadoop
	- Master/slave
	- MapReduce
- Spark
	- Fast Data Sharing
	- MapReduce+
	- Cluster wide caching
- Apache Storm
	- Stream processing
	- Guaranteed message processing

## Lecture 24

- React
	- Released by Facebook 
	- Maintains a virtual DOM
	- One-way state binding
	- JSX
- Flux
	- Single directional data flow
	- Built by facebook to combate scalability of MVC

## Lecture 25

- Google Cloud Platform
	- Support Python, Java, PHP, Go
	- Google handles shading, load balancing, traffic splitting, elasticity
	- 3 tiers of cloud storage 
- Docker
	- Microservice 
	- Containers
- Capistrano
	- Creates custom tasks
	- Automated server deployment 

## Lecture 26

- Turf
	- GeoJSON
	- Analysis
- Javascript InfoVis Toolkit
	- Library to create interactive data visualization on the web
	- Composeable 
	- Data stored in static JSON objects
- Flask
	- BSD
	- Extendable

## Lecture 27

- D3
	- select
	- bind
- Leaflet
	- Layering
	- Multiplatform
	- Call maps

## Lecture 28

- AWS
	- Server
- Javascript Async and Promises
	- Event loop
	- Callback
	- Promises
		- Chain
- More student presentations

