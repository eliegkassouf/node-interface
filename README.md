### node-interface (Interface Structure Example for NodeJS)

- ❓ On a large projects or teams, interfaces provide a critical abstraction. It helps us auto generate documentation and allows architechs/engineers/leads to focus on as a tool to keep code quality known and functionality expected. 
- ‼️ If you're using Angular there is a better way to define and use interfaces (please consult the angular docs). This example is specifically for Node, Express.. (Flow is also another alternative).
- 🛟 I find this helps reduce technical debt. Just remember to use proper variable names. Don't half ass it and you will thank yourself later if you ever need to maintain.



### My preferred method (depends on your version). 
```
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
```
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
```
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
```
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


