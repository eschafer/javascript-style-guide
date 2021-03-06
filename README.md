# JavaScript Style Guide

## Sources
* Maintainable JavaScript by Nicholas Zakas (O’Reilly). Copyright 2012 Nicholas Zakas, 978-1-449-32768-2.
* https://github.com/rwldrn/idiomatic.js
* http://docs.jquery.com/JQuery_Core_Style_Guidelines
* https://github.com/airbnb/javascript

## <a name="TOC">Contents</a>
* [Indentation](#indentation)
* [Line Length](#line-length)
* [Types](#types)
* [Primitive Literals](#primitive-literals)
    * [Strings](#strings)
    * [Numbers](#numbers)
    * [`null`](#null)
* [Operator Spacing](#operator-spacing)
* [Parentheses Spacing](#parentheses-spacing)
* [Object Literals](#object-literals)
* [Comments](#comments)
    * [Single-Line Comments](#single-line-comments)
    * [Multiline Comments](#multiline-comments)
* [Variable Declarations](#variable-declarations)
* [Function Declarations](#function-declarations)
* [Naming](#naming)
* [Strict Mode](#strict-mode)
* [Assignments](#assignments)
* [Equality Operators](#equality-operators)
* [Ternary Operator](#ternary-operator)
* [Statements](#statements)
    * [Simple Statements](#simple-statements)
    * [`return` Statement](#return-statement)
    * [Compound Statements](#compound-statements)
    * [`if` Statement](#if-statement)
    * [`for` Statement](#for-statement)*
    * [`while` Statement](#while-statement)
    * [`do` Statement](#do-statement)
    * [`switch` Statement](#switch-statement)
    * [`try` Statement](#try-statement)
* [jQuery](#jquery)
* [Type Checking](#type-checking)*
* [`this`](#this)
* [Early Returns](#early-returns)
* [White Space](#white-space)
* [Things to Avoid](#things-to-avoid)
* [JSHint](#jshint)*

\* Still need to make some changes.

## <a name="indentation">Indentation</a>

Each indentation level is made up of one tab. Do not use spaces.

If alignment is necessary (which shouldn't be common), use tabs for indentation and spaces for alignment.

```javascript
// Good
if (true) {
	doSomething();
}
```

**[[⬆]](#TOC)**

## <a name="line-length">Line Length</a>

Each line should be no longer than 80 characters, but slightly longer lines are permitted for readability. If a line goes longer than 80 characters, it should be wrapped after an operator (comma, plus, etc.). The following line should be indented two levels.

```javascript
// Good
doSomething(argument1, argument2, argument3, argument4, argument5, argument6,
		argument7);

// Bad: Following line only indented one level
doSomething(argument1, argument2, argument3, argument4, argument5, argument6,
	argument7);

// Bad: Breaking before operator
doSomething(argument1, argument2, argument3, argument4, argument5, argument6
		, argument7);
```

**[[⬆]](#TOC)**

## <a name="types">Types</a>

* **Primitives**: When you access a primitive type you work directly on its value.
    * `String`
    * `Number`
    * `Boolean`
    * `null`
    * `undefined`

    ```javascript
    var foo = 1;
    var bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```
* **Complex**: When you access a complex type you work on a reference to its value.

    * `Object`
    * `Array`
    * `Function`

    ```javascript
    var foo = [1, 2];
    var bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```

**[[⬆]](#TOC)**

## <a name="primitive-literals">Primitive Literals</a>

### <a name="strings">Strings</a>

Strings should always use double quotes (never single quotes) and should always appear on a single line. Never use a slash to create a new line in a string - use string concatenation instead.

```javascript
// Good
var name = "Elizabeth";

// Bad: Single quotes
var name = 'Elizabeth';

// Good: String concatenation
var longString = "Lorem ipsum dolor sit amet, consectetuer adipiscing elit, " +
		"sed diam nonummy nibh euismod";

// Bad: Wrapping to second line
var longString = "Lorem ipsum dolor sit amet, consectetuer adipiscing elit, \
sed diam nonummy nibh euismod";
```

### <a name="numbers">Numbers</a>

Numbers should be written as decimal integers, e-notation integers, hexadecimal integers, or floating-point decimals with at least one digit before and one digit after the decimal point. Never use octal literals.

```javascript
// Good
var count = 10;

// Good
var price = 10.0;
var price = 10.00;

// Good
var num = 0xA2;

// Good
var num = 1e23;

// Bad: Hanging decimal point
var price = 10.;

// Bad: Leading decimal point
var price = .1;

// Bad: Octal (base 8) is deprecated
var num = 010;
```

### <a name="null">`null`</a>

The special value `null` should be used only in the following situations:

* To initialize a variable that may later be assigned an object value
* To compare against an initialized variable that may or may not have an object value
* To pass into a function where an object is expected
* To return from a function where an object is expected

Examples:

```javascript
// Good
var person = null;

// Good
function getPerson() {
	if (condition) {
		return new Person("Elizabeth");
	} else {
		return null;
	}
}

// Good
var person = getPerson();
if (person !== null) {
	doSomething();
}

// Bad: Testing against uninitialized variable
var person;
if (person !== null) {
	doSomething();
}

// Bad: Testing to see if an argument was passed
function doSomething(arg1, arg2, arg3, arg4) {
	if (arg4 !== null) {
		doSomethingElse();
	}
}
```

**[[⬆]](#TOC)**

## <a name="operator-spacing">Operator Spacing</a>

Operators with two operands must be preceded and followed by a single space to make the expression clear. Operators include assignments and logical operators.

```javascript
// Good
var found = (values[i] === item);

// Good
if (found && (count > 10)) {
	doSomething();
}

// Good
for (i = 0; i < count; i++) {
	process(i);
}

// Bad: Missing spaces
var found = (values[i]===item);

// Bad: Missing spaces
if (found&&(count>10)) {
	doSomething();
}

// Bad: Missing spaces
for (i=0; i<count; i++) {
	process(i);
}
```

**[[⬆]](#TOC)**

## <a name="parentheses-spacing">Parentheses Spacing</a>

When parentheses are used, there should be no white space immediately after the opening parenthesis or immediately before the closing parenthesis.

```javascript
// Good
var found = (values[i] === item);

// Good
if (found && (count > 10)) {
	doSomething();
}

// Good
for (i = 0; i < count; i++) {
	process(i);
}

// Bad: Extra space after opening paren
var found = ( values[i] === item);

// Bad: Extra space before closing paren
if (found && (count > 10) ) {
	doSomething();
}

// Bad: Extra space around argument
for (i = 0; i < count; i++) {
	process( i );
}
```

**[[⬆]](#TOC)**

## <a name="object-literals">Object Literals</a>

Object literals should have the following format:
* The opening brace should be on the same line as the containing statement.
* Each property-value pair should be indented one level with the first property appearing on the next line after the opening brace.
* Each property-value pair should have an unquoted property name, followed by a colon (no space preceding it), followed by the value.
* If the value is a function, it should wrap under the property name and should have a blank line both before and after the function.
* Additional empty lines may be inserted to group related properties or otherwise improve readability.
* The closing brace should be on a separate line.

Examples:

```javascript
// Good
var object = {

	key1: value1,
	key2: value2,

	func: function() {
		// do something
	},

	key3: value3
};

// Bad: Improper indentation
var object = {
				key1: value1,
				key2: value2
			};

// Bad: Missing blank lines around function
var object = {

	key1: value1,
	key2: value2,
	func: function() {
		// do something
	},
	key3: value3
};
```

When an object literal is passed to a function, the opening brace should be on the same line as if the value is a variable. All other formatting rules listed earlier still apply.

```javascript
// Good
doSomething({
	key1: value1,
	key2: value2
});

// Bad: All on one line
doSomething({ key1: value1, key2: value2 });
```

**[[⬆]](#TOC)**

## <a name="comments">Comments</a>

Make frequent use of comments to aid others in understanding your code. Use comments when:
* Code is difficult to understand.
* The code might be mistaken for an error.
* Browser-specific code is necessary but not obvious.
* Documentation generation is necessary for an object, method, or property (use appropriate documentation comments).

### <a name="single-line-comments">Single-Line Comments</a>

Single-line comments should be used to document one line of code or a group of related lines of code. A single-line comment may be used on a separate line, describing the code beneath it.

A single-line comment should be at the same indentation level as the code it describes and be preceded by a single line. Never use multiple single-line comments on consecutive lines; use a multiline comment instead.  Do not use end-of-line comments.

```javascript
// Good
if (condition) {

	// if you made it here, then all security checks passed
	allowed();
}

// Bad: No empty line preceding comment
if (condition) {
	// if you made it here, then all security checks passed
	allowed();
}

// Bad: Wrong indentation
if (condition) {
// if you made it here, then all security checks passed
	allowed();
}

// Bad: This should be a multiline comment
// This next piece of code is quite difficult, so let me explain.
// What you want to do is determine if the condition is true
// and only then allow the user in. The condition is calculated
// from several different functions and may change during the
// lifetime of the session.
if (condition) {

	// if you made it here, then all security checks passed
	allowed();
}

// Bad: End-of-line comment
var result = something + somethingElse; // somethingElse will never be null
```

### <a name="multiline-comments">Multiline Comments</a>

Multiline comments should be used to document code that requires more explanation. Each multiline comment should have at least three lines:

1. The first line contains only the `/*` comment opening. No further text is allowed on this line.
2. The next line or lines have a `*` aligned with the `*` in the first line. Text is allowed on these lines.
3. The last line has the `*/` comment opening aligned with the preceding lines. No other text is allowed on this line.

The first line of multiline comments should be indented to the same level as the code it describes. Each subsequent line should have the same indentation plus one space (for proper alignment of the `*` characters). Each multiline comment should be preceded by one empty line.

```javascript
// Good
if (condition) {

	/*
	 * if you made it here,
	 * then all security checks passed
	 */
	allowed();
}

// Bad: No empty line preceding comment
if (condition) {
	/*
	 * if you made it here,
	 * then all security checks passed
	 */
	allowed();
}

// Bad: Missing a space after asterisk
if (condition) {
	/*
	 *if you made it here,
	 *then all security checks passed
	 */
	allowed();
}

// Bad: Wrong indentation
if (condition) {

/*
 * if you made it here,
 * then all security checks passed
 */
	allowed();
}

// Bad: Don't use end-of-line comments
var result = something + somethingElse; /* somethingElse will never be null */
```

## <a name="variable-declarations">Variable Declarations</a>

All variables should be declared before they are used. Variable declarations should take place at the beginning of a function using multiple `var` statements, with one variable per line. Variables should be initialized when declared if applicable. Initialized variables should come first followed by uninitialized variables. Do not align variable names, the equals operator, or values.

```javascript
// Good
var count = 10;
var name = "Elizabeth";
var found = false;
var empty;

// Bad: Improper initialization alignment
var count   = 10;
var name    = "Elizabeth";
var found   = false;
var empty;

// Bad: Multiple declarations on one line
var count = 10, name = "Elizabeth";
var found = false, empty;

// Bad: Uninitialized variables first
var empty;
var count = 10;
var name = "Elizabeth";
var found = false;

// Bad: Single var statement
var count   = 10,
    name    = "Elizabeth",
    found   = false,
    empty;
```

Always declare variables. Implied globals should not be used.

**[[⬆]](#TOC)**

## <a name="function-declarations">Function Declarations</a>

Functions should be declared before they are used. When a function is not a method (that is, not attached to an object), it should be defined using the function declaration format (not function expression format or using the `Function` constructor). There should be no space between the function name and the opening parenthesis. There should be one space between the closing parenthesis and the right brace. The right brace should be on the same line as the `function` keyword. There should be no space after the opening parenthesis or before the closing parenthesis. Named arguments should have a space after the comma but not before it. The function body should be indented one level.

```javascript
// Good
function doSomething(arg1, arg2) {
	return arg1 + arg2;
}

// Bad: Improper spacing of first line
function doSomething (arg1, arg2){
	return arg1 + arg2;
}

// Bad: Function expression
var doSomething = function(arg1, arg2) {
	return arg1 + arg2;
};

// Bad: Left brace on wrong line
function doSomething(arg1, arg2)
{
	return arg1 + arg2;
}

// Bad: Using Function constructor
var doSomething = new Function("arg1", "arg2", "return arg1 + arg2");
```

Functions declared inside of other functions should be declared immediately after the `var` statements.

```javascript
// Good
function outer() {

	var count = 10;
	var name = "Elizabeth";
	var found = false;
	var empty;

	function inner() {
		// code
	}

	// code that uses inner()
}

// Bad: Inner function declared before variables
function outer() {

	function inner() {
		// code
	}

	var count = 10;
	var name = "Elizabeth";
	var found = false;
	var empty;

	// code that uses inner()
}
```

Anonymous functions may be used for assignment of object methods or as arguments to other functions. There should be no space between the `function` keyword and the opening parenthesis.

```javascript
// Good
object.method = function() {
	// code
};

// Bad: Incorrect spacing
object.method = function () {
	// code
};
```

Immediately invoked functions should surround the entire function call with parentheses.

```javascript
// Good
var value = (function() {

	// function body

	return {
		message: "Hi"
	}
}());

// Bad: No parentheses around function call
var value = function() {

	// function body

	return {
		message: "Hi"
	}
}();

// Bad: Improper parentheses placement
var value = (function() {

	// function body

	return {
		message: "Hi"
	}
})();
```

**[[⬆]](#TOC)**

## <a name="naming">Naming</a>

Care should be taken to name variables and functions properly. Names should be limited to alphanumeric characters and, in some cases, the underscore character. Do not use the dollar sign (`$`) or backslash (`\`) characters in any other names (with the exception of [jQuery object variables](#jquery));

Variable names should be formatted in camel case with the first letter lowercase and the first letter of each subsequent word uppercase. The first word of a variable name should be a noun (not a verb) to avoid confusion with functions. Do not use underscores in variable names.

```javascript
// Good
var accountNumber = "8401-1";

// Bad: Begins with uppercase letter
var AccountNumber = "8401-1";

// Bad: Begins with verb
var getAccountNumber = "8401-1";

// Bad: Uses underscore
var account_number = "8401-1";
```

Function names should also be formatted using camel case. The first word of a function name should be a verb (not a noun) to avoid confusion with variables. Do not use underscores in function names.

```javascript
// Good
function doSomething() {
	// code
}

// Bad: Begins with uppercase letter
function DoSomething() {
	// code
}

// Bad: Begins with noun
function car() {
	// code
}

// Bad: Uses underscores
function do_something() {
	// code
}
```

Constructor functions---functions used with the `new` operator to create new objects---should be formatted in camel case but must begin with an uppercase letter. Constructor function names should begin with a nonverb, because `new` is the action of creating an object instance.

```javascript
// Good
function MyObject() {
	// code
}

// Bad: Begins with lowercase letter
function myObject() {
	// code
}

// Bad: Uses underscores
function My_Object() {
	// code
}

// Bad: Begins with verb
function getMyObject() {
	// code
}
```

Variables that act as constants (values that won't be changed) should be formatted using all uppercase letters with words separated by a single underscore.

```javascript
// Good
var TOTAL_COUNT = 10;

// Bad: Camel case
var totalCount = 10;

// Bad: Mixed case
var total_COUNT = 10;
```

Object properties follow the same naming conventions as variables. Object methods follow the same naming conventions as functions. If a property or method is meant to be private, then it should be prefixed with an underscore character.

```javascript
// Good
var object = {
	_count: 10,

	_getCount: function() {
		return this._count;
	}
};
```

**[[⬆]](#TOC)**

## <a name="strict-mode">Strict Mode</a>

Strict mode should be used only inside of functions, never globally.

```javascript
// Bad: Global strict mode
"use strict";

function doSomething() {
	// code
}

// Good
function doSomething() {
	"use strict";

	// code
}
```

If you want strict mode to apply to multiple functions without needing to write `"use strict"` multiple times, use immediate function invocation:

```javascript
// Good
(function() {
	"use strict";

	function doSomething() {
		// code
	}

	function doSomethingElse() {
		// code
	}
}());
```

**[[⬆]](#TOC)**

## <a name="assignments">Assignments</a>

When assigning a value to a variable, use parentheses around a right-side expression that contains a comparison.

```javascript
// Good
var flag = (i < count);

// Bad: Missing parentheses
var flag = i < count;
```

**[[⬆]](#TOC)**

## <a name="equality-operators">Equality Operators</a>

Use `===` and `!==` instead of `==` and `!=` to avoid type coercion errors.

```javascript
// Good
var same = (a === b);

// Bad: Using ==
var same = (a == b);
```

**[[⬆]](#TOC)**

## <a name="ternary-operator">Ternary Operator</a>

The ternary operator should be used only for assigning values conditionally and never as a shortcut for an `if` statement.

```javascript
// Good
var value = condition ? value1 : value2;

// Bad: no assignment, should be an if statement
condition ? doSomething() : doSomethingElse();
```

**[[⬆]](#TOC)**

## <a name="statements">Statements</a>

### <a name="simple-statements">Simple Statements</a>

Each line should contain at most one statement. All simple statements should end with a semicolon (`;`).

```javascript
// Good
count++;
a = b;

// Bad: Multiple statements on one line
count++; a = b;
```

### <a name="return-statement">`return` Statement</a>

A `return` statement with a value should not use parentheses unless they make the return value more obvious in some way. Example:

```javascript
// Good
return;

// Good
return collection.size();

// Good
return (size > 0 ? size : defaultSize);
```

### <a name="compound-statements">Compound Statements</a>

Compound statements are lists of statements enclosed inside of braces.
* The enclosed statements should be indented one more level than the compound statement.
* The opening brace should be at the end of the line that begins the compound statement; the closing brace should begin a line and be indented to the beginning of the compound statement.
* Braces are used around all statements, even single statements, when they are part of a control structure, such as an `if` or `for` statement. This convention makes it easier to add statements without accidentally introducing bugs by forgetting to add braces.
* The statement beginning keyword, such as `if`, should be followed by one space, and the opening brace should be preceded by a space.

### <a name="if-statement">`if` Statement</a>

The `if` class of statements should have the following form:

```javascript
// Good
if (condition) {
	// statements
}

// Good
if (condition) {
	// statements
} else {
	// statements
}

// Good
if (condition) {
	// statements
} else if (condition) {
	// statements
} else {
	// statements
}
```

It is never permissible to omit the braces in any part of an `if` statement.

```javascript
// Good
if (condition) {
	doSomething();
}

// Bad: Improper spacing
if(condition) {
	doSomething();
}

// Bad: Missing braces
if (condition)
	doSomething();

// Bad: All on one line
if (condition) { doSomething(); }

// Bad: All on one line without braces
if (condition) doSomething();
```

### <a name="for-statement">`for` Statement</a>

The `for` class of statements should have the following form:

```javascript
// Good
for (initialization; condition; update) {
	// statements
}

// Good
for (variable in object) {
	// statements
}
```

Variables should not be declared in the initialization section of a `for` statement.

> Not sure I agree with this.

```javascript
// Good
var i;
var len;

for (i = 0, len = 10; i < len; i++) {
	// code
}

// Bad: Variables declared during initialization
for (var i = 0, len = 10; i < len; i++) {
	// code
}

// Bad: Variables declared during initialization
for (var prop in object) {
	// code
}
```

When using a `for-in` statement, double-check if you need to use `hasOwnProperty()` to filter out object members.

### <a name="while-statement">`while` Statement</a>

The `while` class of statements should have the following form:

```javascript
// Good
while (condition) {
	// statements
}
```

### <a name="do-statement">`do` Statement</a>

The `do` class of statements should have the following form:

```javascript
// Good
do {
	// statements
} while (condition);
```

Note the use of a semicolon as the final part of this statement. There should be a space before and after the `while` keyword.

### <a name="switch-statement">`switch` Statement</a>

The `switch` class of statements should have the following form:

```javascript
// Good
switch (expression) {
	case expression:
		// statements

	default:
		// statements
}
```

Each `case` is indented one level under the `switch`. Each `case` after the first, including `default`, should be preceded by a single empty line.

Each group of statements (except the default) should end with `break`, `return`, `throw`, or a comment indicating fall-through.

```javascript
// Good
switch (value) {
	case 1:
		// falls through

	case 2:
		doSomething();
		break;

	case 3:
		return true;

	default:
		throw new Error("This shouldn't happen.");
}
```

If a `switch` doesn't have a `default` case, then it should be indicated with a comment.

```javascript
// Good
switch (value) {
	case 1:
		// falls through

	case 2:
		doSomething();
		break;

	case 3:
		return true;

	// no default
}
```

### <a name="try-statement">`try` Statement</a>

The `try` class of statements should have the following form:

```javascript
// Good
try {
	// statements
} catch (variable) {
	// statements
}

// Good
try {
	// statements
} catch (variable) {
	// statements
} finally {
	// statements
}
```

**[[⬆]](#TOC)**

## <a name="white-space">White Space</a>

Blank lines improve readability by setting off sections of code that are logically related. Two blank lines should always be used in the following circumstances:
* Between sections of a source file
* Between class and interface definitions

One blank line should always be used in the following circumstances:
* Between methods
* Between the local variables in a method and its first statement
* Before a multiline or single-line comment
* Between logical sections inside a method to improve readability

Blank spaces should be used in the following circumstances:
* A keyword followed by a parenthesis should be separated by a space.
* A blank space should appear after commas in argument lists.
* All binary operators except dot (`.`) should be separated from their operands by spaces. Blank spaces should never separate unary operators such as unary minus, increment (`++`), and decrement (`--`) from their operands.
* The expressions in a `for` statement should be separated by blank spaces.

**[[⬆]](#TOC)**

## <a name="jquery">jQuery</a>

* Prefix jQuery object variables with a `$`.

    ```javascript
    // bad
    var sidebar = $(".sidebar");

    // good
    var $sidebar = $(".sidebar");
    ```

* Cache jQuery lookups.

    ```javascript
    // bad
    function setSidebar() {
      $(".sidebar").hide();

      // ...stuff...

      $(".sidebar").css({
        "background-color": "pink"
      });
    }

    // good
    function setSidebar() {
      var $sidebar = $(".sidebar");
      $sidebar.hide();

      // ...stuff...

      $sidebar.css({
        "background-color": "pink"
      });
    }
    ```

**[[⬆]](#TOC)**

## <a name="type-checking">Type Checking</a>

* String: `typeof object === "string"`
* Number: `typeof object === "number"`
* Boolean: `typeof object === "boolean"`
* Object: `typeof object === "object"`
* Plain Object: `jQuery.isPlainObject(object)`
* Function: `jQuery.isFunction(object)`
* Array: `jQuery.isArray(object)`
* Element: `object.nodeType`
* `null`: `object === null`
* `null` or `undefined`: `object == null`
* `undefined`:
    * Global Variables: `typeof variable === "undefined"`
    * Local Variables: `variable === undefined`
    * Properties: `object.prop === undefined`

**[[⬆]](#TOC)**

## <a name="this">`this`</a>

Beyond the generally well known use cases of `call` and `apply`, always prefer `.bind(this)` or a functional equivalent, for creating `BoundFunction` definitions for later invocation. Only resort to aliasing when no preferable option is available.

```javascript
function Device(options) {
	this.value = null;

	// open an async stream,
	// this will be called continuously
	stream.read(options.path, function(data) {

		// Update this instance's current value
		// with the most recent value from the
		// data stream
		this.value = data;
	}.bind(this));

	// Throttle the frequency of events emitted from
	// this Device instance
	setInterval(function() {

		// Emit a throttled event
		this.emit("event");
	}.bind(this), options.frequency || 100);
}

// Just pretend we've inherited EventEmitter ;)
```

When unavailable, functional equivalents to `.bind` exist in many modern JavaScript libraries.

```javascript

// eg. lodash/underscore, _.bind()
function Device(options) {
	this.value = null;
	
	stream.read(options.path, _.bind(function(data) {
		this.value = data;
	}, this));

	setInterval(_.bind(function() {
		this.emit("event");
	}, this), options.frequency || 100);
}

// eg. jQuery.proxy
function Device(options) {
	this.value = null;
	
	stream.read(options.path, jQuery.proxy(function(data) {
		this.value = data;
	}, this));
	
	setInterval(jQuery.proxy(function() {
		this.emit("event");
	}, this), options.frequency || 100);
}
```

As a last resort, create an alias to `this` using `that` as an identifier. This is extremely bug prone and should be avoided whenever possible.

```javascript
function Device(options) {
	var that = this;
	this.value = null;
	
	stream.read(options.path, function(data) {
		that.value = data;
	});

	setInterval(function() {
		that.emit("event");
	}, options.frequency || 100);
}
```

**[[⬆]](#TOC)**

## <a name="early-returns">Early Returns</a>

Early returns promote code readability with negligible performance difference.

```javascript
// Bad:
function returnLate(foo) {
	var value;

	if (foo) {
		value = "foo";
	} else {
		value = "quux";
	}

	return value;
}

// Good:
function returnEarly(foo) {

	if (foo) {
		return "foo";
	}

	return "quux";
}
```

**[[⬆]](#TOC)**

## <a name="jshint">JSHint</a>

http://jshint.com/

**[[⬆]](#TOC)**

## <a name="things-to-avoid">Things to Avoid</a>

* Never use the primitive wrapper types, such as `String`, to create new objects.
* Never use `eval()`.
* Never use the `with` statement. This statement isn't available in strict mode and likely won't be available in future ECMAScript editions.

**[[⬆]](#TOC)**
