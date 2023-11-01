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



