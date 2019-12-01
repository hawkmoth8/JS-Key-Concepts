# What are `prototype` and `__proto__`?

the only true difference between `prototype` and `__proto__` is that the former is a property of a class constructor, while the latter is a property of a class instance.

```javascript
function Foo() {}
const f = new Foo();
console.log(Foo.prototype === f.__proto__); //true
```

# Prototypal Inheritance

```javascript
var parent = {
  foo: function() {
    console.log("bar");
  }
};
var child = Object.create(parent);
console.log(child.__proto__ === parent); //true
```

So what is it doing?
Essentially, it creates a new, empty object that has parent in its prototype chain. That means that even though child doesn’t have its own `foo()` method, it has access to the `foo()` method from parent.

if we `console.log(child)`, we will see

![](./prototypal-inheritance.jpg)

# Prototypal Inheritance VS Classical Inheritance

```javascript
class Foo {
  constructor() {
    this.foo = "foo";
  }
}

class Bar extends Foo {
  constructor() {
    super();
  }

  some = function() {
    console.log("some");
  };
}

const bar = new Bar();
console.log(bar.__proto__ === Bar.prototype); //true
console.log(bar.__proto__.__proto__ === Foo.prototype); //true
console.log(bar);
```

![](./pi-vs-ci-1.jpg)

```javascript
function Foo() {
  this.foo = "foo";
}

function Bar() {
  Foo.call(this);
  this.some = function() {
    console.log("some");
  };
}

Bar.prototype = Object.create(Foo.prototype);
const bar = new Bar();
console.log(bar);
console.log(bar.__proto__ === Bar.prototype); //true
console.log(bar.__proto__.__proto__ === Foo.prototype); //true
```

![](./pi-vs-ci-2.jpg)
