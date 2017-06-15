Table of Contents:
1. Adding angular 
2. directives
3. ng-controller
4. 

Adding angular
```
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
```
Adding angular animate
```
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular-animate.js"></script>

```
Adding angular route
```
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular-route.js"></script>
```
---
Directives

**ng-app** directive tells AngularJS that the <div> element is the "owner" of an AngularJS application.

**ng-model** directive binds the value of the input field to the application variable name.

**ng-bind** directive binds the innerHTML of the <p> element to the application variable name.

**ng-show** and **ng-hide**  directives show or hide and element. This is achieved by setting styles in the site’s CSS.

**ng-class** directive allows class attributes to be dynamically loaded.

**ng-animate** directive provides support for animation, including Javascript, CSS3 transitions, and CSS3 keyframe animations.

**ng-disabled** directive binds AngularJS application data to the disabled attribute of HTML elements.

Events

**
ng-blur
ng-change
ng-click
ng-copy
ng-cut
ng-dblclick
ng-focus
ng-keydown
ng-keypress
ng-keyup
ng-mousedown
ng-mouseenter
ng-mouseleave
ng-mousemove
ng-mouseover
ng-mouseup
ng-paste
**


```
<!DOCTYPE html>
<html>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
<body>
<div ng-app="">
  <p>Name: <input type="text" ng-model="name"></p>
  <p ng-bind="name"></p>
</div>

</body>
</html>
```

The ng-init directive initializes AngularJS application variables.
```
<div data-ng-app="" data-ng-init="firstName='Ayesha'">
<p>The name is <span data-ng-bind="firstName"></span></p>
</div>
```
---
Setters:
```javascript
angular.module('app', []);
```
Getters:
```
angular.module('app');
```
---
HTML Bootstrapping
```
<html ng-app="app">
  <head></head>
  <body></body>
</html>
```
---
$scope -- two way data-binding cycles
```javascript
$scope.someValue = 'Hello';                 //javascipt
```
```
<div ng-controller="AppCtrl">               <!--markup-->
  {{ someValue }}
</div>
```
---

ng-controller

<p>angular js directive that defines the controller. right side of the controller is the name of the javascript function it is referencing</p>

---

scope

In case of array of scope variable
  ```
 <li ng-repeat="x in names">{{x}}</li>           markup
 $scope.names = ["Emil", "Tobias", "Linus"];     javascript
```
---
 AngularJS Filters
 
 Filters can be added to expressions by using the pipe character |, followed by a filter.

currency Format a number to a currency format.
date Format a date to a specified format.
filter Select a subset of items from an array.
json Format an object to a JSON string.
limitTo Limits an array/string, into a specified number of elements/characters.
lowercase Format a string to lower case.
number Format a number to a string.
orderBy Orders an array by an expression.
uppercase Format a string to upper case.

Example: orderBy
By adding the ng-click directive on the table headers, we can run a function that changes the sorting order of the array:

```
<div ng-app="myApp" ng-controller="namesCtrl">

<table border="1" width="100%">
  <tr>
    <th ng-click="orderByMe('name')">Name</th>
    <th ng-click="orderByMe('country')">Country</th>
  </tr>
  <tr ng-repeat="x in names | orderBy:myOrderBy">
    <td>{{x.name}}</td>
    <td>{{x.country}}</td>
  </tr>
</table>

</div>

<script>
angular.module('myApp', []).controller('namesCtrl', function($scope) {
  $scope.names = [
    {name:'Jani',country:'Norway'},
    {name:'Carl',country:'Sweden'},
    {name:'Margareth',country:'England'},
    {name:'Hege',country:'Norway'},
    {name:'Joe',country:'Denmark'},
    {name:'Gustav',country:'Sweden'},
    {name:'Birgit',country:'Denmark'},
    {name:'Mary',country:'England'},
    {name:'Kai',country:'Norway'}
  ];
  $scope.orderByMe = function(x) {
    $scope.myOrderBy = x;
  }
});
</script>
```
---
<h2>Services</h2>

In order to use the service in the controller, it must be defined as a dependency.

Location Service
```
var app = angular.module('myApp', []);
app.controller('customersCtrl', function($scope, $location) {
    $scope.myUrl = $location.absUrl();
});
```
http Service
```
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $http) {
    $http.get("welcome.htm").then(function (response) {
        $scope.myWelcome = response.data;
    });
});
```
Timeout Service
```
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $timeout) {
    $scope.myHeader = "Hello World!";
    $timeout(function () {
        $scope.myHeader = "How are you today?";
    }, 2000);
});
```
Interval Service
```
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $interval) {
    $scope.theTime = new Date().toLocaleTimeString();
    $interval(function () {
        $scope.theTime = new Date().toLocaleTimeString();
    }, 1000);
});
```

Service with a pipe

```
<!DOCTYPE html>
<html>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
<body>

<div ng-app="myApp" ng-controller="namesCtrl">
    
    <ul >
<li ng-repeat="x in counts">{{x | myFormat}}</li>
</ul>
</div>

<script>
    var app = angular.module('myApp', []);   
    app.service('hexafy', function() {
    this.myFunc = function (x) {
        return x.toString(16);
    }
    });
    app.controller('namesCtrl', function($scope) {
        $scope.counts =[35,45,777];
    });
    app.filter('myFormat',['hexafy', function(hexafy) {
        return function(x) {
            return hexafy.myFunc(x);
        };
       }]); 
   
</script>

</body>
</html>
```
Accessing $http properties

```
app.controller('myCtrl', function($scope, $http) {
  $http.get("welcome.htm")                                -.delete(),.get(),.head(),.jsonp(),.patch(),.post(),.put()  .then(function(response) {
      $scope.content = response.data;
      $scope.statuscode = response.status;
      $scope.statustext = response.statusText;            
  });
});
```
http and JSON

```
<body>

<div ng-app="myApp" ng-controller="customersCtrl"> 

<ul>
  <li ng-repeat="x in myData">
    {{ x.Name + ', ' + x.Country }}
  </li>
</ul>

</div>

<script>
var app = angular.module('myApp', []);
app.controller('customersCtrl', function($scope, $http) {
  $http.get("customers.php").then(function (response) {
      $scope.myData = response.data.records;
  });
});
</script>

</body>

```
Angular Tables

Using ng-repeat directive and ng-if with $odd and $even we change the styles for alternating rows 
```

<table>
  <tr ng-repeat="x in names">
    <td ng-if="$odd" style="background-color:#DDA0DD">
    {{ x.Name }}</td>
    <td ng-if="$even">
    {{ x.Name }}</td>
    <td ng-if="$odd" style="background-color:#DDA0DD">
    {{ x.Country }}</td>
    <td ng-if="$even">
    {{ x.Country }}</td>
  </tr>
</table>
```
AngularJS Select Boxes

Dropdowns made with ng-options allows the selected value to be an object, while dropdowns made from ng-repeat has to be a string
Using ng-options
```javascript
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.cars = {
        car01 : "Ford",
        car02 : "Fiat",
        car03 : "Volvo"
    }
});
```
```
<select ng-model="selectedCar" ng-options="y for (x, y) in cars">
</select>

<h1>You selected: {{selectedCar}}</h1>
```
Using ng-repeat
```
<select>
<option ng-repeat="x in names">{{x}}</option>
</select>
```

AngularJS and DB and PHP

```php
<?php
header("Access-Control-Allow-Origin: *");
header("Content-Type: application/json; charset=UTF-8");

$conn = new mysqli("myServer", "myUser", "myPassword", "Northwind");

$result = $conn->query("SELECT CompanyName, City, Country FROM Customers");

$outp = "";
while($rs = $result->fetch_array(MYSQLI_ASSOC)) {
    if ($outp != "") {$outp .= ",";}
    $outp .= '{"Name":"'  . $rs["CompanyName"] . '",';
    $outp .= '"City":"'   . $rs["City"]        . '",';
    $outp .= '"Country":"'. $rs["Country"]     . '"}';
}
$outp ='{"records":['.$outp.']}';
$conn->close();

echo($outp);
?>
```
```
<div ng-app="myApp" ng-controller="customersCtrl">

<table>
  <tr ng-repeat="x in names">
    <td>{{ x.Name }}</td>
    <td>{{ x.Country }}</td>
  </tr>
</table>

</div>

<script>
var app = angular.module('myApp', []);
app.controller('customersCtrl', function($scope, $http) {
    $http.get("customers_mysql.php")
    .then(function (response) {$scope.names = response.data.records;});
});
</script>
```

Angular bind
If there are more than one angular apps directive. angular js only binds one automatically and the other has to be binded manually using angular.bootstrap along with id
```javascript
angular.bootstrap(myDiv2, ["MyModuleB"]);
```

Angular Include

```
<div ng-include="'myFile.htm'"></div>
```

Form validation

Input fields have the following states:

$untouched The field has not been touched yet
$touched The field has been touched
$pristine The field has not been modified yet
$dirty The field has been modified
$invalid The field content is not valid
$valid The field content is valid
They are all properties of the input field, and are either true or false.

Forms have the following states:

$pristine No fields have been modified yet
$dirty One or more have been modified
$invalid The form content is not valid
$valid The form content is valid
$submitted The form is submitted

Angular API

API|Description
--|--
angular.lowercase()|	Converts a string to lowercase
angular.uppercase()|	Converts a string to uppercase
angular.isString()|	Returns true if the reference is a string
angular.isNumber()|	Returns true if the reference is a number

```
<div ng-app="myApp" ng-controller="myCtrl">
<p>{{ x1 }}</p>
<p>{{ x2 }}</p>
</div>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
$scope.x1 = "JOHN";
$scope.x2 = angular.lowercase($scope.x1);
});
</script>
```

Include Cross Domains
By default, the ng-include directive does not allow you to include files from other domains.

```
<body ng-app="myApp">

<div ng-include="'https://tryit.w3schools.com/angular_include.php'"></div>

<script>
var app = angular.module('myApp', [])
app.config(function($sceDelegateProvider) {
    $sceDelegateProvider.resourceUrlWhitelist([
        'https://tryit.w3schools.com/**'
    ]);
});
</script>
</body>
```
`ngRoute` module helps your application to become a Single Page Application.

If you want to navigate to different pages in your application, but you also want the application to be a SPA (Single Page Application), with no page reloading, you can use the ngRoute module.

The ngRoute module routes your application to different pages without reloading the entire application.
Angular route module
```
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular-route.js"></script>
```
Add the dependency
```
var app = angular.module("myApp", ["ngRoute"]);
```
```
<body ng-app="myApp">

<p><a href="#/!">Main</a></p>

<a href="#!red">Red</a>
<a href="#!green">Green</a>
<a href="#!blue">Blue</a>

<div ng-view></div>

<script>
var app = angular.module("myApp", ["ngRoute"]);
app.config(function($routeProvider) {
    $routeProvider
    .when("/", {
        templateUrl : "main.htm"
    })
    .when("/red", {
        templateUrl : "red.htm"
    })
    .when("/green", {
        templateUrl : "green.htm"
    })
    .when("/blue", {
        templateUrl : "blue.htm"
    });
});
</script>

<p>Click on the links to navigate to "red.htm", "green.htm", "blue.htm", or back to "main.htm"</p>
</body>
```

```
<!DOCTYPE html>
<html>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular-route.js"></script>

<body ng-app="myApp">

<p><a href="#/!">Main</a></p>

<a href="#!banana">Banana</a>
<a href="#!tomato">Tomato</a>

<p>Click on the links to change the content.</p>

<p>Use the "otherwise" method to define what to display when none of the links are clicked.</p>

<div ng-view></div>

<script>
var app = angular.module("myApp", ["ngRoute"]);
app.config(function($routeProvider) {
    $routeProvider
    .when("/banana", {
        template : "<h1>Banana</h1><p>Bananas contain around 75% water.</p>"
    })
    .when("/tomato", {
        template : "<h1>Tomato</h1><p>Tomatoes contain around 95% water.</p>"
    })
    .otherwise({
        template : "<h1>Nothing</h1><p>Nothing has been selected</p>"
    });
});
</script>

</body>
</html>

```


More directives

Directive|	Description
--|--
ng-app|	Defines the root element of an application.
ng-bind|	Binds the content of an HTML element to application data.
ng-bind-html|	Binds the innerHTML of an HTML element to application data, and also removes dangerous code from the HTML string.
ng-bind-template|	Specifies that the text content should be replaced with a template.
ng-blur|	Specifies a behavior on blur events.
ng-change|	Specifies an expression to evaluate when content is being changed by the user.
ng-checked|	Specifies if an element is checked or not.
ng-class|	Specifies CSS classes on HTML elements.
ng-class-even|	Same as ng-class, but will only take effect on even rows.
ng-class-odd|	Same as ng-class, but will only take effect on odd rows.
ng-click|	Specifies an expression to evaluate when an element is being clicked.
ng-cloak|	Prevents flickering when your application is being loaded.
ng-controller|	Defines the controller object for an application.
ng-copy|	Specifies a behavior on copy events.
ng-csp|	Changes the content security policy.
ng-cut|	Specifies a behavior on cut events.
ng-dblclick|	Specifies a behavior on double-click events.
ng-disabled|	Specifies if an element is disabled or not.
ng-focus|	Specifies a behavior on focus events.
ng-form|	Specifies an HTML form to inherit controls from.
ng-hide|	Hides or shows HTML elements.
ng-href|	Specifies a url for the <a> element.
ng-if|	Removes the HTML element if a condition is false.
ng-include|	Includes HTML in an application.
ng-init|	Defines initial values for an application.
ng-jq|	Specifies that the application must use a library, like jQuery.
ng-keydown|	Specifies a behavior on keydown events.
ng-keypress|	Specifies a behavior on keypress events.
ng-keyup|	Specifies a behavior on keyup events.
ng-list|	Converts text into a list (array).
ng-maxlength|	Specifies the maximum number of characters allowed in the input field.
ng-minlength|	Specifies the minimum number of characters allowed in the input field.
ng-model|	Binds the value of HTML controls to application data.
ng-model-options|	Specifies how updates in the model are done.
ng-mousedown|	Specifies a behavior on mousedown events.
ng-mouseenter|	Specifies a behavior on mouseenter events.
ng-mouseleave|	Specifies a behavior on mouseleave events.
ng-mousemove|	Specifies a behavior on mousemove events.
ng-mouseover|	Specifies a behavior on mouseover events.
ng-mouseup|	Specifies a behavior on mouseup events.
ng-non-bindable|	Specifies that no data binding can happen in this element, or its children.
ng-open	Specifies| the open attribute of an element.
ng-options|	Specifies <options> in a <select> list.
ng-paste|	Specifies a behavior on paste events.
ng-pluralize|	Specifies a message to display according to en-us localization rules.
ng-readonly|	Specifies the readonly attribute of an element.
ng-repeat|	Defines a template for each data in a collection.
ng-required|	Specifies the required attribute of an element.
ng-selected|	Specifies the selected attribute of an element.
ng-show|	Shows or hides HTML elements.
ng-src|	Specifies the src attribute for the <img> element.
ng-srcset|	Specifies the srcset attribute for the <img> element.
ng-style|	Specifies the style attribute for an element.
ng-submit|	Specifies expressions to run on onsubmit events.
ng-switch|	Specifies a condition that will be used to show/hide child elements.
ng-transclude|	Specifies a point to insert transcluded elements.
ng-value|	Specifies the value of an input element.
