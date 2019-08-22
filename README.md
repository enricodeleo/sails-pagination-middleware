# sails-pagination-middleware-header

## About

Middleware for sails.js for finding the total count by criteria and injecting it among headers. 

Criteria pagination / filtering is built in to Sails, with keywords `limit`, `skip`, `where`. This package only adds a X-Total-Count header to aid with building page indicators. You could define your page size in your frontend application with the keyword `limit` and just adjust `skip` accordingly. Meaning you could implement all sorts of different pagination indicators with this system.

## Basic Usage

    npm install --save sails-pagination-middleware-header

Then in your `config/http.js`, add `paginate` to first place in array:

    middleware: {
        paginate: require('sails-pagination-middleware'),
        order: [
          'paginate',
          // ...
         ]

## Sails version support
It only supports __Sails 1.x+__

## Advanced Usage

You can create a policy, say we called it `api/policies/paginate.js`

    module.exports = require('sails-pagination-middleware').generate({});

Then in `config/policies.js` you can specify which `find` call will get augmented with the count field.

    UserController: {
        'find': ['isLoggedIn', 'paginate'],
    }

## Extra Options

There are options that you can change, just call the `generate()` function

        require('sails-pagination-middleware').generate({
            // if you want to add/remove an action i.e. 'user/search' or whatever
            // the array can contain a string for exact match or a regular expression for a pattern
            // if you use this options, the array you use will override the default, it will NOT concat
            // this is the default,
            // it will match all the usual :model/find, :model/:id/:association/populate
            actions: ['find', 'populate', /^.*\/(find|populate)$/]

            // if the .count() calls fails, to throw an error or not
            silentError: false // default
        }),

## Credits

This package is a fork of the beautiful [sails-pagination-middleware](https://github.com/xtrinch/sails-pagination-middleware).
