### Call,Apply And Bind
***

* Before exploring the call ,apply and bind lets first see which type of problem these three things solve.

**Problem Statement**

Let we have some objects:-

```javascript

const userDetails1 = {
    name: "Rohan",
    age: "23",
    designation: "software developer"
    printDetails: function() {
        console.log(this.name)         //this refers to the current object
    }
}


const userDetails2 = {
    name: "Deepak",
    age: "24",
    designation: "backend developer"
    printDetails: function() {
        console.log(this.name)         //this refers to the current object
    }
}


```

* Now I want to print the name of the user and for this we are creating a new function in every single object which is not a very good practice as we creating the new functions for just printing the same thing i.e, name etc.

* To solve this issue we can use call or apply, however there is a very basic difference between these two which we will see with the help of example.

