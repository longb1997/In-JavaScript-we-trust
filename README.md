In JS we trust - The best way to learn is by building/coding and teaching. I create the challenges to help my friends learn JavaScript and in return it helps me embrace the language in much deeper level. Feel free to clone, fork and pull.

---

###### 1. What's the output?

```javascript
function a(x){
  x++;
  return function(){
  console.log(++x)
  }
}

a(1)();
a(1)();
a(1)();

let x = a(1);
x();
x();
x();
```

- A: `1, 2, 3` and `1, 2, 3`
- B: `3, 3, 3` and `3, 4, 5`
- C: `3, 3, 3` and `1, 2, 3`
- D: `1, 2, 3` and `3, 3, 3`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

This question reminds us about Closure in JS. Closure allows us to create a `stateful function` and such function can access to variable outside of its scope. In a nutshell, a closure can have access to `global` variable (scope), `father function` scope and `its` own scope.

We have here 3, 3, 3 and 3, 4, 5 because first we simply call the function `a()`. It works like a normal function and we do not see something `stateful` here. In later case, we declare a variable `x` and it stores the value of function `a(1)`, that is why we get 3. 4. 5 rather than 3, 3, 3.

This kind of gotcha gives me the feeling of `static` variable in PHP world.
</p>
</details>

---
###### 2. What's the output?

```javascript
function Name(a, b){
  this.a = a;
  this.b = b;
}

const me = Name("Vuong", "Nguyen);

console.log(!(a.length - window.a.length));
```

- A: `undefined`
- B: `NaN`
- C: `true`
- D: `false`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

We get true in the console. The tricky part is when we create an object from the constructor function Name but we DO NOT USE `new` keywork. That makes the variable `a` global one and get the value "Vuong". Remember that it is actually a property of the global object `window` (in the browser) or `global` in the nodejs. 

We then get `a.length` ~ 5 and `window.a.length` ~ 5 which return 0. !0 returns true.

Imagine what would happen when we create the instance `me` with the `new` keywork. That is an interesting inquire!
</p>
</details>

---
###### 3. What's the output?

```javascript
const x = function (...x){
  let k = (typeof x).length;
  let y = ()=> "freetut".length;
  let z = {y:y};
  return k - z.y();
  
};

console.log(Boolean(x()))
```

- A: `true`
- B:  1
- C: -1
- D: `false`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The spread operator `...x` might help us obtain the parameter in the function in the form of array. Yet, in Javascript the typeof array return "object" rather than "array". It is totally odd if you are coming from PHP.

That is said, we now have the length of the string `object` which returns 6. z.y() simply returns the length of the string 'freetut' (7). 

Be aware that the function x() (in the form of `function express` or `anonymous function` (if you are coming from PHP) return -1 when being called and when converted to bool with `Boolean(-1)` return true instead of false. Noted that `Boolean(0)` return false.
</p>
</details>


---
###### 4. What's the output?

```javascript
(function js(x){
   
   const y = (j) => j*x;
   
   console.log(y(s()))
   
   function s(){
     return j();
   }
  
   function j(){
     return x**x;
   }
  
})(3);
```

- A: `undefined`
- B:  18
- C:  81
- D:  12

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C
The function `js()` can be automatically executed without calling it and known as IIFE (Immediately Invoked Function Expression). Noted the parameter `x` of the function `js` is actuallly passed with the value 3.

The value return of the function is y(s())), meaning calling three other functions `y()`, `s()` and `j()` because the function `s()` returns `j()`. 

j() returns 3^3 = 27 so that s() returns 27.

y(s()) means y(27) which returns 27*3 = 81.

Note that we can call `declare function` BEFORE the function is actually declared but not with `expression function`.
</p>
</details>


---
###### 5. What's the output?

```javascript

var tip = 100;

(function () {
    
  console.log("I have $" + husband());
  
  function wife(){
    return tip*2;
  }
  
  function husband(){
    return wife()/2;
  }
  
  var tip = 10;
  
})();
```

- A:  "I have $10";
- B:  "I have $100";
- C:  "I have $50";
- D:  "I have $NaN";

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D
We have here an IIFE (Immediately Invoked Function Expression). It means we do not have to call it but it will be excuted automatically when declared. The flow is as: husband() returns wife()/2 and wife() returns tip*2. 

We might think that tip = 100 because it is a global variable when declaring with `var` keyword. However, it is actually `undefined` because we also have `var tip = 10` INSIDE the function. As the variable `tip` is hoisted with default value `undefined`, the final result would be D. We know that `undefined` returns NaN when we try to divide to 2 or multiple with 2.

If we do not re-declare `var tip = 10;` at the end of the function, we will definately get D.

JS is fun, right?

</p>
</details>


---
###### 6. What's the output?

```javascript

const js = { language: "loosely type", label: "difficult" };

const edu = {...js, level: "PhD"};

const newbie = edu;

delete edu.language;

console.log(Object.keys(newbie).length);
```

- A:  2;
- B:  3;
- C:  4;
- D:  5;

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

This challenge revises the ES6's feature regarding `spread operator ...` Spread operator is quite useful for retrieving parameter in function, to `unite` or `combine` object and array in JavaScript. PHP also has this feature.

In the variable `edu`, we use `...js` (spread operator here) to combine both objects into one. It works in the same way with array.

Then we declare another variable named `newbie`. IMPORTANT note: By declaring the variable like that, both variables point to the SAME POSITION in the memory. We may have known something like `$a = &$b` in PHP, which let both varibles work in the same way. We might have known about `pass by reference` in the case.

Then we have 2 as `edu.language` is deleted. Both objects now have only two elements.

Now is time to think about coping an object in JS either shallow or deep one.
</p>
</details>

---
###### 7. What's the output?

```javascript
var candidate = {
	name : 'Vuong',
	age  : 30
}

var job = {
	frontend : 'Vuejs or Reactjs',
	backend : 'PHP and Laravel',
	city : 'Auckland'
} 

class Combine{
  static get(){
    return Object.assign(candidate, job)
  }
  
  static count(){    
    return Object.keys(this.get()).length;
  }
}

console.log(Combine.count());
```

- A:  5;
- B:  6;
- C:  7;
- D:  8;

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The buit-in method `Object.assign(candidate, job)` merges the two objects `candidate` and `job` into one object. Then the method `Object.keys` counts the number of `key` in the object.

Note that two methods `get()` and `count()` are defined as `static`, so they need to be called statically using `Class.staticmethod()` syntax. Then the final object get 5 elements.

</p>
</details>

---
###### 8. What's the output?

```javascript
var x = 1;

(()=> {x += 1; ++x})();
((y)=> {x +=y; x = x%y;})(2);
(()=> x += x)();
(()=> x *= x)();

console.log(x);
```

- A:  4;
- B:  50;
- C:  2;
- D:  10;

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

Initially `x` is declared with the value 1. In the first IIFE function, there are two operations. First `x` becomes 2 and then 3.

In the second IIFE function, `x = x + y` then the current value is 5. In the second operation, it returns only 1 as it undergoes `5%2`.

In the third and fouth IIFE functions, we get 2 `x = x + x` and then 4 `x = x * x`. It is more than simple.

</p>
</details>


---
###### 9. What's the output?

```php
$var = 10;
$f = function($let)use($var){
    return ++$let + $var;
};

$var = 15;
echo $f(10);
```

```javascript
var x = 10;

const f = (l) => ++l + x;
;

x = 15;
console.log(f(10));
```

- A:  26 and 26;
- B:  21 and 21;
- C:  21 and 26;
- D:  26 and 21;

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

This question illustrates the diffences between PHP and JavaScript when handling closure. In the first snippet, we declare a closure with the keyword `use`. Closure in PHP is simply an anonymous function and the data is passed to the function using the keyword `use`. Otherwise, it is called as `lambda` when we do not use the keyword `use`. You can check the result of the snippet here https://3v4l.org/PSeMY. PHP `closure` only accepts the value of the variable BEFORE the closure is defined, no matter where it is called. As such, `$var` is 10 rather than 15.

On the contrary, JavaScript treats the variable a bit different when it is passed to anonymous function. We do not have to use the keyword `use` here to pass variable to the closure. The variable `x` in the second snippet is updated before the closure is called, then we get 26.

Note that in PHP 7.4, we have arrow function and we then do not have to use the keyword `use` to pass the variable to function. Another way to call a `global` ariable inside a function in PHP is to use the keyword `global` or employ the built-in GLOBAL variable $GLOBALS.

</p>
</details>

---
###### 10. What's the output?

```javascript
let x = {};
let y = {};
let z = x;

console.log(x == y);
console.log(x === y);
console.log(x == z);
console.log(x === z);
```

- A:  true    true    true    true;
- B:  false   false   false   false;
- C:  true    true    false   false;
- D:  false   false   true    true;

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

Technically, `x` and `y` have the same value. Both are empty objects. However, we do not use the value to compare objects.

`z` is `x` are two objects referring to the same memory position. In JavaScript, array and object are passed by `reference`. `x` and `z` therefore return true when being compared.

</p>
</details>


---
###### 11. What's the output?

```javascript
console.log("hello");

setTimeout(()=>console.log("hey"), 1);
setTimeout(()=>console.log("kiora"), 2);
setTimeout(()=>console.log("world"), 0);

console.log("hi");
```

- A:  "hello" "hey" "kiora" "world" "hi"
- B:  "hello" "hi"  "hey"   "kiora" "world"
- C:  "hello" "hi"  "world" "hey"   "kiora"
- D:  "hello" "hi"  "hey"   "world" "kiora"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

Given that three setTimeout() functions will be kept in the `task queue` before jumping back to `stack`, "hello" and "hi" will be printed first, then A is totally incorrect.

We might have the feeling that three setTimeout() functions should be executed in the order "world" -> "hey" -> "kiora" providing that the time we have set are 0 mil second -> 1 mil second -> 2 mil second respectively. Yet, there is no different between 0 and 1 mil second. That is why we will see "hey" in the next. "world" is being executed then and following by the last on "kiora".

For reference, read this https://stackoverflow.com/questions/8341803/difference-between-settimeoutfn-0-and-settimeoutfn-1
</p>
</details>


---

###### 12. What's the output?

```javascript

String.prototype.lengthy = ()=>{
  
    console.log("hello");
  
 };

let x = {name: "Vuong"}

delete x;

x.name.lengthy();

```
- A:  "Vuong";
- B:  "hello";
- C:  "undefined"
- D:  "ReferenceError"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

`String.prototype.something = function(){}` is the common way to define a new built-in method for `String`. We can do the same thing with `Array`, `Object` or `FunctionName` where FunctionName is the function designed by ourself.

That is not challenging to realise that `"string".length()` always returns `hello`. Yet, the tricky part lies in the `delete object` where we might think that this expression will entirely delete the object. That is not the case as `delete` is used to delete the property of the object only. It does not delete the object. Then we get `hello` rather than `ReferenceError`.

Note that if we declare object without `let, const` or `var`, we then have a global object. `delete object` then return true. Otherwise, it always return false.

</p>
</details>

---

###### 13. What's the output?

```javascript

let x = {};

x.__proto__.hi = 10;

Object.prototype.hi = ++x.hi;

console.log(x.hi + Object.keys(x).length);

```
- A:  10
- B:  11
- C:  12
- D:  NaN

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

First we have an empty object `x`, then we add another property `hi` for x with `x.__proto__.hi`. Note this is equivalent to `Object.prototype.hi = 10` and we are adding to the `father` object `Object` the property `hi`. It means every single object will inherit this propety. The property `hi` becomes a shared one. Say now we declare a new object such as `let y = {}`, `y` now has a propery `hi` inherited from the `father` `Object`. Put it simply `x.__proto__ === Object.prototype` returns `true`.

Then we overwrite the property `hi` with a new value 11. Last we have 11 + 1 = 12. `x` has one property and `x.hi` returns 11.

</p>
</details>

---

###### 14. What's the output?

```javascript
const array = (a)=>{
  let length = a.length;
  delete a[length-1];
  return a.length;
};

console.log(array([1, 2, 3, 4]));


const object = (obj)=>{
  let key = Object.keys(obj);  
  let length = key.length;  
  delete obj[key[length - 1]];
  return Object.keys(obj).length;
};

console.log(object({1: 2, 2: 3, 3: 4, 4:5}));


const setPropNull = (obj)=>{
  let key = Object.keys(obj);  
  let length = key.length;  
  obj[key[length - 1]] = null;  
  return Object.keys(obj).length;
  
};

console.log(setPropNull({1: 2, 2: 3, 3: 4, 4:5}));

```
- A:  333
- B:  444
- C:  434
- D:  343

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

This question examines how the `delete` operator works in JavaScript. In short, it does nothing when we write `delete someObject` or `delete someArray`. It nonetheless completely deletes and removes a property of an object when writing something like `delete someObject.someProperty`. In the case of array, when we write `delete someArray[keyNumber]`, it only removes the `value` of the `index`, keep the `index` intact and the new `value` is now set to `undefined`. For that reason, in the code first snippet, we get (the length) 4 elements as in the original array but only 3 properties left in the object passed when the function object() is called, as in the second snippet.

The third snippet gives us 4 as declaring an object's propery to either `null` or `undefined` does not completely remove the property. The key is intact. So the length of the object is immutable.

For those who are familiar with PHP, we have `unset($someArray[index])` that remove the array element, both key and value. When `print_r` the array, we might not see the key and value that have been unset. However, when we push (using `array_push($someArray, $someValue)`) a new element in that array, we might see that the previous key is still kept, but no value and not being displayed. That is something you should be aware of. Have a look at https://3v4l.org/7C3Nf

</p>
</details>



---

###### 15. What's the output?

```javascript

var a = [1, 2, 3];
var b = [1, 2, 3];

var c = [1, 2, 3];
var d = c;

var e = [1, 2, 3];
var f = e.slice();

console.log(a === b); 
console.log(c === d); 
console.log(e === f); 

```
- A:  true  true  true
- B:  false false true
- C:  true  true  false
- D:  false true  false

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

`a` and `b` returns false because they point to different memory location even though the values are the same. If you are coming from PHP world, then it will return true obviously when we compare either value or value + type. Check it out: https://3v4l.org/IjaOs.

In JavaScript, value is passed by reference in case of `array` and `object`. Hence in the second case, `d` is the copy of `c` but they both point to the same memory position. Everything changes in `c` will result in the change in `d`. In PHP, we might have `$a = &$b;`, working in the similar way.

The third one gives us a hint to copy an array in JavaScript using `slice()` method. Now we have `f`, which is the copy of `e` but they point to different memory locations, thus they have different "life". We get `false` accordingly when they are being compared.

</p>
</details>




---
###### 16. What's the output?

```javascript

var languages = {
  name:['elixir', 'golang', 'js', 'php', {name:"feature"}],
  feature: 'awesome',
}


let flag = languages.hasOwnProperty(Object.values(languages)[0][4].name);


(() => {
  if (flag !==false){
    console.log(Object.getOwnPropertyNames(languages)[0].length << Object.keys(languages)[0].length);
  }else{
    console.log(Object.getOwnPropertyNames(languages)[1].length << Object.keys(languages)[1].length);
  }
})()


```

- A:  8
- B:  NaN
- C:  64
- D:  12

<details><summary><b>Answer</b></summary>
<p>

#### Answer: 64

The code snippet is quite tricky as it has a couple of different built-in methods handling object in `JavaScript`. For example, both `Object.keys` and `Object.getOwnPropertyNames` are used even thought they are quite similar except that the latter can return non-enumerable properties. You might want to have a look at this thoroughly written reference https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyNames


`Object.values` and `Object.keys` return the property value and property name of the object, respectively. That is nothing new. `object.hasOwnProperty('propertyName')` returns a `boolean` confirming whether a property exists or not. 

We have `flag` true because `Object.values(languages)[0][4].name` returns `feature`, which is also the name of the property. 

Then we have 4 << 4 in the `if-else` flow that returns the bitwise value, equivalent to `4*2^4` ~ `4*16` ~ 64.
</p>
</details>

---
###### 17. What's the output?

```javascript
var player = {name: 'Ronaldo', age: 34, getAge: function(){return ++this.age - this.name.length}};

function score(greeting, year) {

  console.log(greeting + ' ' + this.name + `! You were born in  ${year - this.getAge()}`);
}


window.window.window.score.call(window.window.window.player, 'Kiora', 2019); 

score.apply(player, ['Kiora', 2009 ]); 

const helloRonaldo = window.score.bind(window.player, 'Kiora', 2029);

helloRonaldo(); 

```

- A:  "Kiora Ronaldo! You were born in  1985", "Kiora Ronaldo! You were born in  1985", "Kiora Ronaldo! You were born in  1985"
- B:  "Kiora Ronaldo! You were born in  1991", "Kiora Ronaldo! You were born in  1991", "Kiora Ronaldo! You were born in  1999"
- C:  "Kiora Ronaldo! You were born in  1991",  NaN,                                     "Kiora Ronaldo! You were born in  1980"
- D:  "Kiora Ronaldo! You were born in  1991", "Kiora Ronaldo! You were born in  1980", "Kiora Ronaldo! You were born in  1999"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

We can use `call()`, `apply()` and `bind()` to appy a function to any object. At first sight, it seems that three functions do the same thing. Yet there are some situations where they are differently employed to handle respective contexts or solve particular problems. 

Of the three, only `bind()` can be executed after binding. We can create a variable to store the result as `helloRonaldo()` in the code snippet above. `apply()` and `call()` will bind and execute the function at the same time. `apply()` hints us `a` ~ array where we need to pass an array as parameter. `call()` hints us `c` or comma where we pass parameters with a comma. You might want to have a look at this post https://stackoverflow.com/questions/15455009/javascript-call-apply-vs-bind

Note that `window.window.window.score` or `window.score` or simply `score` do the same thing. It points to the `score()` function in the global scope.

The correct anwser is D. The `score()` and `getAge()` functions are nothing special.


</p>
</details>


---
###### 18. What's the output?

```javascript

var ronaldo = {age: 34};

var messi = {age: 32};

function score(year, tr, t) {
   
   if(typeof tr === 'function' && typeof t === 'function') {

      console.log(`You score ${tr(year, t(this.age))} times`);
      
  }
}

const transform = (x, y) => x - y;

const title = (x) => ++x+x++;

const helloRonaldo = score.bind(ronaldo, 2029, transform, title);

helloRonaldo(); 

const helloMessi = score.bind(messi, 2029, transform, title);

helloMessi(); 

```

- A:  "You score 1989 times" and "You score 1963 times"
- B:  "You score 1959 times" and "You score 1989 times"
- C:  "You score 1989 times" and "You score 1953 times"
- D:  "You score 1959 times" and "You score 1963 times"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

`bind()` allows us to bind a function declared with any object. Here we bind `score()` and both `ronaldo` and `messi`. 

In `score()` we pass three parameters `year`, `tr` and `t` in which both `tr` and `t` are function. They handle simple things as defined afterwards.

When we bind `score()` with `ronaldo` and `messi`, we pass three parameters as declared in the `score()` function wherein `transform` and `title` are functions.

</p>
</details>


