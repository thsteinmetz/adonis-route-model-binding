# adonis-route-model-binding

This package just takes the example from the the [AdonisJS](https://adonisjs.com) documentation about [extending routes](https://adonisjs.com/docs/4.1/routing#_extending_routes) and adds an additional lookup parameter (the field to look up on) to it.

This package is for AdonisJS 4.x.

## Example Usage

First install this package

```bash
adonis install adonis-route-model-binding
# or
npm install --save adonis-route-model-binding
# or
yarn add adonis-route-model-binding
```

Add the RouteModelBindingProvider to your `start/app.js` file

```js
const providers = [
  ...
  'adonis-route-model-binding/providers/RouteModelBindingProvider',
]
```

Add the binding to a route that you have in your routes file:

```js
Route.get('some/route/:userId', 'UserController.show')
      .bind('App/Models/User', 'user', 'userId', 'id');
```

What does that mean? Below is an explanation of the list of parameters on the above `.bind(..)` method in order.

1. `App/Models/User` is the target model that you want to load

2. `user` is the key that this model will be bound to on the `request` object that gets passed into the controller

3. `userId` is the route parameter that we are using. The `:userId` on `some/route/:userId` in this case

4. *Optional* `id` is the database field we are going to look up the value of `userId` in. `id` is the default so you can leave this off unless you want to explicitly look up on another field.

Now in your controller you will have access to the `user` object on the `show()` method:

```js
class UserController {
  
  async show({ request, params, user }) {
    // do something with user here
  }
  
}
```

## Changelog

### v0.1.0
- Initial release

## License
DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE
TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION AND MODIFICATION

[WTFPL](http://www.wtfpl.net/)