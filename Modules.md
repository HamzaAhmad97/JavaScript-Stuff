The main idea descussed here is that when everything in a program is deeply entangled so that every single peice of code depends on the other in a way that does not show or support using already defined peices of code, adding features or fixing errors will be a really hard problem, that's why we rely on modules and packages to preserve code that can be used multiple times and to avoid falling in such traps.

## Modules

A module is a piece of program that specifies which other pieces it relies on and which functionality it provides for other modules to use (its interface).

An interface is the functionality that modules provide, just like objects, we use their methods and access their publicaly available properties, the rest is internal or hidden.

By restricting the ways in which modules interact with each other, the system becomes more like LEGO, where pieces interact through well-defined connectors.

The relations between modules are called dependencies. When a module needs a piece from another module, it is said to depend on that module.

Since modules rely on each other via their dependencies, each module needs its private scope. Meaning that putting js code into different files does not satisfy theses requirements since the files still share the global namespace, so they can intentionally or accidentally interfere with each other's bindings.

## Packages

The idea is to build a program out of separate pieces which can run on their own, and you can also use or apply the different pieces in different programs.

A package is a chunk of code that can be distributed (copied and installed). It may contain one or more modules and has information about which other packages it depends on.

Packages also come with documentation explaining what they do.

The place or the infrastructure that is used to store and find packages is NPM [](https://npmjs.org).

Some people use licenses to allow others to use their packages freely and some require others to publish thier codes on top of the package, so it is a good thing to check the type of licenses.

## Evaluating data is code 

Using `eval(string)`, we can execute a string in the *current* scope, although it is not recommended for security reasons.

``` 
let x = 1;
eval('x = 2');
console.log(x); // -> 2
```
We can also use the Function constructor to do almost the same (interpreting data as code). It takes two arguments: a string containing a comma-separated list of argument names and a string containing the function body.

```
let plusOne = Function("n", "return n + 1;");
console.log(plusOne(4));
// → 5
```

For a module system, we can wrap the module's code in a function and use the functions's scope as module scope.

## Commonjs

Node.js uses it and is the system used by most packages on NPM.

Using the function **require**, when you call this with the module name of a dependency, it makes sure the module is loaded and returns its interface.

**Because the loader wraps the module code in a function, modules automatically get their own local scope. All they have to do is call require to access their dependencies and put their interface in the object bound to ***exports***.**

to import a module:
```
const package = require('module-name')
```
A JavaScript file is a module when it exports one or more of the symbols it defines, being them variables, functions, objects, suppose we have the file *uppercase.js*:

```
exports.uppercase = (str) => str.toUpperCase()
```

Then we can use this module in any other js file:

```
const uppercaseModule = require('uppercase.js')
uppercaseModule.uppercase('test')
```


The module adds its interface function to exports so that modules that depend on it get access to it.

we can export more than one value:

```
exports.a = 1
exports.b = 2
exports.c = 3
```

Then we can import them individually using destructuring assignment;

```
const { a, b, c } = require('./uppercase.js')
```

Since the module system will create an empty interface object for you (bound to exports), you can replace that with any value by overwriting module.exports **in order to export a single value instead of an interface**.

```
module.exports = value
```

and import it this way:

```
const value = require('./file.js')
```

require keeps a store (cache) of already loaded modules. When called, it first checks if the requested module has been loaded and, if not, loads it. This involves reading the module’s code, wrapping it in a function, and calling it.


The string given to require is translated to an actual filename, for example when it starts with ./ or ../ it is generally interpreted as relative to the cuttent module's filename.

Commonjs is not suitable for the client-side, so ES modules were introduced.

## ECMscript (ES) modules

When it comes to commonjs, the things added to exports are not available in the local scope, also, it can be hard to determine the dependencies of module without running its code.

to import a module:

```
import ordinal from "ordinal";
import {days, months} from "date-names";
```

**export** may appear in front of a function, class, or binding definition ( let , const , or var ).

to export:

```
export function formatDate(date, format) { /* ... */ }
```

An ES module’s interface is not a single value but a set of named bindings.

**here, when you import from another module, you actually import the binding not the value, which means exporting module may change the value of the binding at any time and the modules that import it will see its new value.

when there is a binding named **default**, it is treated as the module's main exported value. If you import a module without braces around the binding name, you get its default binding.

to create a default export:

```
export default ["Winter", "Spring", "Summer", "Autumn"]
```

to rename imported bindings we use the keyword **as**:

```
import {days as dayNames} from "date-names";
```

Another important difference is that ES module imports happen before a module’s script starts running. That means import declarations may not appear inside functions or blocks, and the names of dependencies must be quoted strings, not arbitrary expressions.

* **bundlers**: since fetching a single big file tends to be faster than fetching a lot of tiny ones, these tools roll programs back into a single big file before they publish to the web.

* **multiple**: tools that take a js program and make it smaller by automatically removing comments and whitespaces, renaming bindings and replacing pieces of code with equivalent code that takes less space.

the idea behimd thesse two is that **the JavaScript code you run is often not the code as it was written.**

# End











