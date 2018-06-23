# const

\#programming \#ecmascript \#const \#let \#lexical \#scope 

## TL;DR the TL;DR

- `const` is the new `var`.
- ditch `function fn() {}` for `const fn = () => {}`.
- `const` everywhere.
- no reassignments; ever!


> Table 1 - `reassignment`, `redeclaration`, `hoisting` and `scoping` for `var`, `let` and `const` variables

|		| reassignment | redeclaration | hoisting | scoping        |
|   -   | -            | -             | -        |       -        |
| var	|	yes        |        yes    |    yes   | Variable scope |
| let   |   yes        |		no	   |    no	  | Lexical scope  |
| const |	no         |        no	   |	no	  | Lexical scope  |


## TL;DR.

ES2015 introduced `let` and `const` keywords.  
These works by making **variables** block level.


`let` allows you to declare a variable which can be reassigned;  
`const` allows you do declare variables which cannot be reassigned.  
`var` is old and trusted friend which allows for reassignment, redeclaration and hoisting.


`let` is `{}` scoped variable.  
`const` is `{}` scoped variable.  
`var` is `function(){}` scoped variable.


`let` redeclaration fails with `SyntaxError: Identifier '...' has already been declared`  
`const` reassignment fails with `TypeError: Assignment to constant variable.`  
`var`: *I see no problem in redeclaration or reassignment.*


[Even standard calls them variable.](https://www.ecma-international.org/ecma-262/8.0/index.html#sec-declarations-and-the-variable-statement)

- Why should you use `const`?  
    - Because it is **the new `var`**.  
    - Because reassignment is hard to track.

- Why should your variables not be reassigned?  
    - Every useful processing on data should be named appropriately.  
    - But what about loops?  
        - You don't want to write loops in 2018.  


Now let's look at the definitions from the ECMA-262 standard.

## Standard

According to [ECMA-262 # 13.3 Declarations and the Variable Statement](https://www.ecma-international.org/ecma-262/8.0/index.html#sec-declarations-and-the-variable-statement)

> A `var` statement declares variables that are scoped to the `running execution context`'s `VariableEnvironment`. ...

> `let` and `const` declarations define variables that are scoped to the `running execution context`'s `LexicalEnvironment`. ...


**`const` are variables.**

```javascript
    // assigning a mutable object to person variable.
    const person = { name: 'someone' };
    // allowed operation on mutable object.
    person.name = 'who now?';

    // assigning an immutable object to anubhav variable.
    const anubhav = Object.freeze({ name: 'Anu' });
    // Not an error but, it will fail silently. SILENT FAIL!!!
    anubhav.name = 'this assignment will not be effective';
    anubhav.name === 'Anu' // is true

    // FAILS with Uncaught TypeError: Assignment to constant variable.
    anubhav = person;

```

*`const` are variables* **with immutable bindings.**

This should be enough for you to stop reading here.


## The Long Tail

(incomplete; visit next month for updates)

I am going to further explain why you must use `const` and later only `const`.


### Scoping 

`var` creates variables in \<Variable Scope>.  
`let` creates variables in \<Lexical Scope>.  
`const` creates variables in \<Lexical Scope>.  


`var` not only allows reassignments, it allows redeclaration. It also hoists the variables up.  
`let` allows reassignment, it doesn't allow redeclaration.  
`const` allows neither reassignment nor redeclaration.  


#### Example

Let's look at a simple example:

```javascript

    > var x = 10
    > x
    10
    > var x = 20
    > x
    20


    > let y = 10
    > y
    10
    > let y = 20
    SyntaxError: Identifier 'y' has already been declared


    > const z = 10
    > z
    10
    > const z = 20
    SyntaxError: Identifier 'z' has already been declared


    > y = 20
    20
    > y
    20
    > z = 20
    TypeError: Assignment to constant variable.
    > z
    10

```

This is what happened. When we defined `x` and assigned the value 10. Then, we checked the value, it is 10. After checking the value, we redeclared `x` and assigned it new value of 20. In next line, we check it.

Then we declare `y` and assign it the value 10. We check it to be 10. Then we try to redeclare `y`. This fails with the Error of the type `SyntaxError`. The exact message is `SyntaxError: Identifier 'y' has already been declared`. I am not reassigning as of right now. I will do that later to differentiate with `const` variable.

Next up: declaration and assignment for a `const` variable with value 10. It goes smoothly. A quick check of the value, it has 10, good. Then we try to redeclare it and find the same errror. The exact error message is: `SyntaxError: Identifier 'z' has already been declared`.

Then we try to reassign `y` the value 20; this works. We check it's value to be 20, and it is. Next up is reassignment of variable `z`. This fails; with error of the type `TypeError`. The exact message being `TypeError: Assignment to constant variable.`.

Let's recap quickly.  

> TABLE 0 - tl;dr what you have read so far.

|       | reassignment          | redeclaration      | hoisting          |
|-      |-                      |              -     |         -         |
| var   |          yes          |            Ja      | like a boss       |
| let   |           Ja          | identity crisis    | hard NO           |
| const | confusion intensifies | no-can-do          | no-can-do-aswell  |

Or if you prefer cleaner version for citation:

> Table 1 - `reassignment`, `redeclaration`, `hoisting` and `scoping` for `var`, `let` and `const` variables

|		| reassignment | redeclaration | hoisting | scoping        |
|   -   | -            | -             | -        |       -        |
| var	|	yes        |        yes    |    yes   | Variable scope |
| let   |   yes        |		no	   |    no	  | Lexical scope  |
| const |	no         |        no	   |	no	  | Lexical scope  |


In this document, so far, my attempt has been to let you know two thigs,  
1) difference between `var`, `let`, and `const` in context of `redeclaration`, `reassignment`, `hoisting` and `scoping`.   
2) make you learn it automagically through repetition.


### the new language challenge

There are two kinds of people when it comes to learning new natural language.  
One who care and take time learn mannerisms of new language;  
second, who keep struggling with it forever and have deep accents.

While speaking in natural language is easier since there is no `segfault` in real life; speaking programming language sticking to concepts from older language is recipe for disaster. This makes people want to figure out good and bad parts and write about it.


#### semantics and syntax of new language


When going to a language, you must use ***that*** language's semantics and syntax.

##### natural language

Take German for example, *"Kannst du mir bitte helfen?"* means "Can you please help me?" in English.  
But the verbatim translation is "Can you me please help?".  
Doesn't sound good. And even though you can understand you feel icky as it sounds awkward.


This has nice parallel to programming languages.  


But this creates a problem.  

> People rushing from other langauges assume the workings of the language to be the similar to that of their former language.  

#### The ES rush

Programmers are rushing to EcmaScript from all other languages since ES2011 update.  
A lot of enterprise software is written in ES these days (circa 2018). This is good for ES.  
People rushing from other langauges assume the workings of the language to be the similar to that of their former language.    
ES2015 upgrade has brought a lot of new features.  
These features make EcmaScript look like Java. You can say, there is some Java in JavaScript now.  
Some of these new features are just syntactic sugar and some are really powerful.


One such syntactic sugar-cube is `class`.  
It looks like `Class` from `Java`, `C#` etc.  
Some developers like it, some don't.


`let` and `const` were brought in 2015 version too.  
This has allowed blocks to own variables' and their lifecycle.  
These variables can be Garbage Collected sooner and more memory freed early.  
Thus giving applications more memory.  
And hopefully a snappier feel.


#### when `const` is constant in other languages

Now, in some languages, when you `const` a value, you actually freeze it's value, it's reference and bind reference to the name.  
This makes `const` declarations a constants.  
This is a feature supported by the compiler and the language grammar.


#### `const` is variable in ES

EcmaScript on the other hand, doesn't specify `constant`; it allows for `variable` via `const` keyword.  
This has some programmers throw hands up and refuse to use `const` in their code base at all.


> The difference between constant and a variable?  
Constants don't change in value and variables do.


> The difference between a `const` variable and a `let` variable?  
`let` allows for the reference to the value change; `const` doesn't.

----

### Detour

Now, let's get back to the language and follow-it's-grammar-rules land. "When in Rome, do as Romans do" is not just a cliche; ask anyone who travels a lot. This is an adage to live by.

When you go to Germany, and speak German, you don't speak by English grammar rules, or Chinese grammar rules. You also don't insist that German newspaper should not use words that have different meaning in their native-tongue.

English "bad" is "mies" in German. But German "bad" (das Bad) means the bathroom in English. Now, a Brit cannot declare that German shouldn't have "Bad" in their vocabulary or day-to-day use because majority `(English Speakers / (English + German Speakers))` means "bad" when they say "bad".

German (lang) speaking Brit or English speaking German (person) will have to learn to express thoughts carefully and see that the conversation is not marred by the ambiguity.


#### Aaaand back to `const`

This brings us back to `const`; just because other languages mean something different; doesn't mean that one shouldn't use `const` in ES. Quite the contrary actually, everyone should learn the difference and keep the code cleaner.

------

### The ideal debate

( or the way I hope it goes):

N.B. I am biased in this debate, I'll have my way.

Situation: I wrote code using `const`; this makes me confident that on one will move the variable reference under my feet willy-nilly.


```text

    Reviewer: In this codebase we don't use `const`. Please remove.

    Me: Why is that?

    Reviewer: That has been decided earlier and that's how it is. Please conform to the design principles laid out.

    Me: I understand that. Could you please help me out by letting me know what was the rationale behind it? It would help me explain it to junior and/or future developers.

    Reviewer: We don't use `const` because anybody can still add or even modify object values. Your code wouldn't know it and it might create hard to track problems.

    Me: But we have a competent review process; I am sure a cometent reviewer will catch this.

    Reviewer: True, but mistakes can slip through. Take a look at your spellings for instance, you missed a `p` in second use of the word competent. And `const` gives readers a feel that it is a constant; which it is not and I am sure it is a code smell.

    Me: Thanks for signalling out the typo. But standard doesn't say that `const` means constant object types. In ES, objects can only be frozen using either Object.freeze or via setting modifiable flag in `Object.create()`. `const` is a variable type.

    Reviewer: I don't think so.

    Me: Here's the standard: https://www.ecma-international.org/ecma-262/8.0/index.html#sec-declarations-and-the-variable-statement

    Reviewer: Hmmm, okay. `const` are variables. It seems `const` is new `var`.

    

```

------------

## FAQ


- Why use `const`?
    - It's the new `var`. *Read "`const` is the new `var`".*
    - Variables should not be reassigned or rebound. *Read "The flow of code: Single assignment".*
    - The drawback of `const` that **you can modify object**; exists for `var` and for every other object in EcmaScript.
        - Except frozen objects.
    - Makes variables block scoped; decreases visibility and consequently chances of screwing up.
    - Doesn't hoist variables automatically; you don't have to hoist variables manually. *Read "Hoist Ho".*
    - Even in function declarations. Helps catch bugs as redeclaration of functions can be caught. *Read "Function redefinition".*


- Why use `let`?
    - use `let` when you don't have value available to bind right now.


- Why use `var`?
    - When you hate your co-workers.
    - When you hate clean code.
    - Jeebus, still? I give up!


---------


## `const` is the new `var`

### No difference

#### `var` code

```javascript

    var person = {
        name: {
            first: 'Anu',
            last: 'Saini'
        },
        twitter: 'f0c1s'
    };

    person.preferredLanguage = 'EcmaScript';

```

#### `const` code

```javascript

    const person = {
        name: {
            first: 'Anu',
            last: 'Saini'
        },
        twitter: 'f0c1s'
    };

    person.preferredLanguage = 'EcmaScript';

```

### Difference

#### Reassignment

##### `var` code

```javascript

    var cost = 10;

    if (saturday) {
        cost = 20;
    }

```

##### `const` code

```javascript

    const cost = 10;

    if (saturday) {
        cost = 20; // error
    }

```


#### Scope

##### `var` code

```javascript

    var cost = 10;

    if (saturday) {
        var cost = 20; // same scope; same variable
    }

```

##### `const` code

```javascript

    const cost = 10;

    if (saturday) {
        const cost = 20; // different scope; different variable
    }

```

#### Redeclaration

##### `var` code

```javascript

    var cost = 10;
    var cost = 20; // same scope; same variable; allowed

```

##### `const` code

```javascript

    const cost = 10;
    const cost = 20; // same scope; not allowed: SyntaxError

```

--------

## The flow of code: Single assignment.

Read "Worst possible assignment strategy".

### bad code

```javascript

    const onServiceResponse = (error, response) => {
        if(error) {
            error = new ServiceError(error);
            debug.log(error);
            error = logger(error);
            debug.log(error);
            return callback(error);
        }
        let items = _.get(response, 'body.items');
        items = items.filter(i => i.value > 100).filter(i => ['M', 'P', 'Z'].includes(i.category));
        items = items.map(i => { return { name: i.name, price: i.price } });
        callback(null, items);
    };

    service(params, options, onServiceResponse);

```

### good code

```javascript

    const onServiceResponse = (error, response) => {
        if(error) {
            const serviceError = new ServiceError(error);
            const loggedError = logger(serviceError);
            return callback(loggedError);
        }
        const items = _.get(response, 'body.items');
        const validItems = items.filter(i => i.value > 100).filter(i => ['M', 'P', 'Z'].includes(i.category));
        const displayItems = validItems.map(i => { return { name: i.name, price: i.price } });
        callback(null, displayItems);
    };

    service(params, options, onServiceResponse);

```

------

## Worst possible assignment strategy

This is applicable to `var`, `let`, `const`. None of them can possibly save you from doing this.

```javascript

    const onServiceResponse = (error, response) => {
        if(error) {
            error = new ServiceError(error);
            debug.log(error);
            error = logger(error);
            debug.log(error);
            return callback(error);
        }
        var items = (_items = _.get(response, 'body.items'),
            _items = _items.filter(i => i.value > 100).filter(i => ['M', 'P', 'Z'].includes(i.category)),
            _items = _items.map(i => { return { name: i.name, price: i.price } }),
            _items);
        callback(null, items);
    };

    service(params, options, onServiceResponse);
    
```

### simpler example with literal

```javascript

    var a = (_a = 10, _a = _a + 10, _a = _a * _a, _a);

```

### the real stinker

```javascript

    const person = (_person = {},
        _person['name'] = 'somename',
        _person['aga'] = 100,
        _person);

```

-----

## Hoist Ho!

***Declare variables where you need/use principle.***

### variable hoisting

#### `var` code

```javascript

    function binary (input) {
        return input ? true : false;
    }

    /* variable name is hoisted up; thus no error while console.log(name) the first time */
    function get () {
        var shouldLog = binary(name);
        console.log(name); // logger.log
        var name = 'Anu'; // service.getName();
        var shouldLog = binary(name);
        console.log(name); // logger.log
        return name;
    }

```

#### `const` code

No hoisting; only errors here.

```javascript

    function binary (input) {
        return input ? true : false;
    }

    // no hoist.
    function get () {
        var shouldLog = binary(name);
        console.log(name); // logger.log // error
        const name = 'Anu'; // service.getName(); // declare where need/use principle
        var shouldLog = binary(name);
        console.log(name); // logger.log
        return name;
    }

```

### function hoisting

#### `function` code

It's not that bad though and sometimes needed. This is here to complete the topic of hoisting.

```javascript

    function serviceHandler () {
        console.log(get); // not an error
        get(); // not an error

        function binary (input) {
            return input ? true : false;
        }

        /* variable name is hoisted up; thus no error while console.log(name) the first time */
        function get () {
            return 'Anu';
        }
    }

```

#### `const` code

**No hoisting; only errors here.**

```javascript

    function serviceHandler () {
        console.log(get); // ERROR: ReferenceError: "Uncaught ReferenceError: get is not defined"
        get(); // wouldn't even reach here.

        const binary = input => input ? true : false;

        // no hoist.
        const get =  () => {
            var shouldLog = binary(name);
            console.log(name); // logger.log // error
            const name = 'Anu'; // service.getName(); // declare where need/use principle
            var shouldLog = binary(name);
            console.log(name); // logger.log
            return name;
        };
    }

```

----

## Function redefinition

### `function` way

This can become issue while refactoring. Been there!

```javascript

    function add (a, b) {
        return a + b;
    }

    console.log(add(20, 10));
    
    function add (a, b) {
        return a - b;
    }

    console.log(add(20, 10));

```

Now, if the console reads 30 for the first and 10 for second, then there is a problem;
and, if the console reads 30 for the first and 30 for second, then there is a problem;
and, if the console reads 10 for the first and 10 for second, then there is a problem.

Think about all three cases.


1. Spatial execution; but astute readers will notice that due to function hoisting, this case shouldn't be possible. But, hey language/environment implementations are a thing.
2. Second onward implementations are thrown out.
3. Latest implementation dwarfs/shadows earlier ones. 


### `const` way

```javascript

    const add = (a, b) => a + b;

    console.log(add(20, 10));
    
    const add = (a, b) => a - b; // SyntaxError

    console.log(add(20, 10));

```


---------


## Discussions

Thanks for reading. Please search/create issues to discuss. After creating an issue, please modify this document to reflect the discussion topic below and request a pull.


------

~FIN~
