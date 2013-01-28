---
layout: post
title: Unit testing nodejs modules with Q promises (or why is my code always perfect?)
---

If not done carefully, unit testing with assertions inside promise Callback and Errorback functions can be misleading and make it look like your code is perfect all the time!

When running unit tests the `assert` API throws exceptions to indicate when things aren't going as expected. For example:

<pre><code>
var assert = require('assert');
function myTest(aValue) {
   assert.ok(aValue, "myTest(aValue) expected something to be passed");
}
</code></pre>

But if you are testing inside an promise Callback or Errback the exception get's caught by the wrapper. Consider this snippet:

<pre><code>
var aModule = require('someModule');

aModule.doPromisedThing()
.then(function(aValue) {
  assert.ok(aValue, "Expected aValue to be set");
}, function(aError) {
  assert.fail(aError, null, "Shouldn't be here!");
});
</code></pre>

Here we would expect an assertion if something here went wrong, but in practicality the promise library has caught the exception. Since if we are in the Callback when the error occurs, we can't get to the Errback, and if we are in the Errback then there is nowhere else to handle the error since we are already supposed to be handling the errors!

So what do we do?

The answer is quite simple and sits in a little block on the Q README titled [The End](https://github.com/kriskowal/q#the-end).

By simply ensuring the 'thenable' chain finishes with a simple `.done()` any exceptions thrown in the Callback or Errback are re-thrown.

Our previous code sample becomes:

<pre><code>
var aModule = require('someModule');

aModule.doPromisedThing()
.then(function(aValue) {
  assert.ok(aValue, "Expected aValue to be set");
}, function(aError) {
  assert.fail(aError, null, "Shouldn't be here!");
}).done();
</code></pre>

