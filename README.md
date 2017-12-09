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
├── auth.module.ts                  # Main Module
├── auth.hook.ts                    # Transition Hook
├── auth.states.ts                  # States with Meta Data
├── Login                           # Login Component
│   ├── login.component.ts          # Build for Production
│   ├── login.component.css         # Build for Production
│   ├── login.component.html        # Build for Production
├── Register                        # Registration Component
├── ForgotPassword                  # Forgot Password Component
├── shared                          # Shared components and Services
│   ├── webpack.build.prod.js       # Build for Production
│   ├── webpack.js                  # Main Build for development
│   ├── webpack.serve.dev.js        # Build for dev server
│   ├── webpack.serve.prod.js       # Build for production
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
When defining your states add the "requiredAuth" data element.
