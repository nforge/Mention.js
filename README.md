# Mention.js

<img src="http://i39.tinypic.com/315ir2c.png">

Lightweight (min: ~1.92kb, full: ~4.07kb) wrapper for adding mention auto-completion functionality to Twitter Bootstraps Typeahead plugin.

This enables you to have Twitter-like `@` user mentions, `#` hashtag or any related fucntionality in textarea.

<b>View the demo <a href="http://bijanebrahimi.github.io/Mention.js/" target="_blank">here</a>.</b>

# Version
0.1.0

## Dependencies
* <a href="https://github.com/jquery/jquery" target="_blank">jQuery</a>
* <a href="https://github.com/twitter/bootstrap" target="_blank">Typeahead</a>

## Simple Usage
The `users` parameter accepts an array of objects. **key** value should be
defined which is equal to object variable we want to mention, in this case `username`.

`````javascript
$("#multi-users").mention({
    key: 'username',
    delimiter: '@',
    users: [{
        username: "ashley"
    }, { 
        username: "roger"
    }, { 
        username: "frecklefart123"
    }, {
        username: "jquery",
        delimiter: "#"
    }, {
        username: "plugin",
        delimiter: "#"
    }]
});
`````

## List of available Options

Option | Optional | Description | default 
:-----------|:------------|:------------|:------------
 delimiter  | yes | the character to trigger mention list to pops up | `'@'`
 delimiters | yes | string list of all defined delimiters, without any space | generats from list if not defined
 name | yes | the object value in user's list representing the name | `'name'`
 key | yes | the object value in user's list representing the key | `'username'`
 image | yes | the object value in user's list representing the avatar image
 users | no | array containing user's objects | 
 sensitive | yes | reorder the mention list by the best candidate to lowest | `true`
 emptyQuery | yes | if set true, show mention list by typing delimiter character | `false`
 queryBy | yes | array of object's value to search in | value of `key` option
 typeaheadOpts | yes | extra options for Twitter Bootstrap typeahead plugin | `{}`


## Options

### Sensitivity

With sensitivity set to true, items are ordered by the following divisions of priority:

* Highest: If first letter matches exactly
* High: If first letter matches regardless of case
* Med: If target has matching letters' case
* Low: if target has matching character regardless of case

### Overriding the delimiter:

You can override the delimitter for each array objects by defining `delimiter`
object value. for instance to have *developer* and *developing* hashtag we can
simple define extra delimiter value in each of them and set them to '#':

`````javascript
$("#multi-users").mention({
    delimiter: '@',
    users: [{
        username: "bob",
        name: "Bob Smith",
    }, { 
        username: "alice",
        name: "Alice Smith",
    }, { 
        username: "developer",
        name: "Developer",
        delimiter: "#"
    }, { 
        username: "developing",
        name: "Developing",
        delimiter: "#"
    }]
});
`````


### Sensitivity Examples:
If you were to query `"@r"`, with sensitivity on, the resulting list will be
`["roger", "Ricky", "sarah", "bigRat"]`, but if you were to query `"@R"`, the
resulting list would be `["Ricky", "roger", "bigRat", "sarah"]`


## Name, Username and Image Object's value
Object values of `name`, `username` and `image` in user's list will be shown
in mention list menu if defined. Username value is the one by selecting an
item, will be put into your textbox/input. username is required for this
script to work. each of these object values can be change to something else
by setting `key`, `name` or `image` option. 

`````javascript
$("#multi-users").mention({
    image: 'avatar',
    users: [{
        username: "bob",
        name: "Bob Smith",
        avatar: "http://placekitten.com/25/25"
    }, { 
        username: "alice",
        name: "Alice Smith",
        avatar: "http://placekitten.com/25/25"
    }]
});
`````

## Query
The `queryBy` parameter accepts an array of strings that represent keys in your
user object that you would like to query against. For example, if you were to
type in the `name` "@bob", the script would match the `username` "@bigCat". the
default value is equal to the value of `key` option.

## Empty Querying
You may query for users simply by pressing your delimiter. For example, pressing
the @ symbol will return all users that are a part of your users list, so long
as those users adhere to the `typeaheadOpts.items` limit
```javascript
$('#multi-users').mention({
    emptyQuery: true,
    typeaheadOpts: {
        items: 10 // Max number of items you want to show
    },
    users: [...]
});
```


## Defaults
`````javascript
$("#multi-users").mention({
    key: 'username',
    name: 'name',
    image: 'image',
    users: [], // Array of Objects
    delimiter: '@', // Username Delimiter
    delimiters: '', // Will be filled from user list delimiters
    sensitive : true,
    queryBy: ['username'],
    typeaheadOpts: { // Settings for Typeahead
        matcher: _matcher, // Mention.js's custom matcher function, don't change
        updater: _updater, // Mention.js's custom updater function, don't change
        sorter: _sorter, // Mention.js's custom sorter function, don't change
    }
});
 
`````
 
### License

(The MIT license)

Copyright (c) 2013 Jacob Kelley

Copyright (c) 2013 Bijan Ebrahimi 

* added overriding delimiter
* added optional key/name/image object variable name 
* removed already mentions objects from emptyQuery result
* fixed unclosed mention menu bug
* enhanced query results
* added versioning

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
