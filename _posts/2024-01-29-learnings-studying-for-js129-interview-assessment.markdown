---
layout: post
title: "Learnings studying for the JS129 interview assessment"
date: 2024-01-29 12:02:00 -0600
---

## Feedback From Last Interview (Paraphrased)

- When you've developed an algorithm/process, run a few test cases through it
  before you start coding (it's easier to fix the algorithm before you've
  written the code).
- Test code as you go along, no matter how confident you are.
- Don't just think silently - if you need to think, at least tell the
  interviewer what you're thinking about. Just think out loud as much as
  possible.
- If you say anything that makes you sound unsure, go ahead and test that thing.

## Object Creation Patterns

### Factory Functions (aka Object Factories aka Factory Object Creation Pattern)

- I know this well enough that I'm not going to write it out again.

### Object Creation with Prototypes (aka Objects Linking to Other Objects - OLOO)

- prototypal inheritance
- Not going to write this out again either, but the interesting thing is that
  you can chain prototypes together here also. For example:

  ```javascript
  const animalPrototype = {
    respire() {
      console.log("I'm taking in oxygen and providing it to my cells!");
    },
  };

  const mammalPrototype = Object.assign(Object.create(animalPrototype), {
    regulateOwnBodyTemperature() {
      console.log("I'm maintaining homeostasis of my body temperature!");
    },
  });
  ```

  Then you can use the `mammalPrototype` to create a new object and it will have
  access to methods for both the `mammalPrototype` and `animalPrototype`. If you
  want to get really tricky you can even use something like factory functions to
  create and initialize the objects. It's not covered quite like this in the
  course, though, so not sure how important this is.
  
### Object Constructors (aka Constructors aka Constructor Functions)

-pseudo-classical inheritance

```javascript
function Timepiece() {}
Timepiece.prototype.getCurrentTime = function () {
  return new Date().getTime();
};

function WristWatch() {
  Timepiece.call(this);
}
WristWatch.prototype = Object.create(Timepiece.prototype);
WristWatch.prototype.constructor = WristWatch;
WristWatch.prototype.putOnWrist = function () {};

const sampleClock = new Timepiece();

const sampleWristWatch = new WristWatch();
```

![Diagram of how the prototypal chain works for object constructors](/docs/assets/images/constructor_functions_diagram.svg)

### Classes

-pseudo-classical inheritance

## Weird Stuff

- If you create an object with an object constructor, JavaScript knows what type
  of object it is, even if it might not say so when you do `console.log(obj);`:

  ```javascript
  function ObjType1() {}
  function ObjType2() {}
  ObjType2.prototype = Object.create(ObjType1.prototype);
  // Intentionally forgetting to do `ObjType2.prototype.constructor = ObjType2;`

  const obj = new ObjType2();
  console.log(obj); // ObjType1 {}
  console.log(obj instanceof ObjType2); // true
  ```

  See? JavaScript just _knows_!

## Future thoughts

I'd like to re-learn Graphviz and the DOT Language to generate diagrams for this
blog, and it looks like there are a few plugins for Jekyll that will handle the
rendering. However I'm not going to fall down that rabbit hole and spend the
next two days just figuring out how to render some diagrams of objects.
