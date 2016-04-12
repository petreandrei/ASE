# ASE
http://plnkr.co/edit/gjXyP0eb6c2eLASt9bke

EDIT: daca aveti nevoie de ceva, shoot a message @ andrei.petre@qualitance.com

![alt tag](https://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/AngularJS_logo.svg/695px-AngularJS_logo.svg.png)


Angular - client side js framework for adding interactivity to our html

Modules - what defines the angular app, where we define dependencies. 
The very first piece of code that we write in an angular app is the module.

ng-app  directive creates an angular application by running the module found by name when the document loads. 
So the very first piece of code that we will write in an angular app is 
var app = angular.module('demo', []);
The name doesn't have to be demo, it can be w/e. But make sure to match it with the ng-app="" in your html. 
That array is the list of dependencies for our module, we will add ui.router later.

The module is empty for now, but just including that, our html will be treated as an angular app
and this means we can start writing expressions.
Expressions are how we insert dynamic values in our html.

I am {{4+6}} => ? angular expressions are wrapped in {{ }} . the content from inside will be evaluated by Angular.
You will use expressions to get the data from controller to the view. 

We need to tell our html when to trigger some JS code. 
In angular we add behaviour to our HTML with directives (ng-click, ng-repeat, ng-app, ng-controller, all those are build in Angular directives). 
directive - a marker on html that tells angular to run or reference some js code — later we will be teaching our html new tricks by building our own directive.

========================================

Controllers - help us get our data into our page.
Controllers are where we define our app’s behaviour by defining functions and values.
The code from the anonymous func will get executed when our ctrl is loaded.

Now let’s add an object to our js file. we need to bind this to our ctrl.
Bind the object to scope. Now we need to figure how to access it. In our html
add the ng-controller directive.

But what would happen if we would try to access our obj from outside our ctrl div?
Well it wouldn’t work, because the scope of the ctrl can be accessed only in that div.

Lets add a bootstrap card for our movie. and a Buy ticket button.
Lets only show our button if we are not soldout -> use ng-show directive.

Lets add more movies
Our movie on scope becomes an array. How are we going to display all this data? maybe a directive?

We can show all the movies data by adding the movie index, like movies[0].name, movies[1].name ...
but this is not dynamic, too much repeated code.

lets use a directive to iterate through each item-> we’ll use the ng-repeat directive.

==========================================================
Recap:

Directives - html  attributes that trigger some js behaviour
Modules - Where our application components live
Controllers - Where we add application behaviour
Expressions - How values get displayed in the web page

ng-app - creates an angular application by running the module found by name
ng-controller - attach the ctrl function to a section of our html
ng-show/ng-hide - display or hide a section based on a expression
ng-repeat - repeat a section for each item in an Array

==========================================================
Take a look at filters. You can sort the list of movies by adding orderBy filter to the ng-repeat syntax.
ng-repeat="movie in movies | orderBy: '-title'". This will order the movies in your ng-repeat in descending order.
You can use any property on the object: description, title, likes etc for filtering.
Filters definition: Selects a set of items from array and returns it as a new array. (orderBy for ex)

implement ng-click for likes

what you are starting to see here is some angular magic. when we click like, we increment movie.like on the movie object,
and the value is being automatically updated in the view. This concept is called two way data binding
this means that expressions are re evaluated each time a property on the scope is being changed.

==========================================================

Services 

** In our app we only used built in services provided by Angular, like $scope, $http, $state, $stateParams.
we need to tell angular what services it needs, by injecting them.
this way our controller tells the injector ( when i run i need these services) 
and so when the controller gets activated, the injector provides us with our services that we required.
that’s called dependency injection.

But in Angular, you can build your own services. As you can probably see, in our controllers we have some duplicated code

app.controller('MoviesController', function($scope, $http, $state) {
  $http.get('movies.json').then(function (result) {
    $scope.movies = result.data.movies;
  });
});

app.controller('TrailerController', function($scope, $http, $stateParams) {
  $scope.id = $stateParams.id;
  $http.get('movies.json').then(function (result) {
    $scope.movies = result.data.movies;
  });
});

** They look pretty similar, right? Well, for extra points, read this: 
In AngularJS, controllers can sometimes become structures of mixed business($http requests for example) and view logic, as it’s all too easy to house anything you need for the view inside the controller. It’s convenient, and it just plain works… until your application grows in complexity or needs unit tests. Controllers should not be responsible for anything else than making the data available in our view. They should not care about things like making $http requests. Instead, the bussines logic($http requests) should be moved to Services, for more reusability and maintainability (less lines of code per file).

So why should we move the $http calls to a service?
In short, separation of concerns. Ideally, everything from services, to controllers, to directives, and more should be skinny, and achieving this is very possible in AngularJS. Each part should have a single responsibility and the controller’s responsibility should be to communicate between services(in our case get the data from a json file, or a web server) and make it available in the view (by attaching it to $scope).

For extra points, move the $http requests to a service. See angular docs or examples on StackOverflow for creating a service. Also, instead of making the same http call in both controllers, you can try to pass the needed object between controllers. So when you click 'Go to trailer', try to pass the whole movie object (not the movies array, the movie object from ng-repeat) to the TrailerController. To do this, look up for "communicate between controllers in Angular"

Wish you guys the best of luck!
==========================================================
