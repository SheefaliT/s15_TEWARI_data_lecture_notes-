# Lecture Notes for Data Engineering in Spring 2015

## Lecture 1: 01/13/15

- Created a repository for writing notes.
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
		○ /users/0/possessions (possessions owned by user 0)
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
		○ Sinatra (handling HTTP request)
		○ Rspec (testing)
		○ Typhoeus (Ruby library to do HTTP request on client side)
		○ Node (wrapper around chrome JS engine (VS) & embedded around the chrome)
		○ Express (Ruby side for node)
		
