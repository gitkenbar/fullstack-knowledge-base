# Typescript Fundamentals Notes
 Code along with Max's videos
Take notes on this.typescript-fundamentals.md 

1. Introduction
   Typescript is an extension of Javascript, if you know Javascript you only need to learn the key features of Typescript.

2. Typescript Rationale
   Typescript is a "superset" to JavaScript. It just adds features to JavaScript Syntax, most importantly "static typing"

   Javascript is Dynamically typed.
    The '+' symbol will add two numbers together
   2 + 5 = 7
    it will also concatenate two strings of numbers
    '2'+'5' = '25'
    being able to require a data-type can prevent errors in large projects with many people working on it.

3. Setting Up
   typescriptlang.org <-- Official typescript website
   Max offers a full course on TypeScript if we are interested

   Command to install typescript in a project
   npm install typescript

    Command to install TypeScript Globally
   npm install -g typescript

    Typescript is a "superset" to JavaScript.
    It does not run in browser, it needs to be compiled to JavaScript before it can be used.

    command to invoke the

    npx tsc ||FILENAME.ts||
4. Base Types
   Primatives: number, string, boolean, null, undefined
   Complex Types: arrays, objects
   Function Types, parameters

   Primatives
   let age: number;
   age = 12; //all good
   age = "12"; // error

   let userName: string;

    Complex Types

    let hobbies: string[];

    hobbies = ['Sports', 'Cooking'];

    Type Inference
    let person: {
        name: string;
        age: number;
    };

    person = {
        name: 'Ken',
        age: 32
    }

    person = {  //this would throw an error
        isEmployee: true
    }

    this code defines people as an array of objects by defining the object and following it with []
    let people: {
        name: string;
        age:number;
    }[]

    Type Inference

    let course = 'React - The Complete Guide';
    course = 12341; //Error, course is inferred to be a string, trying to assign a number will fail
5. Union Types
   using | "pipes" | indicates the object can be of one type or the other
   let course: string | number;
   course = 12341; // no error, course is allowed to be strings or numbers
6. Type Aliases
   type Person = {
        name: string,
        age: number
    }

    let Ken: Person {
        name: 'Ken',
        age: 32
    }
7. Functions and Types
    assigning types in functions
   function add(a:number, b: number) {
    return a + b; // return value is inferred to be a number, because the arguments are both numbers.
   }
   function printOutput(value: any) { // "print()" is a built in JavaScript function so it needs to be named something else
    console.log(value); //function doesn't return anything, it's type is void
   }
8. Configuring the Compiler
   
