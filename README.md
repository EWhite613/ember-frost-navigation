[ci-img]: https://img.shields.io/travis/ciena-frost/ember-frost-navigation.svg "Travis CI Build Status"
[ci-url]: https://travis-ci.org/ciena-frost/ember-frost-navigation

[cov-img]: https://img.shields.io/coveralls/ciena-frost/ember-frost-navigation.svg "Coveralls Code Coverage"
[cov-url]: https://coveralls.io/github/ciena-frost/ember-frost-navigation

[npm-img]: https://img.shields.io/npm/v/ember-frost-navigation.svg "NPM Version"
[npm-url]: https://www.npmjs.com/package/ember-frost-navigation

[ember-observer-badge]: http://emberobserver.com/badges/ember-frost-navigation.svg "Ember Observer score"
[ember-observer-badge-url]: http://emberobserver.com/addons/ember-frost-navigation

[ember-img]: https://img.shields.io/badge/ember-1.12.2+-orange.svg "Ember 2.3.0+"

[bithound-img]: https://www.bithound.io/github/ciena-frost/ember-frost-navigation/badges/score.svg "bitHound"
[bithound-url]: https://www.bithound.io/github/ciena-frost/ember-frost-navigation

# ember-frost-navigation
###### Dependencies

![Ember][ember-img]
[![NPM][npm-img]][npm-url]

###### Health

[![Travis][ci-img]][ci-url]
[![Coveralls][cov-img]][cov-url]

###### Security

[![bitHound][bithound-img]][bithound-url]

###### Ember Observer score
[![EmberObserver][ember-observer-badge]][ember-observer-badge-url]

Navigation made easy. Makes use of liquid fire and the `RouterDSL` prototype to make a clean and concise way of
creating, and navigating routes.

Also supports [ember-engines](https://github.com/dgeb/ember-engines)

 * [Installation](#installation)
 * [API](#api)
 * [Examples](#examples)
 * [Development](#development)

## Installation
```
ember install ember-frost-navigation
```

## Usage

Add the `{{frost-navigation}}` component to the template where you want the navigation to appear, then configure
your navigation in `app/router.js`

#### Template
```hbs
{{frost-navigation
  logo=(component ...)
  menu=(component ...)

  navActions=(hash
    myAction=(action 'custom-action')
  )
}}
```

#### Router (Full Example)
```js
Router.map(function () {
  this.nav('demo', {
    path: '/'
  }, function () {
    this.category('Category 1', {
      pack: 'dummy',
      icon: 'sample'
    }, function () {
      this.column('Column 1', {
        color: '#009eef'
      }, function () {
        this.action('Action Example', {
          action: 'myAction',
          pack: 'dummy',
          icon: 'sample',
          description: 'This is an action',
          inline: true
        })
        this.app('Route Example', {
          route: 'go',
          description: 'This is a route',
          pack: 'dummy',
          icon: 'sample'
        })
        this.engine('Blog Engine', {
          route: 'blog',
          description: 'This is an engine example',
          package: 'ember-blog-engine',
          pack: 'dummy',
          icon: 'sample'
        })
        this.section('More Content', {
          color: '#a1e7ff'
        }, function () {
          this.link('Google', {
            url: 'http://google.ca',
            description: 'Go to Google',
            pack: 'dummy',
            icon: 'sample',
            tabbed: true
          })
          this.link('http://google.ca')
          this.action('Action 1', {
            action: 'myAction',
            pack: 'dummy',
            icon: 'sample'
          })
        })
      })
      this.column('Empty Column')
    })
  })
})
```

## Documentation

### `this.nav`
```js
/**
 * Initializes the navigation bar
 * @parent Ember.RouterDSL
 * @param {string} config.dialogClass class to apply to liquid-modal
 * @param {object} config.actions actions to pass up to liquid-modal
 * @param {array} config.model predefined model to be rendered
 */
```

### `this.category`

```js
/**
 * Category as a navigation bar entry
 * @parent {type:nav}
 * @param {string} config.icon icon
 * @param {string} config.pack icon pack
 * @param {array} config.model predefined category model
 */
```

### `this.column`
```js
/**
 * Creates a column viewable within a category
 * @parent {type:category}
 * @param {string} config.color color
 * @param {array} config.routes predefined routes array
 * @param {array} config.actions predefined actions array
 */
```
### `this.section`
```js
/**
 * Creates a section under within a category
 * @parent {type:category}
 * @param {string} config.color color
 * @param {array} config.routes predefined routes array
 * @param {array} config.actions predefined actions array
 */
```
### `this.app`
```js
/**
 * Creates a routable route instance
 * @parent {type:[column, section]}
 * @param {string} config.description description
 * @param {string} config.icon icon
 * @param {string} config.pack icon pack
 * @param {string} config.route route to navigate to
 * @param {object} config.params query params
 */
```
### `this.engine`
```js
/**
 * Creates a routable engine instance
 * @parent {type:[column, section]}
 * @param {string} config.package package name for engine
 * @param {string} config.route route name for nav entry
 * @param {object} config.params query params
 * @param {string} config.description description
 * @param {string} config.icon icon
 * @param {string} config.pack icon pack
 */
```
### `this.action`
```js
/**
 * Creates a menu item that serves as an action,
 * without performing a transition
 * @parent {type:[column, section]}
 * @param {string} config.description description
 * @param {string} config.icon icon
 * @param {string} config.pack icon pack
 * @param {string} config.action key for action on controller
 * @param {boolean} config.dismiss flag to dismiss modal after click
 */
```
### `this.link`
```js
/**
 * Creates a link accessible from frost-navigation
 * @parent {type:[column, section]}
 * @param {string} config.description description
 * @param {string} config.icon icon
 * @param {string} config.pack icon pack
 * @param {string} config.route navigate to route without registering on DSL
 * @param {string} config.url url to set href to
 * @param {boolean} config.tabbed flag to open in new tab (default false)
 */
```

### CSS
The following CSS classes are defined by this addon to make it easier to layout a page using `frost-navigation`:

 * `frost-application`: This class should be applied to, the parent of the `frost-navigation`
   element.
 * `frost-application-content`: This class should be applied to the element below the `frost-navigation` element.
   It will ensure that that element takes up all the space below the navigation.

```handlebars
<div class='frost-application'>
  {{frost-navigation ...}}
  <div class='frost-application-content'>
    <!-- the rest of your page here -->
  </div>
</div>
```

### User menu
An example of a user-menu is defined in the dummy app at `tests/dummy/app/pods/components/user-menu` There are also
a couple classes defined in this addon that will format your own user-menu properly:
 * `frost-navigation-user` for the actual user menu button
 * `frost-navigation-user-menu` for the popover menu that is expanded when clicking on the above button
 * `frost-navigation-user-menu-list` for the `<ul>` that holds the list items of the user menu

## Testing with [ember-hook](https://www.npmjs.com/package/ember-hook)

The navigation component is accessible using ember-hook with the top level hook names, or you can access the internal
components as well -

| Property                                     	| Hook                                                                            	|
|----------------------------------------------	|---------------------------------------------------------------------------------	|
| top level hook                               	| `$hook('frost-nav')`                                                            	|
| modal hook                                   	| `$hook('frost-nav-modal')`                                                      	|
| category hook                                	| `$hook('frost-nav-category-<index>')`                                           	|
| section / column hook                        	| `$hook('frost-nav-modal-section-<index>')`                                      	|
| section actions hook`                        	| `$hook('frost-nav-modal-section-actions')`                                      	|
| inline action from section context           	| `$hook('frost-nav-modal-section-<sectionIndex>-action-<actionIndex>')`          	|
| route hook                                   	| `$hook('frost-nav-modal-section-<sectionIndex>-route-<routeIndex>')`            	|
| frost-link within the route / action context 	| `$hook('frost-nav-modal-section-<sectionIndex>-(route / action)-<index>-link')` 	|
| action from section actions context          	| `$hook('frost-nav-modal-section-actions-<index>')`                       	        |


## Setup
```
git clone git@github.com:ciena-frost/ember-frost-navigation.git
cd ember-frost-navigation
npm install && bower install
```

## Development Server
A dummy application for development is available under `ember-frost-navigation/tests/dummy`.
To run the server run `ember server` (or `npm start`) from the root of the repository and
visit the app at http://localhost:4200.

### Testing
Run `npm test` from the root of the project to run linting checks as well as execute the test suite
and output code coverage.
