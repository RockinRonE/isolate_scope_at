Lets review the isolate scopes that we went over together.

HTML

```html
<div ng-app="pizzaApp">
  <div ng-controller="PizzaController">
    <pizza type="Mushroom" brand="brand" bake-pizza="bakePizza(type, message)"></pizza>
    <pizza type="Pepperoni" brand="brand" bake-pizza="bakePizza(type, message)"></pizza>
    <pizza type="Sausage" brand="brand" bake-pizza="bakePizza(type, message)"></pizza>
  </div>
</div>
```

JS

```js
var app = angular.module('pizzaApp', []);

app.controller('PizzaController', function($scope){
  $scope.bakePizza = function(type, message){
    alert('Your ' + type + ' pizza was ' + message);
  };
});

app.directive('pizza', function(){
  return {
    restrict: 'E',
    scope: {
      type: '@',
      brand: '=',
      bakePizza: '&'
    },
    template:  '<div class="panel">Type: {{type}}<br> Brand:<select ng-model="brand" ng-options="brand for brand in brands"></select><br>' + 'How was your pizza? <input type="text" ng-model="value">' + '<br><button ng-click="bakePizza({type: type, message:value})">Give a Shout Out!</button><br><hr>',
    
   
    link: function(scope){
        scope.brands = ["Papa Johns", "Pizza Hut", "Dominoes"];
        scope.brand = scope.brands[0];
      }
  };
});
```

[The fiddle](https://jsfiddle.net/kpjxt0tm/22/)

A recap of what the three scopes do:

1. @ symbol reads an **AT**tribute. The pizza type appears in the HTML due to the @ symbol
2. = symbol is for two way binding. We’re only ordering our pizzas from one company at a time, so when a company is selected the other drop menus change with it. There is no relationship with between the directives themselves, but two way binding causes them to refelct the same values.
3. & symbol allows us to call our bakePizza function in the controller. Note that in Angular when you have a camel case name, it’s typed with a dash in the HTML: bakePizza =\> bake-pizza















