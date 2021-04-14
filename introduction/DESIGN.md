# The Plan

## Our Library

We are going to build a very simple library application.
* We can buy new books and add them to the libraries collection,
* A user can log into the system
* While a book is in our collection a logged in user can borrow it.
* A  user can return a book they have borrowed (even if they aren't logged in)
* A logged in user can log out.
* We can remove old books from the collection when they're too old.
* When logging in the system will fetch the details of the user.
* When the call takes to long the user can cancel it.
* If something goes wrong an error can be raised
* When the user acknowledges an error it can be cleared.

## Library data model

Our basic data structure is as follows.

``` mermaid
classDiagram

Library *-- Book
Library *-- CurrentUser
Library: Book[] books
Library: CurrentUser currentUser
Library: String[] errors
Library: String[] users
Library: boolean apiFetching
Library: apiCancel()
Library: apiFetch()
Library: collectionAdd()
Library: collectionRemove()
Library: errorAdd()
Library: errorClear()
Library: usersClear()
Library: usersUpdate()
Book: String title
Book: String author
Book: Date borrowed
Book: Date borrower
Book: bookBorrow()
Book: bookReturn()
CurrentUser: String fullName
CurrentUser: String id
CurrentUser: URL photo
CurrentUser: logOff()
CurrentUser: logOn()
```

## The screens

### Welcome

Viewed when the user is not logged in.

<table border="2">
	<tr><th colspan="2">Welcome</th></tr>
	<tr><td><b>User ID</b></td><td>Please select...<br/><i>Dropdown Box of users from randomme API</i></td>
	<tr><td></td><td>Submit<br/><i>Button to submit the page</i></td></tr>
</table>

### Catalog

Default route when logged in

<table border="2">
	<tr><th>Catalog</th></tr>
	<tr><td>
		<table border="2">
			<tr>
				<td><b>Author</b><br/><i>Sortable column</i></td>
				<td><b>Title</b><br/><i>Sortable column</i></td>
				<td><b>Lent on</b><br/><i>Sortable column,<br/>Admin only</i></td>
				<td><b>Lent to</b><br/><i>Sortable column,<br/>Admin only</i></td>
				<td><b>Actions</b></td>
				<td></td>
			</tr>
			<tr>
				<td><i>Text</i></td>
				<td><i>Text</i></td>
				<td><i>Text</i></td>
				<td><i>Text</i></td>
				<td><i>Borrow Icon if not on loan.<br/>Return Icon if on loan<br/>Trash icon if admin</i></td>
				<td><i>Details for each book.<br/>All books shown for an admin.<br/>Only non Loaned books and books loaned to current user shown for non-admin.</i></td>
		</tr>
	</table>
	<i>Table</i>
	</td></tr>
		<tr>
			<td><b>Add</b><br/><i>Button<br/>Only visible for admin</i></td>
	</tr>
	<tr><td>Collection Icon | My Books Icon | Log off Icon<br/><i>Navigation Panel</i></td></tr>
</table>

### My books

<table border="2">
	<tr><th>My books</th></tr>
	<tr><td>
		<table border="2">
			<tr>
				<td><b>Author</b><br/><i>Sortable column</i></td>
				<td><b>Title</b><br/><i>Sortable column</i></td>
				<td><b>Actions</b></td>
				<td></td>
			</tr>
			<tr>
				<td><i>Text</i></td>
				<td><i>Text</i></td>
				<td>Return Icon</td>
				<td><i>Details for each book.<br/>Only books loaned to current user shown.</i>		
			</td>
		</tr>
	</table>
	<i>Table</i>
	</td></tr>
	<tr><td>Collection Icon | My Books Icon | Log off Icon<br/><i>Navigation Panel</i></td></tr>
</table>


### Add a book screen

<table border="2">
	<tr><th colspan="2">Add a book</th></tr>
	<tr><td><b>Title</b></td><td><i>Inline Text Box</i></td>
	<tr><td><b>Author</b></td><td><i>Inline Text Box</i></td>
	<tr><td></td><td>Submit<br/><i>Button to submit the page</i></td></tr>
</table>

## The "randomuser" API

The randomuser API is a free to use REST API which provides dummy user data.
This diagram represents the fields we will be using from the randomuser API.
This [example](https://randomuser.me/api/1.3/?results=2&inc=name,picture,email&noinfo&seed=learning-app-library&format=yaml) will display this data for 2 users in YAML format for easier reading, however we will use the JSON version of the API.

``` mermaid
classDiagram

API *-- Result
Result *-- Name
Result *-- Picture
API: Result[] results
Result: API_Name name
Result: String email
Result: Picture picture
Name: String title
Name: String first
Name: String last
Picture: URL large
Picture: URL medium
Picture: URL thumbnail
```

| Object  | Field     | Type   | Description |
| ------- | --------- | ------ | --- |
| Results | email     | String | The user's email address, used as an ID. |
| Name    | title     | String | The users title. |
| Name    | first     | String | The users first name. |
| Name    | last      | String | The users last name. |
| Picture | large     | URL    | A link the the large version of the users photo. |
| Picture | medium    | URL    | A link to the medium version of the users photo. |
| Picture | thumbnail | URL    | A lnk the the small version of the users photo. |
