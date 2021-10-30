# Declaring Variables
### Dynamic
```typescript
let variable_name = variable_value
```
Ex:
```typescript
let animal = "pig"
```

<br>

## Strict typed
```typescript
let variable_name: variable_type = variable_value
```

Types:
* string
* number
* obj
* struct
* custom type (using class or struct)

Ex:
```typescript
let animal: string = "cow"
```

#### Arrays
to create a strict typed array
```typescript
let variable_name: variable_type[] = [/*only values that are of the variable_type can go here*/]
```
to create a dynamic array
```typescript
let variable_name[] = [/*any value of any type can go in here*/]
```

<br>

# Function declaration
```typescript
function_name(function_parameters) {
    function_code
}
```

The parameters is just a list of identifiers seperated by commas, and types can be used but are not needed

Ex:
```typescript
say_animal(animal_name: string, amount_of_animal) { // Amount of animal is dynamic
    print("This animal is a " + animal_name + ", there are " + amount_of_animal + animal_name + "s in the world")
}
```

<br>

# Object orientation
## Classes
The class syntax looks like this:
```typescript
class class_name {
    code...
}
```

#### @init function
<br>
@init is the function ran on the classes initlization, and it takes parameters passed through the initialization of the class. @init is the only function of the class that has write access to <i>this</i>

```typescript
@init(params) {
    this.//etc
}
```
Ex:
```typescript
class Person {
    @init(name, age) {
        this.name = name
        this.age = age
    }
}

let preston = new Person("Preston", 13)
```
<br>

When passing parameters to the @init function, you can either pass by reference or by value

Ex:
```typescript
class Person {
    @init(name, age, car()) {
        this.name = name
        this.age = age
        this.car = car()
    }
}

class Car {
    @init(name: string, age: number, fav_car: string) {
        this.fav_car = fav_car
        // Passing this.car() to the Person class is passing by reference, the rest of the values (name and age) are being passed by value
        this.person = new Person(name, age, this.car())
    }

    car() {
        print(this.fav_car)
    }
}

let preston = new Person("Preston", 13)
```

#### Class inheritance
To inherit from a class, you pass the class you want to inherit as a class parameter
```typescript
class inherit_class_name {
    code
}

class class_name(inherit_class_name) {
    code
}
```

This allows you to use data from the inherited class in your new class

Ex:
```typescript
class Person {
    @init(name, age) {
        this.name = name
        this.age = age
    }

    greet() {
        print("Hello, I am " + this.name + " and I am " + age + " years old")
    }
}

class Worker(Person) {
    work() {
        print("I am " + this.name + " and I am going to work now.")
    }
}

let worker_man = new Worker("Preston", 13)

worker_man.greet() // Prints "Hello, I am Preston and I am 13 years old
worker_man.work() // Prints I am Preston and I am going to work now
```
If you want to add an init function to the child class, then it will not inherit the parents init function

Ex:
```typescript
class Person {
    @init(name, age) {
        this.name = name
        this.age = age
    }

    greet() {
        print("Hello, I am " + this.name + " and I am " + age + " years old")
    }
}

class Worker(Person) {
    @init(name, age, occupation) {
        this.name = name
        this.age = age
        this.occupation = occupation
    }

    work() {
        print("I am a " this.occupation + ", my name is " + this.name + " and I am going to work now.")
    }
}

let worker_man = new Worker("Preston", 13, "kid")

worker_man.greet() // Prints "Hello, I am Preston and I am 13 years old
worker_man.work() // Prints "I am a kid, my name is Preston and I am going to work now."
```

## Objects
Objects in peko are almost the same as json objects. Declaring them can be dynamic or strict typed
```typescript
let variable_name: obj = {
    key: value
}
```
OR
```typescript
let variable_name = {
    key: value
}
```
To access and change the key value pairs in objects:
```typescript
let variable_name = {
    key: value
}

variable_name.key = new_value
// To read
variable_name.key
```
If you want to access all of the key value pairs in an object, use the following:
```typescript
let variable_name = {
    key: value
}

// Values must go in order
variable_name.loopEach((key, value, index) {
    // Do something with these values
})
```

## Structs
To create a struct, use the following syntax
```typescript
let struct_name: struct = {
    key: type
    // OR
    key
}
```
To use that struct
```typescript
let variable: struct_name = {
    key: value
}
```
Example:
```typescript
let person: struct = {
    name: string,
    age
}

let preston: person = {
    name: "Preston",
    age: 13
}
```