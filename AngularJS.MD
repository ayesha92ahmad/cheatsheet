Adding angular :
```
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
```

------------------------------------------------------------------------------------------<br>

The ng-app directive tells AngularJS that the <div> element is the "owner" of an AngularJS application.

The ng-model directive binds the value of the input field to the application variable name.

The ng-bind directive binds the innerHTML of the <p> element to the application variable name.

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

angular js directive that defines the controller. right side of the controller is the name of the javascript function it is referencing 
----------------------------------------------------------------------------------------------------------------------------

scope

In case of array of scope variable
  ```
 <li ng-repeat="x in names">{{x}}</li>           markup
 $scope.names = ["Emil", "Tobias", "Linus"];     javascript
```
---------------------------------------------------------------------------------------------------------------------------
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
----------------------------------------------------------------------------------------------------------------------------

  
