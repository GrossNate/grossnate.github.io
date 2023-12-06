---
layout: post
title: "Learnings studying for the JS119 interview assessment"
date: 2023-12-05 23:38:00 -0600

---

These are all the ~~dumb mistakes I've made~~learning experiences I've given
myself while completing many practice problems. I'm keeping this more as a
running log for myself, but if it helps others then that's great! Also note that
I'll stop adding to this document once I have the interview because I don't want
to risk revealing anything from the interview itself. There are also one or two
things that I learned I needed to work on from the computer assessment and I'm
intentionally not including them here.

- Watch out for JavaScript inserting semicolons wherever it wants. This is one
  of the many terrible "features" of JavaScript, but I thought I pretty much had
  it under control. Then I spent an embarrassing amount of time trying to figure
  out why a function I was writing was returning `undefined`. Well, take a look
  at this:
  ```javascript
  return
    someString
      .split("")
      .reduce(some logic here);
  ```
  Is there any logical reason that JavaScript should assume you want it to
  insert a semicolon after `return`? No. Does it do that anyway? Yes.
- If you notice a requirement or edge case that's not covered by a test case,
  create the test case. We've done a lot of string processing exercises, and in
  one I did on an outside site, the instructions said not to be case-sensitive,
  but in the sample test cases they had only lowercase characters. It was easy
  to change my `RegExp` to be case-insensitive, but I missed it at first because
  I thought I'd just remember to do it. I think I'm going to make sure to really
  think about any provided test cases to ensure I have full coverage.
- This brings me to another thing - numbers. Remember there's a
  `Number.MAX_SAFE_INTEGER`. I don't know if this will actually come up in the
  interview, but if the problem involves numbers then it's probably good to ask
  "how big?"
- We've done so much with arrays that I think it's helpful to review how objects
  work, how to make copies, etc. In the few practice problems I did recently, I
  realized I was struggling more than with arrays.
  - One little aside related to this. I solved one problem by creating an array
    of objects (this was probably the hard way of doing things) and I did
    something like `let foo = Array(10).fill(Object());` and of course I got an
    array of 10 elements and each element was a reference to the same one
    object. 🤦

I'm going to add more to this later.
