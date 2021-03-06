# [](#variations-on-a-structure)Variations on a structure

There is a common problem in javascript where you have to convert a data structure from one form to another. However it's complicated as you often run out of names.

eg. `var foo = { a: [1,2,3] }` is known as a "foo" object. And we have a function that expects a "foo" object.

But what if we, for some reason have something that is _almost_ a foo object: `var foo = { a: '1,2,3' }`. 
We could just convert inline like `foo.a = foo.a.split(',')`. But if this is a common conversion we will have a lot of duplicated logic and will quickly lead to confusion. 

To me this is a naming problem. If we had a system of saying this is a `foo`, `foo_1`, or `foo_N` we could define more descriptively what those variations entail. And provide functions to convert from `foo_1 -> foo`.

Then it becomes possible to make a rule where structures are only ever converted from one form to another via a function.  And to put in checks to say "i expect this object to be of this particular form"

First step is to define the "natural" structure. So in js that means date objects for dates, arrays for lists and ints / floats for number values.

Now say we fetch an object over a json api. Most things should be in their natural structure, except for date objects. So the api gives us a `foo1` and we have to convert that to `foo`.

Now we want to populate an edit-form with the object. Date objects are still fine, but arrays need to be serialized to comma-separated strings. And maybe some nested objects need to be flatten. So this will be `foo -> foo2`.

When the form is submitted we just need a function `foo2 -> foo` and then we can also have a `foo -> foo1` to send back to the api.
