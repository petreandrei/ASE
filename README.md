# ASE
http://plnkr.co/edit/gjXyP0eb6c2eLASt9bke

Angular - client side js framework for adding interactivity to our html

Modules - what defines the angular app, where we define dependencies. 
The very first piece of code that we write in an angular app is the module.

ng-app  directive creates an angular application by running the module found by name when the document loads. 
The module is empty for now, but just including that, our html will be treated as an angular app
and this means we can start writing expressions

Expressions are how we insert dynamic values in our html.

I am {{4+6}} => ?

We need to tell our html when to trigger some JS code. 
In angular we add behaviour to our HTML with directives. 
directive - a marker on html that tells angular to run or reference some js code — later we will be teaching our html new tricks 

========================================

Controllers - help us get our data into our page.
Controllers are where we define our app’s behaviour by defining functions and values.
The code from the anonymous func will get executed when our ctrl is loaded.

Now let’s add an object to our js file. we need to bind this to our ctrl.
Bind the object to scope. Now we need to figure how to access it in our html
add the ng-controller directive

But what would happen if we would try to access our obj from outside our ctrl div?
Well it wouldn’t work, because the scope of the ctrl can be accessed only in that div.

Lets add a bootstrap card for our movie. and a Buy ticket button.
Lets only show our button if we are not soldout -> use ng-show directive.

Lets add more movies
Our movie on scope becomes an array. How are we going to display all this data? maybe a directive?

We can show all the movies data by adding the movie index, like movies[0].name, movies[1].name ...
but this is not dynamic, too much repeated code.

lets use a directive to iterate through each item-> we’ll use the ng-repeat directive

==========================================================

recap

Directives - html  attributes that trigger some js behaviour
Modules - Where our application components live
Controllers - Where we add application behaviour
Expressions - How values get displayed in the web page

ng-app - creates an angular application by running the module found by name
ng-controller - attach the ctrl function to a section of our html
ng-show/ng-hide - display or hide a section based on a expression
ng-repeat - repeat a section for each item in an Array

==========================================================

Filters - movie in movies | orderBy: '-title'" 
Selects a set of items from array and returns it as a new array. (orderBy for ex)

ng-click for likes

what you are starting to see here is some angular magic. when we click like, we increment movie.like on the movie object,
and the value is being automatically updated in the view. This concept is called two way data binding
this means that expressions are re evaluated each time a property on the scope is being changed.


Services - log messages to our console with $log
	      - fetch son data fro ma web server with $http - this will return a promise
		a promise allows you to do callbacks on it, like .success()

we need to tell angular what services it needs, let’s inject them
this way our controller tells the injector ( when i run i need these services) 
and so when the controller gets activated, the injector provides us with our services that we required
that’s called dependency injection

this http req might take a second, but our page isn’t going to wait for it to finish, because http calls are async
