The isolate scope ‘&’ allows you to invoke an expression from your app’s controller. Lets start off with this initial setup:

HTML

```html
<div ng-app="pizzaApp">
  <div ng-controller="PizzaCtrl">
    <div pizza topping="bakePizza()"></div>
  </div>
</div>
```

JS

```js
var app = angular.module('pizzaApp', []);

app.controller("PizzaCtrl", function ($scope) {
  $scope.bakePizza = function () {
    alert("An awesome pizza!");
  };
});

app.directive("pizza", function () {
  return {
    scope: {
      topping: "&"
    },
    template: '<div class="button" ng-click="topping()">What kind of pizza was baked?</div>',
  };
});
```

[The fiddle](https://jsfiddle.net/xrvvznw2/12/)

**The isolate scope ‘&' allows you to invoke an expression of the parent scope of the directive.** In this case it is `​PizzaCtrl`​ since our `​pizza`​ directive is wrapped with our `​PizzaCtrl`​ div (true?). When our button is clicked, our `​topping`​ (binding?) is bound to `​bakePizza()`​, which invokes this function in the `​PizzaCtrl`​.

Since the isolate scope ‘&’ allows you to invoke an expression, it is possible to pass data into method within the template. For example: 

HTML

```html
<div ng-app="pizzaApp">
  <div ng-controller="PizzaCtrl">
    <div pizza topping="bakePizza(topping)"></div>
  </div>
</div>
```

JS

```js
var app = angular.module('pizzaApp', []);

app.controller("PizzaCtrl", function ($scope) {
  $scope.bakePizza = function (topping) {
    alert('You baked a ' + topping + ' pizza :-)');
  };
});

app.directive("pizza", function () {
  return {
    scope: {
      topping: "&"
    },
    template: '<input type="text" ng-model="type">' +
      '<button ng-click="topping({topping:type})">' +
      'Bake Pizza!</button>',
  };
});
```

[The Fiddle](https://jsfiddle.net/zwmvgn1w/2/)

Here we setup a method called `​bakePizza`​. The relationship is setup by passing this method to an attribute called `​topping`​. This `​topping`​ is defined with the isolate scope ‘&’, which means we can invoke `​topping`​ through `​ng-click`​, passing in a `​type`​ from the input to the `​topping`​ object.





















