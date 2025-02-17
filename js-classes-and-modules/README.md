# JS Classes and Modules

## Working With Modules and Classes

## Before we start
1. This practical task will be verified automatically with tests. 
2. Please put all `JavaScript` code in the `src/script.js` file and `HTML` code in the `src/index.html` file. Functions from `src/script.js` are used in the `<script>` inside `src/index.html`. If you use any other file, it cannot be verified.
3. Please don't change the page structure if this is not required. It may affect the tests.

## Development
While developing, you can open `src/index.html` in your browser to check your task as you go. However, we have prepared a more convenient way to run it locally. You can find the details here: [Local Development](https://gitlab.com/gap-bs-front-end-autocode-documents/autocode-documents/-/blob/main/docs/LocalDevelopment.md).

## Run JavaScript code in RunJS application
`RunJS` is a JavaScript and TypeScript playground for desktop operating systems. It runs code as it's written and displays formatted results in the output panel on the right.

![RunJS application in work](https://gitlab.com/gap-bs-front-end-autocode-documents/autocode-documents/-/raw/main/images/runjs-intro.png)

RunJS is available on macOS, Windows, and Linux operating systems.

Here are detailed instructions on installing and using it: [RunJS documentation](https://runjs.app/docs).

## Check your solution before submitting it (OPTIONAL)

To be sure you submit a correct solution, you can verify it locally, but this will require some local setup. You can find the instructions here: [Verify your solution locally](https://gitlab.com/gap-bs-front-end-autocode-documents/autocode-documents/-/blob/main/docs/VerifySolutionLocally.md).


## Task Requirements

This task has two parts: `JS Modules` and `JS Class creation`.

**Please, note:**
- If the task requirement says *Function should **return** <something>*, it should deliberately return the expected value. If you show it in the console instead of returning a value, it will not pass the check. For more about returning a value: [Returning a value](https://javascript.info/function-basics#returning-a-value).

### JS Modules
1. **Function "sayHelloToUser"**
In the `script.js` file, there is the function `sayHelloToUser`. By default, it will not work because it requires several other JS modules to work properly. In this task, you will create them.
`sayHelloToUser` function code:
```js
function sayHelloToUser(name) {
    if (!isValid(name)) { // "isValid" will be imported
        return 'Invalid name';
    }
    return `${GREETING}, ${name}!`; // "GREETING" will be imported
}
```
**1.1.** In the `src` folder, create the file `isValidName.js`, which should export the function `isValidName` by default:
```js
function isValidName(name) {
    return !!name && typeof name === 'string' && name.trim().length > 1;
}
```
After you create it, import the function to `script.js` with the name `isValid`. This function will be used in `sayHelloToUser`. Please note that the names of the function are different in `isValidName.js` and `script.js`. This is done on purpose. 
**1.2** In the `src` folder, create the folder `constants` and add the file `GREETING.js`, which should export the constant `GREETING`:
```js
const GREETING = 'Hello';
```
After you create the constant, import it to `script.js` with the original name.
If you did everything correctly, `sayHelloToUser` will work. You can verify this in the `index.html` file.

2. **Function "formatPrices"**
**2.1** In the `src` folder, create the file `formatPrices.js`, which should export the function `formatPrices`:
```js
function formatPrices(prices, currency) {
    const currencySymbol = CURRENCY_SYMBOLS[currency] || '$';
    return prices.map((price) => {
        return formatWithCurrency(price, currencySymbol);
    });
}
```
As you can see, it uses the constant (`CURRENCY_SYMBOLS`) and the function (`formatWithCurrency`), which you need to create and import.
**2.2** In the `src/constants` folder, create the file `CURRENCY_SYMBOLS.js`, which should export the constant `CURRENCY_SYMBOLS`:
```js
const CURRENCY_SYMBOLS = {
    US: '$',
    EUR: '€',
    JPN: '¥',
};
```
After you create the constant, import it to `formatPrices.js` with the original name.
**2.3** In the `src` folder, create the file `formatWithCurrency.js`, which should export the function `formatWithCurrency`:
```js
function formatWithCurrency(price, currencySymbol) {
    return `${price.toFixed(2)}${currencySymbol}`;
}
```
Please note that you should export this function with its name as you did for the constants.
After you create the function, import it to `formatPrices.js`.
If you did everything correctly, `formatPrices` will work. You can verify this in the `index.html` file.

### JS Class Creation
You need to create two classes, `User` and `Task`, to store the user's data with the assigned tasks.
Before you start, in the `src` folder, create the folder `user-data`. 
You will put class files in it.
1. **Class "Task"**
Create a file called `Task.js` in the `src/user-data` folder. 
Then, create an empty `Task` class.
This file should export the `Task` class. 
This class is used to create tasks assigned to a user. 
Every task object created via the `Task` class should have one public property:
- `name` - string, the name of a task
**Class implementation requirements:**
- **constructor**: takes one parameter `name` and assigns its value to the `name` property of the object.
**Usage example:**
```js
let task = new Task('Clean the room');
console.log(task.name); // 'Clean the room'
```
- **"description" setter and getter**. A description of the task will be stored in a private property of the object. **By default, this should be an empty string**. Here you can find more details on how to create private properties: [Private "#waterLimit"](https://javascript.info/private-protected-properties-methods#private-waterlimit).
    - **"description" getter**: add a getter for `"description"`. The getter should return a value from the private `#description` property.
    ```js
    let task = new Task('Clean the room');
    console.log(task.description); // "" - this is an empty string by default
    ```
    - **"description" setter**: add a setter for `"description"`. The setter should update a value in the private `#description` property. It should only set a new value if this value is of the `string` type. It should ignore the other types.
    ```js
    let task = new Task('Clean the room');
    task.description = 777; // 777 ignored by setter
    console.log(task.description); // ""
    task.description = 'New Description'; // set new value of the string type
    console.log(task.description); // "New Description"
    ```
Please don't forget to export the `Task` class.

2. **Class "User"**
Create a file called `User.js` in the `src/user-data` folder. 
After that, create an empty `User` class.
This file should export the `User` class. 
This class is used to create user objects.
Every user object should have four public properties:
- `firstName` - user's first name
- `lastName` - user's last name
- `age` - user's age
- `tasks` - an array of tasks assigned to a user. Every task is an instance of the class `Task` created previously.
**Class implementation requirements:**
- **constructor**: should take two parameters, `firstName` and `lastName`, and assign their values to the `firstName` and `lastName` properties of the object.
**Usage example:**
```js
let user = new User('Stan', 'Jackman');
console.log(user.firstName); // "Stan"
console.log(user.lastName); // "Jackman"
```
The properties `age` and `tasks` should not be specified in the constructor but should have default values. `age` should be `1`, and `tasks` should be an empty array(`[]`);
```js
let user = new User('Stan', 'Jackman');
console.log(user.age); // 1
console.log(user.tasks); // []
```
Default values should be set as `"Class Fields"`: [Class Fields](https://javascript.info/class#class-fields)
- **"fullName" getter**: add getter for a `"fullName"`. Getter should return a concatenated `firstName` and `lastName` with a space between them. It should be a getter, not a regular public property.
    ```js
    let user = new User('Stan', 'Jackman');
    console.log(user.fullName); // "Stan Jackman"
    ```
- **method "setAge"** - a method for updating the `age` property. 
    - It should take one parameter: `newAge`: new value for the `age` property.
    - It should update the `age` property only if a new value fits the requirements:
        - It is finite.
        - It is more than `0`.
        - It is a `number` type.
    ```js
    let user = new User('Stan', 'Jackman');
    console.log(user.age); // 1
    user.setAge(NaN); // It doesn't work; it is not a finite value.
    console.log(user.age); // 1
    user.setAge(Infinity); // It doesn't work; it is not a finite value.
    console.log(user.age); // 1
    user.setAge(-Infinity); // It doesn't work; it is not a finite value.
    console.log(user.age); // 1
    user.setAge(-100); // It doesn't work; the value is less than 0.
    console.log(user.age); // 1
    user.setAge(0); // It doesn't work; the value is 0.
    console.log(user.age); // 1
    user.setAge('100'); // It doesn't work; value is of the string type.
    console.log(user.age); // 1
    user.setAge(44); // It sets a new value.
    console.log(user.age); // 44
    ```
- **method "addTasks"** - a method for adding tasks to the public property `task`
    - It should take one parameter, `tasks`, and is an array of objects created with the `Task` class. These tasks should be added to the end of an array stored in the property `tasks`.
    - It should add only objects created with the `Task` class. If there is an object in the array created with a different constructor, it should be ignored.
    ```js
    let user = new User('Stan', 'Jackman');
    let newTasks1 = [
        new Task('Task1'),
        new Task('Task2'),
    ];
    user.addTasks(newTasks1);
    console.log(user.tasks); // [{ name: 'Task1' }, { name: 'Task2' }];
    let newTasks2 = [
        new Task('Task3'),
    ];
    user.addTasks(newTasks2);
    user.addTasks([{}, {}, {}]); // Should ignore just objects
    console.log(user.tasks); // [{ name: 'Task1' }, { name: 'Task2' }, { name: 'Task3' }];
    ```
- **method "getTasksCount"** - should return the number of tasks in the `tasks` property.
    ```js
    let user = new User('Stan', 'Jackman');
    let newTasks1 = [
        new Task('Task1'),
        new Task('Task2'),
    ];
    user.addTasks(newTasks1);
    console.log(user.getTasksCount()); // 2
```
