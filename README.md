### node-interface (Interface Structure Example for NodeJS)

- I have a lot of angular apps and node/java services. 
- This serves as a quick reference when the two need to communicate because js can become messy quickly.
- Looks tideous but when you nail down a process, it becomes muscle memory.
- Depends on what technologies you use, theres a few examples down there (no java examples, if you don't know what a class is yet, check out this [link](https://www.w3schools.com/java/java_classes.asp)

- ❓ On a large projects or teams, interfaces provide a critical abstraction. They help us to auto generate documentation and allows architechs/engineers/leads to focus on as a tool to keep code quality known and functionality expected. 
- ‼️ If you're using Angular there is a better way to define and use interfaces (please consult the angular docs). This example is specifically for Node, Express.. (Flow is also another alternative).
- 🛟 I find this helps reduce technical debt. Just remember to use proper variable names. Don't half ass it and you will thank yourself later if you ever need to maintain.
- 🙋‍♂️ Why? Something like this may be useful if you need to communicate back and forth with an Angular App or even an API. It's bascially just a class that we can extend or declare as a variable to re-use throughout the software lifecycle. IDE's will also generate more accurate hints/auto completion based on this "class". 



### Angular Interface Example
```typescript
export interface DemoInterface {
  test1: string;
  test2: number;
}

// In a different controller/class
// Being able to use the interface a type
// is key here especially when you need
// to reuse it.
const demoInterface: DemoInterface = {
  test1: "test1",
  test2 : 100
};

OR

const demoInterface = {
  test1: "test1",
  test2 : 100
} as DemoInterface;
```


### My preferred method (depends on your version). 
```typescript
// Being able to enforce the variable type is key here 
// (using tools like IntelliJ/Webstorm will help you auto generate getters and setters easily).
// I understand that not everyone has this luxury -> fallback posted below. 
class UserInterface {

  private _test1: string;
  get test1(): string { return this._test1; }
  set test1(value: string): void { this._test1 = value; }
  
  private _test2: number;
  get test2(): number { return this._test2; }
  set test2(value: number): void { this._test2 = value; }
  
  // Comes in handy for various reasons.
  serialize() {
    return {
      test1: this._test1,
      test2: this._test2
    }
  }
  
  constructor(
    test1: string = "",
    test2: number = 0
  ) {
    // Setup interface any way you like.
    this._test1 = test1;
    this._test2 = test2;
  }
  
}
```
  
  
### Fallback if you're using an older version
```javascript
class UserInterface {
  
  _test1;
  get test1() { return this._test1; }
  set test1(value) { this._test1 = value; }

  _test2;
  get test2() { return this._test2; }
  set test2(value) { this._test2 = value; }

  serialize() {
    return {
      test1: this._test1,
      test2: this._test2
    }
  }

  constructor(
    test1 = "",
    test2 = 0
  ) {
    // Setup interface any way you like.
    this._test1 = test1;
    this._test2 = test2;
  }

}
```


### Interface (Variable)
```javascript
// You could define in the same file if the project is small
// otherwise I recommend the interface is placed on its own.

const newEmptyUser = new UserInterface(); // -> Empty (Constructor is optional in this case)
newEmptyUser.test1 = "test1";
newEmptyUser.test2 = 100;
const serializedData1 = newEmptyUser.serialize();

const newUser = new UserInterface("test1", 100); // -> Default Values 
const serializedData2 = newUser.serialize();
```



### Interface Extending Class
```javascript
// You can set this up however you like. Enjoy!
class DemoClass extends UserInterface {
  
  constructor(
    test1,
    test2
  ) {
    super(
      test1,
      test2
    );
  }
  
}
```


