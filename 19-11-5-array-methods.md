https://www.decipherzone.com/blog-detail/javascript-array

```const fruits = ['banana', 'apple', 'orange', 'watermelon', 'apple', 'orange', 'grape', 'apple'];```

// remove duplicates from array (2 methods to do so)

```const uniqueFruits = Array.from(new Set(fruits));```

```const uniqueFruits2 = [...new Set(fruits)];```

// change a particular value in an array

```fruits.splice(0,2, 'potato', 'tomato');```

// map through array without using .map()

```const friends = [
    { name: 'John', age: 22 },
    { name: 'Peter', age: 23 },
    { name: 'Mark', age: 24 },
    { name: 'Maria', age: 22 },
    { name: 'Monica', age: 21 },
    { name: 'Martha', age: 19 },
]
```

```const friendsNames = Array.from(friends, ({name}) => name);```

// empty an array
```const groceries = ['milk', 'butter', 'napkins'];```
```groceries.length = 0;```

// convert an array to an object
```const veggies = ['onion', 'green pepper', 'carrot', 'broccoli'];```
```const veggiesObj = { ...veggies };```
