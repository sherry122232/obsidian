https://howtodoinjava.com/typescript/typescript-introduction/
# Intro

- TypeScript is the **ES6 version of JavaScript + a few other TypeScript-only** features that Angular needs to work.
- **TypeScript is a superset of JavaScript**. It scales JavaScript with datatype support.

# Types

https://rmolinamir.github.io/typescript-cheatsheet/#array
```
$ tsc helloworld.ts //It compile the file into helloworld.js
```

## String:
```
  const myName: string = 'Robert';
```

## Number:
```
  const myAge: number = 24;
```

## Boolean:
```
  const bHasHobbies: boolean = true;
```
Array:

## Object:
```
  let userData: { name: string, age: number } = {
    name: 'Max',
    age: 27
  };
```
## function:
```
  function sayHello(): void {
    console.log('Hello!');
    // return myName; // Not possible because the function can't return anything due to the void assigned type (more on this below).
  }
```

```
  const myMultiply: (val1: number, val2: number) => number;
  // myMultiply = sayHello; // Not possible.
  // myMultiply(); // Not possible.
  myMultiply = multiply;

  console.log(myMultiply(5, 2));
```
## Complex Objects

As you may expect, the assigned types to the `object` key-value pairs can reach high levels of complexity, for example:

```
  let complex: { data: number[], output: (all: boolean) => number[] } = {
    data: [100, 3,99, 10],
    output: function(all: boolean): number[] {
      return this.data
    }
  };
```

# Leetcode
## Array
let myArr1: boolean[]; 
let myArr2: boolean[] = []; 
let myArr3: boolean[] = new Array(); 
let myArr4: boolean[] = Array(); 


```
let flags: boolean[] = [false, false, true]; 
let flags: Array<boolean> = [false, false, true];
```


push: add to the end of the array
pop: remove one from the end of the array
unshift: add one first element
shift: remove the first element
splice: add/remove elements from an array
slice: return shallow copy

### clone
```
let origScores: number[] = [10, 20, 30];
let clonedScores: number[] = [...origScores];
```
### merge 
```
let mergedScore = [...scores1, ...scores2];
```




## Set
const directions = new Set<string>();
const directions = new Set<string>(['east', 'west']);

1. `set.add(v)` – adds the specified value to the `Set`.
2. `set.has(v)` – checks the existence of the specified value in the `Set`.
3. `set.delete(v)` – deletes the specified value from the `Set`.
4. `set.clear()` – clears all the values from the `Set`.
5. `set.size` – ‘`size`‘ property will return the size of `Set`.

numSet.add(1).add(2).add(2);


## Map

let myMap = new Map<string, string>([ ["key1", "value1"], ["key2", "value2"] ]);

1. `**map.set(key, value)**` – adds a new entry in the `Map`.
2. `**map.get(key)**` – retrieves the value for a given key from the `Map`.
3. `**map.has(key)**` – checks if a key is present in the `Map`. Returns _true_ or _false_.
4. `**map.size**` – returns the count of entries in the `Map`.
5. `**map.delete(key)**` – deletes a key-value pair using its key. If key is found and deleted, it returns _true_, else returns _false_.
6. **`map.clear()`** – deletes all entries from the Map.

![[Pasted image 20240424110422.png]]


let [key, value] of nameAgeMapping

