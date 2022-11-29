# Objects
* JavaScript object also __inherits__ the properties of another object, known as its __"prototype."__
* The methods of an object are typically inherited properties, and this __"prototypal inheritance"__ is a key feature of JavaScript.
* __Any value__ in JavaScript that is not a _string_, a _number_, a _Symbol_, or _true_, _false_, _null_, or _undefined_ is an object.
* And even though strings, numbers, and booleans are not objects, they can behave like __immutable objects__.
* Objects are __mutable__ and manipulated by __reference__ rather than by __value__.
* The most common things to do with objects are to __create__ them and __set__, __query__, __delete__, __test__, and __enumerate__ their properties.
* A property has a name and a value.
* A property name may be any string, including the empty string (or any Symbol), but __no object may have two properties__ with the same name.
* JavaScript
uses the term ```own property``` to refer to non-inherited properties.
* In addition to its name and value, each property has three ___property attributes:___
    * The ___writable attribute___ specifies whether the value of the property can be set.
    * The ___enumerable attribute___ specifies whether the property name is returned by a
    for/in loop.
    *  The ___configurable attribute___ specifies whether the property can be deleted and whether its attributes can be altered.
* Many of JavaScript’s __built-in__ objects have properties that are ___read-only, non-enumerable, or non-configurable.___
* __By default__, however, all properties of the objects you create are ___writable, enumerable, and configurable___.
# Creating Objects
* Objects can be created with __object literals__, with the __new keyword__, and with the __Object.create()__ function.
## Object Literals
* The ___easiest way___ to create an object is to include an object literal in your JavaScript code.
* In its simplest form, an object literal is a comma-separated list of colon-separated name:value pairs, enclosed within curly braces.
* A property name is a Java‐Script identifier or a string literal (the empty string is allowed).

```javascript
let empty = {}; // An object with no properties
let point = { x: 0, y: 0 }; // Two numeric properties
let p2 = { x: point.x, y: point.y+1 }; // More complex values
let book = {
    "main title": "JavaScript", // These property names include spaces,
    "sub-title": "The Definitive Guide", // and hyphens, so use string literals.
    for: "all audiences", // for is reserved, but no quotes.
    author: { // The value of this property is
        firstname: "David", // itself an object.
        surname: "Flanagan"
    }
};
```
* A ___trailing comma___ following the last property in an object literal is legal, and some programming styles encourage the use of these trailing commas so you’re ___less likely to cause___ a syntax error if you add a new property at the end of the object literal at some later time.
* ___An object literal is an expression that creates and initializes a new and distinct object each time it is evaluated.___
* The value of each property is evaluated each time the literal is evaluated.
* This means that a single object literal can create many new objects if it appears within the body of a loop or in a function that is called repeatedly, and that the property values of these objects may differ from each other.
## Creating Objects with new
* ___The new operator creates and initializes a new object.___
* ___The new keyword must be followed by a function invocation.___
* ___A function used in this way is called a constructor___ and serves to initialize a newly created object.
* JavaScript includes constructors for its built-in types.

_For example:_
```javascript
let o = new Object(); // Create an empty object: same as {}.
let a = new Array(); // Create an empty array: same as [].
let d = new Date(); // Create a Date object representing the current time
let r = new Map(); // Create a Map object for key/value mapping
```
# Prototypes
* Almost __every__ JavaScript object has __a second JavaScript object__ associated with it.
* ___This second object is known as a prototype, and the first object inherits properties from the prototype.___
* __All objects _created by object literals_ have the same prototype object__, and we can refer to this prototype object in JavaScript code as ```Object.prototype```.
* ___Objects created using the new keyword and a constructor invocation use the value of the prototype property of the constructor function as their prototype.___
* So the object created by __new Object()__ inherits from ```Object.prototype```, just as the object created by {} does.
* Similarly, the object created by new Array() uses Array.prototype as its prototype, and
the object created by new Date() uses ```Date.prototype``` __as its prototype__.
* ___Remember:___ _almost all objects have a prototype, but only a relatively small number of objects have a prototype property._ 
* It is these objects with prototype properties that define the prototypes for all the other objects.
* ```Object.prototype``` ___is one of the rare objects that has no prototype: it does not inherit any properties.___ 
* _Other prototype objects are normal objects that do have a prototype._
* Most __built-in constructors__ (and most user-defined constructors) have a prototype that inherits from Object.prototype.
* _For example_, ```Date.prototype``` ___inherits properties___ from ```Object.prototype```, so a Date object created by ```new Date()``` inherits properties ___from both___ ```Date.prototype``` and ```Object.prototype```.
* ___This linked series of prototype objects is known as a prototype chain.___
## Object.create()
* ___```Object.create()``` creates a new object, using its first argument as the prototype of that object:___
```javascript
let o1 = Object.create({x: 1, y: 2}); // o1 inherits properties x and y.
o1.x + o1.y // => 3
```
* You can pass ___null___ to create a new object that does ___not have a prototype___, but if you do this, the newly created object will not inherit anything, not even basic methods like ```toString()``` (which means it won’t work with ___the + operator___ either):
```javascript
let o2 = Object.create(null); // o2 inherits no props or methods.
```
* If you want to create an ordinary empty object (like the object returned by __{}__ or __new Object()__), pass __Object.prototype__:
```javascript
let o3 = Object.create(Object.prototype); // o3 is like {} or new Object().
```
# Querying and Setting Properties

* To obtain the value of a property, use the __dot (.)__ or __square bracket ([])__ operators.
``` javascript
let author = book.author;   //Get the "author" property of the book.
let name = author.surname; // Get the "surname" property of the author.
let title = book["main title"]; // Get the "main title" property of the book.
```
* _To create or set a property, use a dot or square brackets._
```javascript
book.edition = 7; // Create an "edition" property of book.
book["main title"] = "ECMAScript"; // Change the "main title" property.
```
# Objects As Associative Arrays
```javascript
object.property
object["property"]
```
* The second syntax, __using square brackets__ and a string, looks like array access, but to an array indexed by strings rather than by numbers.
* __This kind of array is known as an associative array (or hash or map or dictionary).__
* ___JavaScript objects are associative arrays.___
* _Strings are JavaScript data‐
types, so they can be manipulated and created while a program is running. So, for
example, we can write the following code in JavaScript:_
``` javascript
let addr = "";
for(let i = 0; i < 4; i++) {
addr += customer[`address${i}`] + "\n";
}
```
* This code __reads__ and __concatenates__ the __address0, address1, address2, and address3__ properties of the customer object.
# Inheritance
* Every time you create an __instance of a class__ with __new__, you are creating an object that ___inherits properties from a prototype object___.
* ___Suppose you query the property x in the object o. If o does not have an own property with that name, the prototype object of o is queried for the property x. If the prototype object does not have an own property by that name, but has a prototype itself, the query is performed on the prototype of the prototype. This continues until the property x is found or until an object with a null prototype is searched. As you can see, the prototype attribute of an object creates a chain or linked list from which properties are inherited:___

```javascript
let o = {};   // o inherits object methods from Object.prototype
o.x = 1;      // and it now has an own property x.
let p = Object.create(o); // p inherits properties from o and Object.prototype
p.y = 2;      // and has an own property y.
let q = Object.create(p); // q inherits properties from p, o, and...
q.z = 3;      // ...Object.prototype and has an own property z.
let f = q.toString(); // toString is inherited from Object.prototype
q.x + q.y     // => 3; x and y are inherited from o and p
```
* ___Now suppose you assign to the property x of the object o. If o already has an own (non-inherited) property named x, then the assignment simply changes the value of this existing property. Otherwise, the assignment creates a new property named x on the object o. If o previously inherited the property x, that inherited property is now hidden by the newly created own property with the same name.___
* Property assignment examines the prototype chain only to determine whether the assignment is allowed.
* __If o inherits a read-only property named x, for example, then the assignment is not allowed.__
* If the assignment is allowed, however, it always creates or sets a property in the original object and ___never modifies objects in the prototype chain.___
* The fact that inheritance occurs when querying properties but not when setting them is a ___key feature of JavaScript___ because it allows us to selectively override inherited properties:
```javascript
let unitcircle = { r: 1 }; // An object to inherit from
let c = Object.create(unitcircle); // c inherits the property r
c.x = 1; c.y = 1; // c defines two properties of its own
c.r = 2; // c overrides its inherited property
unitcircle.r // => 1: the prototype is not affected
```
# Deleting Properties
* The __delete operator__ removes a property from an object.
```javascript
delete book.author; // The book object now has no author property.
delete book["main title"]; // Now it doesn't have "main title", either.
```
* The __delete__ operator only deletes own properties, not inherited ones.
* A delete expression evaluates to __true if the delete succeeded__ or __if the delete had no effect__ (such as __deleting a nonexistent property__).
* ```delete``` also evaluates to ```true``` when used (meaninglessly) with an expression that is not a property access expression:
```javascript
let o = {x: 1}; // o has own property x and inherits property toString
delete o.x // => true: deletes property x
delete o.x // => true: does nothing (x doesn't exist) but true anyway
delete o.toString // => true: does nothing (toString isn't an own property)
delete 1 // => true: nonsense, but true anyway
```
* In __strict mode__, attempting to delete a non-configurable property ___causes a TypeError.___ In __non-strict
mode__, delete simply ___evaluates to false___ in this case:
```javascript
// In strict mode, all these deletions throw TypeError instead of returning false
delete Object.prototype // => false: property is non-configurable
var x = 1;              // Declare a global variable
delete globalThis.x     // => false: can't delete this property
function f() {}         // Declare a global function
delete globalThis.f     // => false: can't delete this property either
```
* When __deleting configurable properties__ of the global object in non-strict mode, you can __omit the reference__ to the global object and simply __follow the delete operator__ with the property name:
```javascript
globalThis.x = 1; // Create a configurable global property (no let or var)
delete x          // => true: this property can be deleted
```
* In strict mode, however, __delete raises a SyntaxError__ if its operand is an _unqualified identifier like x_, and you have to be explicit about the property access:
```javascript
delete x;            // SyntaxError in strict mode
delete globalThis.x; // This works
```
# Testing Properties
* We can do this with the ```in``` operator, with the ```hasOwnProperty()``` and ```propertyIsEnumerable()``` methods, or simply by querying the property.
```javascript
let o = { x: 1 };
"x" in o // => true: o has an own property "x"
"y" in o // => false: o doesn't have a property "y"
"toString" in o // => true: o inherits a toString property
```
* The ```propertyIsEnumerable()``` refines the ```hasOwnProperty()``` test.
* It __returns true__
only if the named property is an __own property__ and its __enumerable attribute is true.__
```javascript
let o = { x: 1 };
o.propertyIsEnumerable("x")        // => true: o has an own enumerable property x
o.propertyIsEnumerable("toString") // => false: not an own property
Object.prototype.propertyIsEnumerable("toString") // => false: not enumerable
```
* Instead of using the ```in``` operator, it is often sufficient to simply query the property and use ```!==``` to make sure it is not undefined:
```javascript
let o = { x: 1 };
o.x !== undefined        // => true: o has a property x
o.y !== undefined        // => false: o doesn't have a property y
o.toString !== undefined // => true: o inherits a toString property
```
* ```in``` can distinguish between properties that do not exist and properties that exist but have been set to ```undefined```. Consider this code:
```javascript
let o = { x: undefined }; // Property is explicitly set to undefined
o.x !== undefined         // => false: property exists but is undefined
o.y !== undefined         // => false: property doesn't even exist
"x" in o                  // => true: the property exists
"y" in o                  // => false: the property doesn't exist
delete o.x;               // Delete the property x
"x" in o                  // => false: it doesn't exist anymore
```
# Enumerating Properties
* There are a few different ways __to
iterate__ through or obtain a list of all the properties of an object. 
* ___Built-in methods___ that objects inherit are not enumerable, but the properties that your code adds to objects are ___enumerable by default___.
* _For example:_
```javascript
let o = {x: 1, y: 2, z: 3};        // Three enumerable own properties
o.propertyIsEnumerable("toString") // => false: not enumerable
for(let p in o) {   // Loop through the properties
 console.log(p);    // Prints x, y, and z, but not toString
}
```
* To guard against enumerating inherited properties with ```for/in```, you can add an ___explicit check___ inside the loop body:
```javascript
for(let p in o) {
 if (!o.hasOwnProperty(p)) continue;       // Skip inherited properties
}
for(let p in o) {
 if (typeof o[p] === "function") continue; // Skip all methods
}
```
* There are ___four functions___ you can use to get an ___array of property names:___
    * ```Object.keys()``` returns an array of the names of the __enumerable own properties__ of an object. It does __not include non-enumerable__ properties, __inherited__ properties, or properties whose name is a __Symbol__.
    * ```Object.getOwnPropertyNames()``` works like ```Object.keys()``` but returns an array of the names of non-enumerable own properties as well, as long as their names are strings.
    * ```Object.getOwnPropertySymbols()``` returns own properties whose names are Symbols, whether or not they are enumerable.
    * `Reflect.ownKeys()` returns all own property names, both enumerable and non enumerable, and both string and Symbol.
# Property Enumeration Order
* ES6 formally ___defines the order___ in which the own properties of an object are enumerated. 
    *  String properties whose names are ___non-negative integers___ are listed first, in numeric order from smallest to largest. 
    *   After all properties that ___look like array indexes___ are listed, all remaining properties with string names are listed (including properties that look like negative numbers or floating-point numbers). These properties are listed ___in the order in which they were added to the object___.
    *  Finally, the properties whose names are ___Symbol objects___ are listed in the order in which they were added to the object.
# Extending Objects
* A common operation in JavaScript rograms is needing to ___copy the properties of one
object to another object___.
* It is easy to do that with code _like this_:
```javascript
let target = {x: 1}, source = {y: 2, z: 3};
for(let key of Object.keys(source)) {
 target[key] = source[key];
}
target  // => {x: 1, y: 2, z: 3}
```
