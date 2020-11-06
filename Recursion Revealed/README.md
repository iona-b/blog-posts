![Cover Image](./cover-image.jpg)

*photo by [@pkmfaris](https://unsplash.com/@pkmfaris)*

# Recursion Revealed

As a recent software engineering graduate, I've been spending a lot of time readying myself for technical interviews. Part of this process has been learning more about data structures and algorithms. In this post, I'll be discussing why recursion is useful and how we can implement it.

## What is Recursion?

We can say that a function is recursive if it calls itself as a subroutine. Personally, I've found that, while this makes sense theoretically, it can take a while to really wrap your head around how recursion works.

You might wonder how we can implement a function that calls itself. The trick is that each time a recursive function calls itself, it reduces the given problem into subproblems. The recursion call continues until it reaches a point where the subproblem can be solved without further recursion.

### Why is Recursion Useful?

Recursion is great.

### Elements of Recursion

All recursive algorithms must have the following:

Base Case (i.e., when to stop)
Work toward Base Case
Recursive Call (i.e., call ourselves)
The "work toward base case" is where we make the problem simpler. The recursive call, is where we use the same algorithm to solve a simpler version of the problem. The base case is the solution to the "simplest" possible problem (For example, the base case to adding a list of numbers would be if the list had only one number... thus the answer is the number).

Recursion is a method of solving problems where you solve smaller portions of the problem until you solve the original, larger problem. A method or function is recursive if it can call itself.

![Spiral](./spiral.jpg)

*photo by [@benji3pr](https://unsplash.com/@benji3pr)*

### Example of Recursion

#### Example 1: Recursively Numbers From 1 to n

In this example, we're going to look at a function that takes a number, *n*, and returns the sum of all the numbers from 1 to n.

```javascript
const recursiveSumToN = (n) => {

  if (n <= 1) {
    return n;
  } else {
    return n + recursiveSumToN(n - 1);
  }

}

recursiveSumToN(5);

// 15
```

Let's go through this line by line.

```javascript
const recursiveSumToN = (n) => {

  if (n <= 1) {
    return n;
  } else {
    return n + recursiveSumToN(n - 1);
  }

}

recursiveSumToN(5);

// 15
```

Let's add some console logs to see what comes out.

```javascript
const recursiveSumToN = (n) => {

  if (n <= 1) {
    console.log("n: " + n);
    console.log("We've hit the base case!");
    return n;
  } else {
    console.log("n: " + n);
    return n + recursiveSumToN(n - 1);
  }

}

recursiveSumToN(5);

// n: 5
// n: 4
// n: 3
// n: 2
// n: 1
// We've hit the base case!
// 15
```

![Circles](./circles.jpg)

*photo by [@robertbye](https://unsplash.com/@robertbye)*

#### Example 2: Recursively Reversing a String

```javascript
function recursiveReverseString(string) {

  if (string === "") {
    return "";
  }
  else {
    return recursiveReverseString(string.substr(1)) + string.charAt(0);
  }
}

recursiveReverseString("hello");
```

```javascript
function recursiveReverseString(string) {

  if (string === "") {
    return "";
  }
  else {
    return recursiveReverseString(string.substr(1)) + string.charAt(0);
  }
}

recursiveReverseString("hello");
```

```javascript
function recursiveReverseString(string) {

  if (string === "") {
    console.log("string: " + string);
    console.log("We've hit the base case!");
    return "";
  }
  else {
    console.log("string: " + string);
    return recursiveReverseString(string.substr(1)) + string.charAt(0);
  }
}

recursiveReverseString("hello");

// string: hello
// string: ello
// string: llo
// string: lo
// string: o
// string: 
// We've hit the base case!
// olleh
```

### Practice

Being able to implement recursion can be very useful, especially in a technical interview. [HackerRank](https://www.hackerrank.com/domains/algorithms?filters%5Bsubdomains%5D%5B%5D=recursion), [Codewars](https://www.codewars.com/collections/recursion-1), and [LeetCode](https://leetcode.com/explore/featured/card/recursion-i/) have a variety of recursion-based exercises for you to learn more, develop your skills, and practice.


### Sources

https://leetcode.com/explore/learn/card/recursion-i/250/principle-of-recursion/1439/
https://www.quora.com/What-is-the-function-of-recursion-Why-do-we-need-recursion-in-programming
https://dev.to/christinamcmahon/recursion-explained-with-examples-4k1m