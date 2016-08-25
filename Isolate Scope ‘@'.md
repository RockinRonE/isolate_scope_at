The isolate scope “@“ binds a directive scope property to the evaluated value of a DOM attribute. 

Here’s our starting setup example: 

[JSFiddle of the setup](https://jsfiddle.net/3g8u3dh7/17/)

HTML

```html
<div ng-app="pizzaApp">
  <div ng-controller="PizzaCtrl">
    <input type="text" ng-model="ctrlTopping">
    <div pizza topping="{{ ctrlTopping }}"></div>
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
    	topping: '@',
    },
    template: '<div>{{ topping }} is the best pizza :-\)\</div>',
  };
});
```

We have setup a pizzaApp with a controller and a “pizza” directive in which you can enter the topping of the pizza. When you enter a topping you’ll notice that your input (ctrlTopping) is interpolated and it appears below the box. The isolate scope “@“ binds the evaluated value `{{ctrlTopping}}`​ to our topping scope property, inserts it to a div, which is dropped into the pizza element directive. 

What’s happening under the hood is that the @ isolate scope is acting as if it’s a linking function. Check out the example below: 

HTML

```html
<div ng-app="pizzaApp">
  <div ng-controller="PizzaCtrl">
    <div pizza topping="Mushroom"></div>
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
    template: '<div>{{ topping }} is the best pizza :-\)\</div>',
    link: function (scope, element, attrs) {
    	scope.topping = attrs.topping; 
    }
  };
});
```

Here our linking function on line 9 and 10 is setting the topping attribute from the directive to scope.topping, which then is dropped into the pizza element directive. [Check out the fiddle](https://jsfiddle.net/3g8u3dh7/24/)