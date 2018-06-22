# Callback functions: named vs anonymous in EcmaScript

## Round 1

```ecmascript

  const sum = (a, b, callback) => callback(a + b)

  function run () {
      console.log(onSum);
      sum(10, 20, onSum = val => console.log(val));
  }

```

Questions:

- Will there be an error or not?
- If `onSum()` threw error will it be in the stack trace or not?


## Round 2

```ecmascript

  const sum = (a, b, callback) => callback(a + b)

  function run () {
      console.log(onSum);
      sum(10, 20, function onSum (val) { console.log(val) } )
  }

```

Questions:

- Will there be an error or not?
- If `onSum()` threw error will it be in the stack trace or not?


## Round 3

```ecmascript

  const sum = (a, b, callback) => callback(a + b)

  function run () {
      console.log(onSum);
      function onSum (val) { console.log(val) }
      sum(10, 20, onSum)
  }

```

Questions:

- Will there be an error or not?
- If `onSum()` threw error will it be in the stack trace or not?
