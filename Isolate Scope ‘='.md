The isolate scope “=“ sets up a two-way binding with an object (not a string as with @). 

HTML

```html
<div ng-app="pizzaApp">
  <div ng-controller="PizzaCtrl">
  
    <!-- Controller -->
    <p>Input from controller</p>
    <input type="text" ng-model="ctrlTopping">
    
    <!-- Directive -->
    <div pizza topping="ctrlTopping"></div>
  </div>
</div>
```

JS

```js
var app = angular.module('pizzaApp', []);

app.controller("PizzaCtrl", function ($scope) {
})

app.directive("pizza", function () {
  return {
		scope: {
    	topping: '=',
    },
    template: '<p>Input from template directive</p> <input type="text" ng-model="topping">',
  };
});
```

[And the fiddle](https://jsfiddle.net/m40cw5wg/1/)

We have setup our `​pizza`​ directive with the `​topping`​ binding as an input that is bound to `​ctrlTopping`​.

If you inspect element on the input from template directive, you’ll see this:

```html
<!--Directive-->
<div pizza topping="ctrlTopping">
  <p>Input from template directive</p> 
  <input type="text" ng-model="topping">
</div>
```

I am trying to explain how it’s bound. I am confused by controller binding and model binding if that makes sense











