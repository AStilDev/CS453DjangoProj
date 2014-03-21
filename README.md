BookRental
==========

Django application to service as a computer science book rental system.


<b>SQL to Django Queries:</b>

<p>info page, displays the user's usersname and password</p>

<u>SQL:</u><br>
SELECT username, password<br>
FROM login<br>

<u>Django:</u><br>
Login.object.filter(username, password)

<p>Books page, displays a table of book titles</p>

<u>SQL:</u><br>
SELECT title<br>
FROM Book<br>

<u>Django:</u><br>
Book.object.filter(title)

<p>Login page, displays the name of the user</p>

<u>SQL:</u><br>
SELECT name<br>
FROM  login<br>
WHERE name = John <br>

<u>Django:</u><br>
Logins.object.filter(name_iexact="John")

<p>Returns page, gets the isbn that the user needs to return</p>

<u>SQL:</u><br>
SELECT isbn<br>
FROM returns,login<br>
WHERE returns.isbn = cart.isbn <br>

<u>Django:</u><br>
Returns.object.filter(Login__cart_isbn=1234)

<p>Returns page, displays table </p>

<u>SQL:</u><br>
SELECT isbn<br>
FROM returns,login<br>
WHERE returns.isbn = cart.isbn <br>

<u>Django:</u><br>
Returns.object.filter(Login__username)


Display the current user's full name at the top of each page after logging in (ex. cart page).

<u>SQL:</u><br>
SELECT name<br>
FROM Cart

<u>Django:</u><br>
Cart.objects.get(name)

<b>On the cart page, display a table of the isbns, prices, and quantities of books a user wishes to checkout.</b>

<u>SQL:</u><br>
SELECT isbn, title, quantity, price<br>
FROM Cart, Book<br>
WHERE Cart.isbn = Book.isbn

<u>Django:</u><br>
Cart.objects.get(isbn)<br>
Cart.objects.get(book__isbn__title)<br>
Cart.objects.get(quantity)<br>
Cart.objects.get(price)

<b>On the checkout page, display the user's name, email, phone number, and returndate as a table.</b>

<u>SQL:</u><br>
SELECT username, name, email, phone, returndate<br>
FROM Returns, Login<br>
WHERE Returns.username = Login.username

<u>Django:</u><br>
Returns.objects.get(login__username__name)<br>
Returns.objects.get(login__username__email)<br>
Returns.objects.get(login__username__phone)<br>
Returns.objects.get(returndate)


<b>On the return page, display the user's name and email in addition to book titles, quantities, and the return date.</b>

<u>SQL:</u><br>
SELECT name, email, title, quantity, returndate<br>
FROM Login, Book, Cart, Returns<br>
WHERE Login.username = Returns.username<br>
  ^ Returns.isbn = Book.isbn<br>
  ^ Returns.username = Cart.username
  
<u>Django:</u><br>
Returns.objects.get(login__username__name)<br>
Returns.objects.get(login__username__email)<br>
Returns.objects.get(login__username__phone)<br>
Returns.objects.get(book__isbn__title)<br>
Returns.objects.get(cart__username__quantity)<br>
Returns.objects.get(returndate)
