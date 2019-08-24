### Array.from()

```
// script.js

const testString = 'Hello, it is very nice to meet you.';
const strAlphabet = 'abcdefghijklmnopqrstuvwxyz';
const strNumbers = '123456789';
let testArr = ['Red', 'Blue', 'Purple', 'Brown', 'Pink'];
let testArrNum = [8,6,7,5,3,0,9];

const testButton = () => {
  arrFrom2(testString);
}

// Array.from() method creates a new, shallow-copied Array instance from an array-like or iterable object.
// like a string...
const arrFrom1 = (str) => {
  const arr = Array.from(str);
  console.log('arr', arr);
}

// and you can map through them too 
const arrFrom2 = (str) => {
  const arr = Array.from(str, x => x + x);
  console.log('arr', arr);
}
```

```
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <button onClick="testButton()">Test Button</button>
  <script src="script.js"></script>
</body>
</html>
```
