# Representational state transfer (REST)

A way of using HTTP verbs (POST, GET, PUT, DELETE) to provide a standardized Web API to remote data.

Data is thought of in terms of collections and items.

Only a set of guidelines, not a strict protocol.

## GET

Either gets one item by ID or lists all items in a collection.

`GET /cats`: returns a list of all cats

`GET /cats/3`: returns the cat with the ID of 3

## POST

Create a new entry in a collection.

`POST /cats`: the parameters passed will be used to create a new cat

`POST /cats/1`: Doesn't do anything, unless cats is a collection of other objects.

## PUT

Replace any data at the endpoint with a new set of data.

`PUT /cats/`: Would take a list of cats and replace all cats with that list (probably a bad idea)

`PUT /cats/3`: Would take new data for the cat with the ID of 3 and update the existing cat using that data

## DELETE

Deletes a collection or an item in a collection.

`DELETE /cats/`: Would delete all cats (a terrible idea!)

`DELETE /cats/3`: Would delete the cat with the ID of 3

**Note**: Deleting doesn't actually mean you have to delete the object.  One way you can "delete" an object is by setting a `deleted` field in the database row to 1, and never return any results where `deleted` is true.

# Return Format

The data remains the same no matter whether the request is by a user looking at a website or by AJAX code.

Though "AJAX" stands for "Asynchronous JavaScript and XML", we almost always return JSON instead of XML.

You can detect whether or not the request is from a user or from your JavaScript code by checking for `request.xhr?` in Sinatra and Rails.

If it's a JavaScript request, we can return JSON to our code so that we can handle the data and return something to the user.

# Return Formats

## HTML Page

What we've already been doing.

## JSON

A data format for serializing data from our database.  Native JSON, very easy format, super popular.

  [
		{'id':15, 'name':'Meowseph', 'breed':'awesome'},
		{'id':12, 'name':'Cat', 'breed':''}
	]

This allows us to manipulate our page based on the data.

## HTML Partial

Only the portion of the page that has new data, we can replace the old portion of the page with the new.

The benefit of this approach is that we don't have to write HTML code in JavaScript to restructure the JSON data on the page.  That code should already be in backend, which means you would have to recode the template layer twice.

## Good Use of JSON

You can use JSON for things like errors.  Instead of writing form validation on the client-side, you can pass the data to the server, which will return a JSON array of errors if the data isn't valid and then render that list of errors on the client-side.

This saves you from having to write form validation code twice (once on the browser, once on the server).
