### Call,Apply And Bind
***

* Before exploring the call ,apply and bind lets first see which type of problem these three things solve.

**Problem Statement**

Let we have some objects:-

```javascript

const userDetails1 = {
    name: "Rohan",
    age: "23",
    designation: "software developer",
    printDetails: function() {
        console.log(this.name)         //this refers/points to the current object
    }
}
userDetails1.printDetails();


const userDetails2 = {
    name: "Deepak",
    age: "24",
    designation: "backend developer",
    printDetails: function() {
        console.log(this.name)         //this refers/points to the current object
    }
}
userDetails1.printDetails();

```

* Now I want to print the name of the user and for this we are creating a new function in every single object which is not a very good practice as we creating the new functions for just printing the same thing i.e, name etc.

* To solve this issue we can use call or apply, however there is a very basic difference between these two which we will see with the help of example.

### Call
***

The call() method calls a function by passing this and specified values as arguments.

* Solving the above problem with **call()**.

```javascript

const userDetails1 = {
    name: "Rohan",
    age: "23",
    designation: "software developer",
    printDetails: function() {
        console.log(this.name)
    }
}
userDetails1.printDetails();


const userDetails2 = {
    name: "Deepak",
    age: "24",
    designation: "backend developer"
}
userDetails1.printDetails.call(userDetails2);  //call the printDetails() method of userDetails1 for userDetails2.

```

```
Output

Rohan
Deepak
```

* Now we need not to create the printDetails() method again and again to print the same data.

> **Let us see one more scenario where the printDetails() method is outside the object i.e, it is an individual a function,  then how we will be using call()**

**Example**

```javascript

const userDetails1 = {
    name: "Rohan",
    age: "23",
    designation: "software developer",
}

 let printDetails = function() {
        console.log(this.name)
    }

printDetails.call(userDetails1)

const userDetails2 = {
    name: "Deepak",
    age: "24",
    designation: "backend developer"
}
//function borrowing
printDetails.call(userDetails2);  

```

```
Output:

Rohan
Deepak
```

> Explanation

**printDetails function:**

* printDetails is a function that does not take any arguments explicitly, but it attempts to print the name property of the object it's called on.

* It uses the this keyword inside the function, which refers to the object that the function is called on. In this case, it's expected to be called on an object that has a name property.

**printDetails.call(userDetails1)**

* This line of code calls the printDetails function on the userDetails1 object using the call method. The call method allows you to specify the value of this within the function.

* As a result, within the printDetails function, this refers to userDetails1, and it prints "Rohan" to the console because userDetails1 has a name property with the value "Rohan".

**printDetails.call(userDetails2):**

* This line of code does the same thing as the previous call but with the userDetails2 object.

* When printDetails is called on userDetails2, this refers to userDetails2, and it prints "Deepak" to the console because userDetails2 has a name property with the value "Deepak".

**Summary**

* The printDetails function is a generic function that can be called on different objects, and it uses the this keyword to access and print the name property of the object it's called on. By using the call method, you can change the context (i.e., the value of this) for the function, allowing it to work with different objects and print their respective name properties.

> **call() method with argument passing**

```javascript

const userDetails1 = {
    name: "Rohan",
    age: "23",
    designation: "software developer",
}

 let printDetails = function(state, country) {
        console.log(this.name,state,country)
    }

printDetails.call(userDetails1,"Jharkhand", "India")

const userDetails2 = {
    name: "Deepak",
    age: "24",
    designation: "backend developer"
}
printDetails.call(userDetails2,"Bihar", "India");
```
```
Output

Rohan Jharkhand India
Deepak Bihar India
```

### Apply()
***

* The apply() in Javascript is used to call a function in a different object with the given **this(current object reference)** value, and the arguments are passed in the form of an array. 

* And this is the only difference between call() and apply() that with **call()** we can not pass the arguments as a single array list, we have to pass arguments separately and individually. But with **apply()** we can pass the multiple argument as single array list.

**Example**

```javascript

const userDetails1 = {
    name: "Rohan",
    age: "23",
    designation: "software developer",
}

 let printDetails = function(state, country) {
        console.log(this.name,state,country)
    }

printDetails.apply(userDetails1, ["Jharkhand", "India"])
```

```
Output

Rohan Jharkhand India
```

* This method allows us to write methods that can be used on different objects and hence increase the reusability of code.

> Note : we can also use apply() instead of call() only when there is no argument in the apply().

**Example**

```javascript
const userDetails1 = {
    name: "Rohan",
    age: "23",
    designation: "software developer",
}

 let printDetails = function() {
        console.log(this.name)
    }

printDetails.apply(userDetails1);
```

```
Output

Rohan
```

> Note: But if we are passing argument and using apply() then we must have to pass the arguments as array, otherwise we will get error.

**Example**

```javascript

const userDetails1 = {
    name: "Rohan",
    age: "23",
    designation: "software developer",
}

 let printDetails = function(state, country) {
        console.log(this.name,state,country)
    }

printDetails.apply(userDetails1,"Jharkhand", "India")
```

```
Output

printDetails.apply(userDetails1,"Jharkhand", "India")
             ^

TypeError: CreateListFromArrayLike called on non-object
```

### Bind()
***

* The bind() method creates a new function where this keyword refers to the parameter in the parenthesis. This way the bind() method enables calling a function with a specified this value. 

* Bind() method tells us that don't call the function directly instead store it as new function and call and use whenever needed.

```javascript

const userDetails1 = {
    name: "Rohan",
    age: "23",
    designation: "software developer",
}

 let printDetails = function(state, country) {
        console.log(this.name,state,country)
    }

const newFun = printDetails.bind(userDetails1,["Jharkhand", "India"]);
newFun();
```

```
Output

Rohan [ 'Jharkhand', 'India' ] undefined
```


```javascript

const userDetails1 = {
    name: "Rohan",
    age: "23",
    designation: "software developer",
}

 let printDetails = function(state, country) {
        console.log(this.name,state,country)
    }

const newFun = printDetails.bind(userDetails1,"Jharkhand", "India");
newFun();
```

```
Output

Rohan Jharkhand India
```

* Here we are calling the printDetails function and storing this in a variable newFun and we can call this variable as a new function whenever we need.

### What is 'this' in Javascript
***

![Screenshot 2023-11-01 195004](https://github.com/codingXpert/Js-Interview-Question/assets/101451924/968d194a-a49f-418d-97b5-a68ac9500805)


### Map(), Filter(), Reduce(), forEach() And Sort() 
***

**forEach() Method**

* forEach() is a higher order function as it receives a callback as parameter.

* The forEach() method is an iterative method. It calls a provided callbackFn function once for each element in an array in ascending-index order. 

* Unlike map() , forEach() always returns undefined and is not chainable.

* There is no way to stop or break a forEach() loop other than by throwing an exception. If we need such behavior, the forEach() method is the wrong tool.

**Syntax And Parameters**

![Screenshot 2023-11-02 190850](https://github.com/codingXpert/Js-Interview-Question/assets/101451924/6962733f-fd4b-4310-8669-597e0bb3ca39)

**Examples**

```javascript
const companies = [
    {name: "Google", category: "Product Based", start: "1981", end: "2050"},
    {name: "Paytm", category: "Product Based", start: "1999", end: "2040"},
    {name: "Amazon", category: "Product Based", start: "1967", end: "2060"},
    {name: "TCS", category: "Product Based", start: "1956", end: "2080"},
    {name: "Mindtree", category: "Product Based", start: "1981", end: "2050"}
]
```

**Traditional Approach To Iterate:-**

```javascript
for(let i=0; i<=companies.length; i++){
    console.log(companies[i].name);
}
```

**forEach() Method To Iterate**

```javascript
companies.forEach(function(company){
    console.log(company.name);
})
```

**Shorthand Way Of Writing This(Using Arrow Function)**

```javascript
companies.forEach((company) => {
    console.log(company.name);
})
```

**One Line Code**

```javascript
companies.forEach(company => console.log(company.name));   // if we do not have multiple argument in callback we need not to use '()'
```

```
Output Of All the code

Google
Paytm
Amazon
TCS
Mindtree
```

> Note: We can also iterate over any function.

```javascript
const numbers = [65, 44, 12, 4];
numbers.forEach(myFunction)

function myFunction(item, index, arr) {
  console.log(item, index, arr);
}
```

```bash
Output

65 0 [ 65, 44, 12, 4 ]
44 1 [ 65, 44, 12, 4 ]
12 2 [ 65, 44, 12, 4 ]
4 3 [ 65, 44, 12, 4 ]
```

 ### Filter() Method
 ***

 * filter() is a higher order function.

 * The filter() method creates a new array filled with elements that pass a test provided by a function. 

 * The filter() method does not execute the function for empty elements. 

 * The filter() method does not change the original array.

**Syntax And Parameters**

![Screenshot 2023-11-02 202943](https://github.com/codingXpert/Js-Interview-Question/assets/101451924/458ec8a3-e016-4831-91ce-3540b34628c1)

![Screenshot 2023-11-02 202958](https://github.com/codingXpert/Js-Interview-Question/assets/101451924/e31cc419-c13a-45f1-a97b-b894b7c76210)

**Examples**

```javascript
const ages = [33, 12, 20, 16, 5, 54, 21, 44, 61, 13, 15, 45, 25, 64, 32];
```
**Traditional Approach To Iterate:-**

```javascript
for(let i=0; i<=ages.length; i++){
    if(ages[i] >= 20){
        console.log(ages[i]);
    }
}
```

```
Output

33
20
54
21
44
61
45
25
64
32
```

**filter() Method To Iterate**

```javascript
const age = ages.filter(function(age){
    if(age >= 20){
        return true;
    }
});
console.log(age);
```

```javascript
Output

[33, 20, 54, 21, 44,61, 45, 25, 64, 32]
```

**Shorthand Way Of Writing This(Using Arrow Function)**

```javascript
const age = ages.filter(age => age >= 20);
console.log(age);
```

```javascript
Output

[33, 20, 54, 21, 44,61, 45, 25, 64, 32]
```

```javascript
const sb = companies.filter((company) => company.category == "Product Based");
console.log(sb);
```

```
Output

[
  {
    name: 'Google',
    category: 'Product Based',
    start: '1981',
    end: '2050'
  },
  {
    name: 'Paytm',
    category: 'Product Based',
    start: '1999',
    end: '2040'
  },
  {
    name: 'Amazon',
    category: 'Product Based',
    start: '1967',
    end: '2060'
  },
  {
    name: 'TCS',
    category: 'Product Based',
    start: '1956',
    end: '2080'
  },
  {
    name: 'Mindtree',
    category: 'Product Based',
    start: '1981',
    end: '2050'
  }
]

```

### Map() Method
***
* map() is a higher order function.

* map() creates a new array from calling a function for every array element.

* map() does not execute the function for empty elements.

* map() does not change the original array.

**Syntax And Parameters**

![Screenshot 2023-11-03 112124](https://github.com/codingXpert/Js-Interview-Question/assets/101451924/eff55a8d-0852-40e5-be7d-9ab5401dbcb2)

![Screenshot 2023-11-03 112136](https://github.com/codingXpert/Js-Interview-Question/assets/101451924/3bb83802-846c-4337-8e1b-95acd6bb55da)


**Examples**
```javascript

const data = companies.map((company) => {
    return `${company.name} ${company.start}`
});
console.log(data)
```

```
Output

[
  'Google 1981',
  'Paytm 1999',
  'Amazon 1967',
  'TCS 1956',
  'Mindtree 1981'
]
```

### Sort() Method
***
* sort() is higher order predefined function.

* The sort() sorts the elements of an array.

* The sort() overwrites the original array.

* The sort() sorts the elements as strings in alphabetical and ascending order.

**Syntax And Parameters**

![Screenshot 2023-11-03 125938](https://github.com/codingXpert/Js-Interview-Question/assets/101451924/010512f9-9126-4a65-b0d7-9618cfbb2125)

![Screenshot 2023-11-03 130002](https://github.com/codingXpert/Js-Interview-Question/assets/101451924/297eb516-52d4-49d4-b9ed-9b44da8f9a67)

**Example**

```javascript

const sorted = companies.sort(function(c1, c2){
    if(c1.start > c2.start){
        return 1;
    }else{
        return -1;
    }
});
console.log(sorted);
```

```
Output 

[
  {
    name: 'TCS',
    category: 'Product Based',
    start: '1956',
    end: '2080'
  },
  {
    name: 'Amazon',
    category: 'Product Based',
    start: '1967',
    end: '2060'
  },
  {
    name: 'Mindtree',
    category: 'Product Based',
    start: '1981',
    end: '2050'
  },
  {
    name: 'Google',
    category: 'Product Based',
    start: '1981',
    end: '2050'
  },
  {
    name: 'Paytm',
    category: 'Product Based',
    start: '1999',
    end: '2040'
  }
]
```

**Shorthand Way Of Writing This(Using Arrow Function)**

```javascript
const sorted = companies.sort((c1, c2) => (c1.start > c2.start ? 1 : -1));
console.log(sorted);
```

```
Output

[
  {
    name: 'TCS',
    category: 'Product Based',
    start: '1956',
    end: '2080'
  },
  {
    name: 'Amazon',
    category: 'Product Based',
    start: '1967',
    end: '2060'
  },
  {
    name: 'Mindtree',
    category: 'Product Based',
    start: '1981',
    end: '2050'
  },
  {
    name: 'Google',
    category: 'Product Based',
    start: '1981',
    end: '2050'
  },
  {
    name: 'Paytm',
    category: 'Product Based',
    start: '1999',
    end: '2040'
  }
]
```

> **Explanation**

The comparison is done as follows:

* If c1.start is greater than c2.start, the function returns 1. This indicates that c1 should come after c2 in the sorted array.

* Otherwise, if c1.start is less than or equal to c2.start, the function returns -1. This indicates that c1 should come before or stay in the same position as c2 in the sorted array.

* 1 is for ascending order.

* -1 is for descending order.

* The sort method uses the comparison function to determine the order of the elements in the array. It repeatedly calls the comparison function for pairs of elements and rearranges them based on the return values until the array is sorted in ascending order according to the "start" property.

**Some more examples**

```javascript
const sortedAges = ages.sort((a, b) => (a - b));
console.log(sortedAges);
```

```javascript
Output

[5,12,13,15,16,20,21,25,32,33,44,45,54,61,64]
```

```javascript
const sortedAges = ages.sort((a, b) => (b - a));
console.log(sortedAges);
```

```
Output

[64,61,54,45,44,33,32,25,21,20,16,15,13,12,5]
```

### Reduce() Method
***

* reduce() is a higher order predefined method.

* The reduce() method executes a reducer function for array element.

* The reduce() method returns a single value: the function's accumulated result.

* The reduce() method does not execute the function for empty array elements.

* The reduce() method does not change the original array.

**Syntax And Parameters**

![Screenshot 2023-11-03 134950](https://github.com/codingXpert/Js-Interview-Question/assets/101451924/f9f57328-ae37-4de2-a6ab-58c8ce282714)

![Screenshot 2023-11-03 135010](https://github.com/codingXpert/Js-Interview-Question/assets/101451924/6bf8a23a-dc21-4fb0-a868-3e09fd1280e9)

![Screenshot 2023-11-03 135018](https://github.com/codingXpert/Js-Interview-Question/assets/101451924/7b5b07cb-80bf-456f-ac6d-5fcd88654f35)


**Example**

```javascript
const ages = [33, 12, 20, 16, 5, 54, 21, 44, 61, 13, 15, 45, 25, 64, 32];
```

**Traditional Approach To Find Sum/Total**

```javascript

let total = 0;
for(let i=0; i<ages.length; i++){
    total += ages[i]
}
console.log(total);
```

**solving by reduce()**

```javascript

const sumAges = ages.reduce(function(total, age){
    return total+age;
},0);
console.log(sumAges);
```

**Shorthand Way Of Writing This(Using Arrow Function)**

```javascript
const sumAges = ages.reduce((total, age) => total+age, 0);
console.log(sumAges);
```

> **Note:-** zero is the initial value of total.

```
Output of the above 3 codes.

460
```

### What Is Difference Between Map() And forEach().
***

* The map() method returns a new array, whereas the forEach() method does not return a new array.

* The map() method is used to transform the elements of an array, whereas the forEach() method is used to loop through the elements of an array.

* The map() method can be used with other array methods, such as the filter() method, whereas the forEach() method cannot be used with other array methods.

**Examples**

```javascript
const myArray = [5, 4, 3, 2, 1]

const result = myArray.map(x => x * x);
console.log(result);
console.log(myArray);
```

```
Output

[ 25, 16, 9, 4, 1 ]
[ 5, 4, 3, 2, 1 ]
```

```javascript
const myArray = [5, 4, 3, 2, 1]

myArray.forEach(x => console.log(x * x));
console.log(myArray);
```

```
Output

25
16
9
4
1
[ 5, 4, 3, 2, 1 ]
```

```javascript
const myArray = [
  { id: 1, name: "john" },
  { id: 2, name: "Ali" },
  { id: 3, name: "Mass" },
]

 myArray.forEach(element => console.log(element.name));
```

```
Output

john
Ali
Mass
```

 **Conclusion**

In conclusion, the forEach() and map() methods are both used to loop through arrays and objects. The forEach() method does not return a new array, whereas the map() method returns a new array. The map() method is used to transform the elements of an array, whereas the forEach() method is used to loop through the elements of an array.


### Destructuring, Rest and Spread Operator.  
*** 

![freeCodeCamp-Cover-1](https://github.com/codingXpert/Js-Interview-Question/assets/101451924/cf245dc7-dd40-40ae-ad2a-ac00801ad57d) 