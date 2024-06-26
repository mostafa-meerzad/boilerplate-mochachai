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

`isString(val, message)` or `isNotString(val, message)` asserts that the actual value is a string.

`include(string, val, message)` and `notInclude(string, val, message)` work for strings too! include() asserts that the actual string contains the expected substring.

`match(string, regex)` asserts that the actual value matches the second argument regular expression. `.notMatch(string, regex)` is the opposite.

`property(obj, prop, message)` asserts that the actual object has a given property. `notProperty(obj, prop, message)` is the opposite.

`typeOf(obj, obj-type-in-string)` checks if the provided object's type is the stringified equivalent of the provided type in string, `notTypeOf(obj, obj-type-in-string)` is the opposite.

`instanceOf(obj, constructor)` asserts that an object is an instance of a constructor. `notInstanceOf(obj, constructor)` is the opposite.

Mocha allows you to test asynchronous operations like calls to API endpoints with a plugin called `chai-http`.

```js
suite('GET /hello?name=[name] => "hello [name]"', function () {
  test("?name=John", function (done) {
    chai
      .request(server)
      .keepOpen()
      .get("/hello?name=John")
      .end(function (err, res) {
        assert.equal(res.status, 200, "Response status should be 200");
        assert.equal(res.text, "hello John", 'Response should be "hello John"');
        done();
      });
  });
});
```

The test sends a GET request to the server with a name as a URL query string (?name=John). In the end method's callback function, the response object (res) is received and contains the status property.

The first assert.equal checks if the status is equal to 200. The second assert.equal checks that the response string (res.text) is equal to "hello John".

Also, notice the done parameter in the test's callback function. Calling it without an argument at the end of a test is necessary to signal that the asynchronous operation is complete.

Finally, note the keepOpen method just after the request method. Normally you would run your tests from the command line, or as part of an automated integration process, and you could let chai-http start and stop your server automatically.

However, the tests that run when you submit the link to your project require your server to be up, so you need to use the keepOpen method to prevent chai-http from stopping your server.

To send a PUT request and a JSON object to the '/travellers' endpoint, you can use `chai-http` plugin's `put` and `send` methods:

```js

chai
  .request(server)
  .keepOpen()
  .put('/travellers')
  .send({
    "surname": [last name of a traveller of the past]
  })
  ...
```
