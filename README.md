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


