# Authentication Module
An Authentication Library for angular Using UI-Router


An Authentication library for authentication

## How it works
Using UI-Router Transition Hooks, A "requiredAuth" boolean is checked. If truthful it checks to see if any user is logged in.
If the user is logged in the route will resolve. If not the transition is rejected and the user is sent to the login page.


## File Structure


## How to Use
When defining your states add the "requiredAuth" data element.
