# Chapter 2: State, Actions and Reducers

1. Inside `.\library\src`, create a folder `store`
	> This directory will hold everything related to your data model (the redux parts)
3. Inside `.library\src\store`, create a file `initialState.json` with the following content:
	``` json
	{
		"books": [
			{ "title": "Little Women",        "author": "Alcott, Louisa May",	"borrowed": null, "borrower": null },
			{ "title": "The Foundation"       "author": "Asimov, Isaac",		"borrowed": null, "borrower": null },
			{ "title": "Pride and Prejudice", "author": "Austen, Jane",         "borrowed": null, "borrower": null },
			{ "title": "Jane Eyre",           "author": "Bronte, Charlotte",	"borrowed": null, "borrower": null },
			{ "title": "Wuthering Heights",   "author": "Brontë, Emily",		"borrowed": null, "borrower": null },
			{ "title": "Robison Crusoe",      "author": "Defoe, Daniel",		"borrowed": null, "borrower": null },
			{ "title": "The Great Gatsby",    "author": "Fitzgerald, F. Scott",	"borrowed": null, "borrower": null },
			{ "title": "Moby Dick",           "author": "Melville, Herman",		"borrowed": null, "borrower": null },
			{ "title": "Merchant of Venice",  "author": "Shakespeare, William", "borrowed": null, "borrower": null },
			{ "title": "Frankenstein",        "author": "Shelley, Mary",		"borrowed": null, "borrower": null }
			
		],
		"currentUser": null,
		"errors": [ "Totally expected error" ],
		"users": [],
		"apiFetching": false
	}
	```
	> This file (`.\library\src\store\initialState,json`) contains the default initial state for your library, ie what the user will see when they access the application for the first time.
	> * `/` is a JSON object (a JSON file can only contain one element at top level)
	> * The  `/books` property contains an array of books.
	> * The `/books[n]` item contains an object
	> * The `/books[n]/title` property contains the title of the book
	> * The `/books[n]/author` property contains the name of the book's author
	> * The `/books[n]/borrowed` property will contain the date the book was last borrowed
	> * The `/books[n]/borrower` property will contain the user who borrowed the book last
	> * The `/currentUser` property will contain the email address of the current user.
	> * The `/errors` property contains an array of errors
	> * The `/errors[n]` item contains an error message string
	> * The `/users` property contains the list of users returned by the API.
	> * The `/users[n]` item contains the details of a retrieved user.
	> * The `/apiFetching` property contains the boolean of whether an API call is in progress.

4. Inside `.\library\src\store`, create a folder `actions`
5. Inside `.library\src\store\actions`, create a file `actions.js` with the following content:
	``` js
	const actions = {
		BOOK_BORROW: "book_borrow: a user borrows a book from the collection",
		BOOK_RETURN: "book_return: a user returns a book they borrowed",
		COLLECTION_ADD: "collection_add: add a new book to the libraries collection",
		COLLECTION_REMOVE: "collection_remove: a book is removed from the libraries collection",
		ERROR_ADD: "error_add: raise a new error message",
		ERROR_CLEAR: "error_clear: clear an error message",
		LOG_OFF: "log_off: a user logs off",
		LOG_ON: "log_on: a user logs on",
		API_CANCEL: "api_cancel: user cancels an api call",
		API_FETCH: "api_fetch: an api call is initiated",
		USERS_CLEAR: "users_clear",
		USERS_UPDATE: "users_update"
	}
	export default actions
	```
	> This file provides an [enumeration](https://www.w3schools.com/java/java_enums.asp) of actions that we can perform against the data, when declaring it:
	> * By using a reference list we can avoid typos, as references to an object property that doesn't exist (eg `actions.USER_UPDATE` would fail as it is USERS not USER) will error,
	> * We use a `const` (constant) declaration to ensure that the `actions` object cannot be edited, this means we cannot accidentally overwrite it.
	> * Both the name and value of each property **must** be unique, however beyond it's uniqueness the value does not matter. As good practice I recommend that:
	> 	* Use the value of each property provide a brief description of the action in the value, for later reference and easier maintenance,
	> 	* Repeat the name of the property at the start of each value to ensure uniqueness.
	> 	* Keep the actions in alphabetical order, to prevent duplication.
	>
	> The `export default actions` makes the actions object available from other parts of your code.
