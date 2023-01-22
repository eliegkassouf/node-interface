### node-interface (Interface Structure Example for NodeJS.)

- ❓ On a large project or in a big team, interfaces provide a critical abstraction and the maintaining and use of them is something that Architects or Lead will focus on as a tool to keep code quality known and functionality expected
- ✳️ I prefer a stronger typed language so this is meant to <b>enforce</b> something you need to blueprint.
- 🛟 I find this helps reduce technical debt. Just remember to use proper variable names. Don't half ass it and you will thank yourself later if you ever need to maintain.



```
// My preferred method (depends on your version). 
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
      test1: this.test1,
      test2: this.test2
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
  
  
```
class UserInterface {
  
  // Fallback
  _test1;
  getTest1() { return this._test1; }
  setTest1(value) { this._test1 = value; }

  _test2;
  getTest2() { return this._test2; }
  setTest2(value) { this._test2 = value; }

  // Comes in handy for various reasons.
  serialize() {
    return {
      test1: this.getTest1(),
      test2: this.getTest2()
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


```
// You could define in the same file if the project is small
// otherwise I recommend the interface is placed on its own.
const newUser = new UserInterface("test1", 100);
```

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
