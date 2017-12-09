# Authentication Module
An Authentication Library for angular Using UI-Router


An Authentication library for authentication

## How it works
Using UI-Router Transition Hooks, A "requiredAuth" boolean is checked. If truthful it checks to see if any user is logged in.
If the user is logged in the route will resolve. If not the transition is rejected and the user is sent to the login page.


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
