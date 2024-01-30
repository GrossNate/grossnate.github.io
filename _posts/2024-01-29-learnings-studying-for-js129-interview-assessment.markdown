---
layout: post
title: "Learnings studying for the JS129 interview assessment"
date: 2024-01-29 12:02:00 -0600
---

# Outline

- Make a diagram of the prototypal chain, etc.
- Write something about `this`
- Write out examples of each way of making objects, including anything to
  demonstrate inheritance (where possible)

# Object Creation Patterns

## Factory Functions (aka Object Factories aka Factory Object Creation Pattern)

## Object Creation with Prototypes (aka Objects Linking to Other Objects - OLOO)

-prototypal inheritance

## Object Constructors (aka Constructors aka Constructor Functions)

-pseudo-classical inheritance
```javascript
function Timepiece() {}
Timepiece.prototype.getCurrentTime = function() {
  return new Date().getTime();
}

function WristWatch() {
  Timepiece.call(this);
}
WristWatch.prototype = Object.create(Timepiece.prototype);
WristWatch.prototype.constructor = WristWatch;
WristWatch.prototype.putOnWrist = function() {};

const sampleClock = new Timepiece();

const sampleWristWatch = new WristWatch();
```
![Diagram of how the prototypal chain works for object constructors](/docs/assets/images/constructor_functions_diagram.svg)

## Classes

-pseudo-classical inheritance

# Weird Stuff

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

- Here's another list item.

# Future thoughts

I'd like to re-learn Graphviz and the DOT Language to generate diagrams for this
blog, and it looks like there are a few plugins for Jekyll that will handle the
rendering. However I'm not going to fall down that rabbit hole and spend the
next two days just figuring out how to render some diagrams of objects.
