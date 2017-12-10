# Authentication Module
An Authentication Library for angular Using UI-Router


An Authentication library for authentication


## How it works
Using UI-Router Transition Hooks, A "requiredAuth" boolean is checked. If truthful it checks to see if any user is logged in.
If the user is logged in the route will resolve. If not the transition is rejected and the user is sent to the login page.

## Key Features

#### Core
* [Angular](http://angular.io/)
* [Ui-Router](https://ui-router.github.io/)
* [Angular Material](https://material.angular.io/)


#### Packing 
* [webpack](https://github.com/webpack/webpack)
* [babel](https://github.com/babel/babel)
* [eslint](http://eslint.org)

#### Testing
* [mocha](https://mochajs.org/)
* [sinon](http://sinonjs.org/)
* [chai](https://github.com/chaijs/chai)
* [husky](https://github.com/typicode/husky) 


#### CSS
* [reflex](leejordan.github.io/reflex/docs/)
* [santize](https://github.com/jonathantneal/sanitize.css/)
* [postcss](https://github.com/postcss/postcss)
* [stylelint](https://www.npmjs.com/package/stylelint)


Here are all the scripts that you can run

|`npm run <script>`|Description|
|------------------|-----------|
|`start`|Serves your app at `localhost:8080`. "webpack-dev-server --config \"config/webpack.serve.dev\" --progress --inline".|
|`test`|Runs unit tests with Karma and generates a coverage report. "mocha --require ignore-styles --reporter mocha-multi-reporters --reporter-options configFile=config/mocha-multi-reporters.json tests/ignore-utils.js tests/helpers/setup.js tests/**/*tests.js src/**/*tests.js"|
|`dev`|Same as `npm start`, but enables nodemon for the server as well.|
|`serve-dist`|Serves the production verstion fo the app "webpack-dev-server --config \"config/webpack.serve.prod\""|
|`prestart`|Removes Unecessary packages and runs tests "npm run lint && npm run test"|
|`clean`|remove the dist folder "rimraf dist"|
|`build`|Builds the Production version of the app "webpack --config \"config/webpack.build.prod\" --optimize-minimize --progress -p"|
|`lint:js`|Lint all `.js` files. "eslint \"./src\"", [Read more on this](http://eslint.org/docs/user-guide/command-line-interface.html#fix). |
|`lint`|Lint all `.js` and `.css` files. "npm run lint:js && npm run lint:css" |
|`lint:css`|Lint and fix all `.css` files. "stylelint \"./src/**/*.css\"", |



### Application Structure

This application strcuture here as a suggestion and can be changed to fit your needs. It is meant to be a guideline.

```
.
├── auth.module.ts                      # Main Module
├── auth.hook.ts                        # Transition Hook
├── auth.states.ts                      # States with Meta Data
├── Login                               # Login Component
│   ├── login.component.ts              # Login Compoment
│   ├── login.component.css             # Login Component Styles
│   └── login.component.html            # Login Component HTML
├── Register                            # Registration Component
│   ├── register.component.ts           # Registration Compoment
│   ├── register.component.css          # Registration Component Styles
│   └── register.component.html         # Registration Component HTML
├── Forgot-password                     # Forgot Password Component
│   ├── forgot-password.component.ts    # Registration Compoment
│   ├── forgot-password.component.css   # Registration Component Styles
│   └── forgot-password.component.html  # Registration Component HTML
├── shared                              # Shared components and Services
│   ├── services                        # Build for Production
│   ├── models                          # Main Build for development
│   ├── webpack.serve.dev.js            # Build for dev server
│   ├── webpack.serve.prod.js           # Build for production
│   └── mocha-multi-reporters.json  # 
├── src                             # Application source code
│   ├── index.html                  # Main HTML page container for app
│   ├── index.js                    # Application Entry Point and Route Definition
│   ├── index.css                   # Application-wide styles (generally settings)
│   ├── app                         # Components that dictate major page structure
│   │   ├── Dashboard               # Dashboard Page
│   │   ├── Home                    # Home Page
│   │   ├── MainLayout              # Main Template for layout
│   │   ├── NotFound                # Not Found Page
│   │   └── Shared                  # Shared Re-usable Components
│   └── shared                      # Main route definitions and async split points
│       ├── images                  # Images for the app
│       │   └── favicon.ico         # Favicon for the app
│       └── theme                   # Assets for the app
│           ├── fonts               # Fonts for the app
│           ├── index.js            # Setup for the Theme
│           └── variables.js        # CSS variables for colors and Sizes
└── tests                           # Unit tests
```

## How to Use

### Declaring your states
When defining your states add the "requiredAuth" data element.

```
export const enrollState = {
	parent: 'app',
	name: 'sampleRoute',
	url: '/sample',
	component: SampleAppComponent,
	params: {
		brokerId: '',
	},
	data: { 
		meta: {
			title: 'Sample Route'
		},
		requiresAuth: true,
	},
}
```
### Implement Using UIRouterModule.forRoot()

```
UIRouterModule.forRoot({
    states: App_states,
    useHash: true,
    otherwise: {state: 'home'},
    config: routerConfigFn,
  })
 ```
 
 ### Router Configuration
 The Router Configuration file is configured like this
 
 ```
 import { UIRouter, Category } from "@uirouter/angular";

// Hooks
import { requiresAuthHook } from './Auth/auth.hook';

export function routerConfigFn(router: UIRouter) {
  const transitionService = router.transitionService;
  requiresAuthHook(transitionService);

  router.trace.enable(Category.TRANSITION);
}
 ```
 
 It calls the transition and declares the hook on service.
