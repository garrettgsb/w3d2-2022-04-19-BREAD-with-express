# BREAD With Express

## Okay, so you've written a bunch of Javascript... How's somebody going to use it?

  So you have a bunch of interesting Javascript behavior. That's great! But you don't have an app yet: There must be some way for the outside world to interact with it, without modifying your source code, in order for it to be an application. That means you need:

  a) A plan for getting information in
  b) A plan for getting information out

  **Analogy: Command line interfaces**

  One interface that you've learned about is the command line: A user (human or machine) can use your program by passing arguments after the filename. They never have to read your code: They simply learn what arguments can be passed in to achieve what effect, and use the program productively.

  Do you have a plan for:

  * Getting information in? **Yes!** The command line arguments in `process.argv`
  * Getting information out? **Yes!** The terminal output (STDOUT, or standard out)

  **HTTP interfaces**

  An HTTP interface is similar: You can set up a server to listen for HTTP requests, then using HTTP endpoints (URLs), a human or machine user can specify what they want via an HTTP request (instead of, for example, a terminal command). Then, the server can send back a response: A web page, some data, or an instruction of some sort (e.g. to redirect to another endpoint).

    Do you have a plan for:

  * Getting information in? **Yes!** The URL itself, and any data sent along with the HTTP request
  * Getting information out? **Yes!** The HTTP response

## Usually you want your apps to do BREAD stuff to Resources.

  ### So what's BREAD?

  B - Browse - Show some representation of a **collection**
  R - Read - Show some representation of a specific **entry** in a collection
  E - Edit - Modify a specific **entry** in a collection
  A - Add - Create a new entry in a **collection**
  D - Delete - Remove a specific **entry** from a collection

  ### What's a resource?

  Your resources tend to be the "nouns" in your app: You might think of them as different variations on the concept of "Users" (representations of people/agents) and "Posts" (things that Users create). Although that's a vast simplification, it has significant explanatory power-- Many things are just a type of Post:

  * Pin - Post, but it's an image
  * Gram - Post, but it's an image
  * Classified ad - Post, specifically for buying/selling/dating/etc. something
  * Tweet - Post, but 280 characters (or something)
  * Article, message, etc.: Many things map onto this "post" concept straightforwardly

  ### REST: Doing BREAD stuff to resources

  So given that many apps can be thought of as simply combining two well-known patterns (i.e. Doing BREAD stuff to Resources), we can often apply one common routing convention to do most of our routing (using a `users` resource as an example):

  Browse - `GET /users`
  Read   - `GET /users/:id`
  Edit   - `POST /users/:id`
  Add    - `POST /users`
  Delete - `POST /users/:id/delete` (or `DELETE /users/:id` if available)

## Notes from Lecture

This section is an aggregation of some of the comments that appear in the source code files.

### Query string params:

  Query string params are used when you make a GET request with a form that has named fields, and Express exposes these to you in `request.query`. If it's a POST request instead, the field values will appear in `request.body` and you won't see them in the URL.

  Example: http://localhost:8080/set?newCounterValue=55555&someOtherValue=hello

  `?` -> Start the query string params (end the "path" part of the URL)
  `newCounterValue` -> The key that shows up in `request.query`
  `55555` -> The value that the user (presumably) typed into the form
  `&` -> Separates key-value pairs

  (So `someOtherValue` will be a second key, with `hello` as the second value)

### Three places to look for your "stuff":
  * `request.params` -> URL params (e.g. /users/:id) - :id is the param
  * `request.query` -> Form data from a GET request (Query string params)
  * `request.body` -> Form data from a POST request

  `/users/1`
  `/users/:id` will appear in Express as `request.params.id` with a value of  `'1'`


## What's a Resource?

**Examples:**

* Products
* Articles
* Tweets
* Users
* Admins
* Todos
* Playlists
* Songs
* Classifieds

Resources can be thought of as just different variations of "Users" or "Posts" (as described above).

## What's a BREAD action?

BREAD is similar to CRUD
CRUD - Create, Read, Update, Delete

Most interface actions (e.g. HTTP endpoints, command line commands, buttons you can click) perform some BREAD action.

B - Browse - Look at a whole collection
R - Read - Look at a specific entry in a collection
E - Edit - Change an entry
A - Add - Add an entry to a collection
D - Delete - Remove an entry from a collection

If you know:
* What the resources are
* That you want to do BREAD stuff to them

...Then you can map those to a common routing convention (often called "RESTful routing") without thinking too hard about it! (As described above in the **REST: Doing BREAD stuff to resources** section)


### Why do we (...I) prefer BREAD for talking about web interface routing?
  * CRUD sounds gross
  * CRUD doesn't have the "B"
