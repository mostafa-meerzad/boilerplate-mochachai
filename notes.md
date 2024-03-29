# Testing with Chai testing library

Chai.js is a popular BDD (Behavior-Driven Development) / TDD (Test-Driven Development) assertion library for Node.js and the browser that can be delightfully paired with any javascript testing framework. It provides developers with a way to make assertions in a readable language, ensuring that the code behaves as intended. Chai.js supports the two most common styles of assertions:

1. **Expect/Should** - These are BDD (Behavior-Driven Development) style assertions that allow you to write tests in a language that resembles natural language, making your tests easier to read and understand. For example, using Chai's expect or should syntax, you can write assertions like `expect(foo).to.be.a('string');` or `foo.should.be.a('string');`.

2. **Assert** - This style is more classical and is inspired by Node.js's built-in `assert` module. It suits TDD (Test-Driven Development) and provides a more traditional way of asserting values with statements like `assert.typeOf(foo, 'string');`.

Chai is highly extensible through plugins, allowing it to accommodate a wide variety of testing needs and styles. It's designed to work both in Node.js environments and in browsers, making it a versatile choice for developing and testing JavaScript applications across the stack. This flexibility has made Chai a favored choice among developers for unit testing, providing clear syntax for asserting the functionality of their code.

## The syntax

```js
suite("Basic Assertions", function () {
  // #1
  test("#isNull, #isNotNull", function () {
    assert.isNull(
      null,
      "This is an optional error description - e.g. null is null"
    );
    assert.isNotNull(1, "1 is not null");
  });
  // #2
  test("#isDefined, #isUndefined", function () {
    assert.isDefined(null, "null is not undefined");
    assert.isUndefined(undefined, "undefined IS undefined");
    assert.isDefined("hello", "A string is not undefined");
  });
  // #3
  test("#isOk, #isNotOk", function () {
    assert.fail(null, "null is falsey");
    assert.fail("I'm truthy", "A string is truthy");
    assert.fail(true, "true is truthy");
  });
  // #4
  test("#isTrue, #isNotTrue", function () {
    assert.fail(true, "true is true");
    assert.fail(
      !!"double negation",
      "Double negation of a truthy value is true"
    );
    assert.fail(
      { value: "truthy" },
      "Objects are truthy, but are not boolean values"
    );
  });
});
```

`.isNull(val, message)` checks if the passed value is "null", `.isNotNull(val, message)` checks if the provided value is "not null"

`.isDefined(val, message)` checks if the passed value is "defined", `.isUndefined(val, message)` checks if the provided value is "not defined"

`.isOk(val, message)` will test for a truthy value, and `.isNotOk(val, message)` will test for a falsy value.

`.isTrue(val, message)` will test for the boolean value true and `.isNotTrue(val, message)` will pass when given anything but the boolean value of true

`.isFalse(val, message)` and `.isNotFalse(val, message)` also exist, and behave similarly to their true counterparts except they look for the boolean value of false.

`.equal(val1, val2, message)` compares objects using `==`. `.notEqual(val1, val2, message)` is the opposite

`.strictEqual(val1, val2, message)` compares objects using `===`. `.notStrictEqual(val1, val2, message)` is the opposite

`.deepEqual(val1, val2, message)` asserts that two objects are deep equal. `.notDeepEqual(val1, val2, message)` is the opposite

`.isAbove(val1, val2, message)` checks if val1 is greater than val2 `.isAtMost(val1, val2, message)` checks if the val1 is less than or equal to val2

`.isBelow(val1, val2, message)` checks if val1 is less than val2 `.isAtLeast(val1, val2, message)` checks if the val1 is greater than or equal to val2

Tests if a Value Falls within a Specific Range `.approximately(actual, expected, delta, [message])` Asserts that the actual is equal to expected, to within a +/- delta range.

```js
test("#approximately", function () {
  assert.approximately(weirdNumbers(0.5), 1, 0.5);
  assert.approximately(weirdNumbers(0.2), 1, 0.8);
});
```

`.isArray(val, message)` checks if the provided value is an array, `.isNotArray(val, message)` is the opposite.

`.include(array, val, message)` checks if the provided value is in the provided array, `.notInclude(array, val, message)` is the opposite.

`isString` or `isNotString` asserts that the actual value is a string.
