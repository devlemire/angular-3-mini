<img src="https://devmounta.in/img/logowhiteblue.png" width="250" align="right">

# Project Summary

In this project, we'll implement routing into an Angular application. You'll notice that the `js/` folder has another level of folders inside of it. The Angular community has found the best way to organize your files, so your project can scale, is too break out your code into "features". Therefore, you'll find all the HTML and JS for each feature in its folder. Take a minute to get familiar with the file structure.

## Setup

* Fork and clone this repository
* Take a minute to familiarize yourself with the file structure.

## Step 1

### Summary

In this step, we'll create a container where the routing HTML will live. We'll also add some static HTML for navigating between routes.

### Instructions

* Open `index.html`.
* Above your `scripts` tags in the `body`, create a new `div` with a class of `menu`.
  * Inside of `menu` and a `ul` element with three `li` elements:
  * Each `li` element should contain an `a` element with a `ui-sref` attribute that equals the name of the feature.
  * The `li` for the products feature should have a nested `ul` element with an `li` for `Shoes` and `Socks`.
    * The `ui-sref` attribute on these `li` elements should use an object with an `id` property that equals `Shoes` or `Socks`.
* Under the `div` with a class of `menu` add a new `div` with a class of `view-container`.
  * Inside of `view-container` add a `div` element with an attribute `ui-view` that doesn't equal anything

### Solution

<details>

<summary> <code> index.html </code> </summary>

```html
<!DOCTYPE html>
<html ng-app="myApp">
  <head>
    <title>Routing App</title>
    <link type="text/css" rel="stylesheet" href="styles.css" />
  </head>

  <body>
    <div class="menu">
      <ul>
        <li><a ui-sref="home">Home</a></li>
        <li>
          Products
          <ul>
            <li><a ui-sref="products({id: 'shoes'})">Shoes</a></li>
            <li><a ui-sref="products({id: 'socks'})">Socks</a></li>
          </ul>
        </li>
        <li><a ui-sref="settings"> Settings </a></li>
      </ul>
    </div>

    <div class="view-container">
      <div ui-view></div>
    </div>

    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.6/angular.min.js"></script>
    <script src="js/app.js"></script>
  </body>
</html>
```

</details> 

## Step 2

### Summary

In this step, we'll inject `ui.router` into our Angular application and define the available routes.

### Instructions

* Open `js/app.js`.
* Inject `ui.router` into `myApp`.
* Chain a `.config` to `myApp` that uses an anonymous function.
  * Just like you would for a `controller` or `service`.
* Inject `$stateProvider` and `$urlRouterProvider` into the anonymous function.
* Call `$stateProvider` and chain a `.state` for each feature route ( hint: there should only be three ).
  * `.state` should be invoked and passed two parameters:
    * The first parameter is the `string` of the route. This much match the strings used in the previous step.
      * Hint: `ui-sref`.
    * The second parameter is and object that has three properties:
      * url: A string that specifies the route
      * templateUrl: A string that is a file path to the HTML. 
      * controller: A string that specifies what controller the HTML should use.
* Call `$urlRouterProvider` and chain a `.otherwise` and pass in `'/'`.

### Solution

<details>

<summary> <code> js/app.js </code> </summary>

```js
angular.module('myApp', ['ui.router']).config( function( $stateProvider, $urlRouterProvider ) {
  $stateProvider
    .state('home', {
      url: '/',
      templateUrl: 'js/home/homeTmpl.html',
      controller: 'homeCtrl'
    })
    .state('products', {
      url: '/products/:id',
      templateUrl: 'js/products/productsTmpl.html',
      controller: 'productsCtrl'
    })
    .state('settings', {
      url: '/settings',
      templateUrl: 'js/settings/settingsTmpl.html',
      controller: 'settingsCtrl'
    });

  $urlRouterProvider
    .otherwise('/');
});
```

</details>

## Step 3

### Summary

In this step, we'll modify the products feature to display data based on what page the user is on.

## Contributions

If you see a problem or a typo, please fork, make the necessary changes, and create a pull request so we can review your changes and merge them into the master repo and branch.

## Copyright

© DevMountain LLC, 2017. Unauthorized use and/or duplication of this material without express and written permission from DevMountain, LLC is strictly prohibited. Excerpts and links may be used, provided that full and clear credit is given to DevMountain with appropriate and specific direction to the original content.

<p align="center">
<img src="https://devmounta.in/img/logowhiteblue.png" width="250">
</p>

