# Lecture Notes for Data Engineering in Spring 2015

## Lecture 1: 01/13/15

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

## Lecture 2: 01/15/15

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

## Lecture 3: 01/20/15

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

## Lecture 4: 01/22/15

Presentations over git and github.

## Lecture 5: 01/27/15

Node.js

- http core module
- require function
- create server
- "If user click here, do this."
- Add to work to the event queue
- Callbacks: Event emitters 
- Node = single threaded
- Demo in class with curl

## Lecture 6: 01/29/15
- Went over student links

Express
- Web applicatoin framework written in JS for use in Node.js
- Influenced by Sinata
- Middleware
- Developed web servce in Express: demo

## Lecture 7: 02/03/15
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

## Lecture 8: 02/05/15
- Go over angular js app

## Lecture 9: 02/10/15
- Javascript
	- Default binding
		- This
			- Don't have to declare it
			- Can't assign a value to it
			- If you assign a property to this in a function, then that property is created in the global context
	- Blocks don't create scope; functions do
- Went through contacts web app

## Lecture 10: 02/12/15
- Consumer keys, access tokens
	- Access to Twitter's APIs are secured by OAuth
	- A consumer key identifies a particular application (and developer)
	- An access token identifies a particular user
	- OAuth allows an application to act on behalf of many users

# OAuth.Properties 
- First step in accessing Twitter data via the REST, Search, and Streaming APIs is to create a file called oauth.properties
- Single JSON object inside with these properties

# Utilities 
- To sign the request, we have to pass the method, url, params, and our tokens (get, post, put, delete)

