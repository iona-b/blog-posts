![Cover Image](./cover-image.jpg)

*photo by [@pkmfaris](https://unsplash.com/@pkmfaris)*

# Recursion Revealed

As a recent software engineering graduate, I've been spending a lot of time readying myself for technical interviews. Part of this process has been learning more about data structures and algorithms. In this post, I'll be discussing why recursion is useful and how we can implement it. I'll also examine two common recursion examples, how to sum numbers from 1 to n and how to reverse a string using recursion.

## What is Recursion?

We can say that a function is recursive if it calls itself as a subroutine. Personally, I've found that, while this makes sense in theory, it can take a while to really wrap your head around how recursion works. Essentially what we're doing is breaking something down into smaller problems by calling the function on itself. Once we reach a point where the problem can be solved without being further reduced, we stop the recursion call and return the answer.

### When to Use Recursion Rather Than Iteration?

Recursion and iteration can often be used to similarly solve problems. Why then would we choose to implement a recursive solution rather than a straightforward iterative one? Here are some points to take into consideration when deciding:

1. Recursive functions are normally shorter than iterative ones, which can (but doesn't always!) lead to cleaner and more legible code.
2. Recursive solutions are often able to handle more complex problems and structures than iterative solutions. If you're dealing with, for instance, an elaborate tree structure, you'll probably want to use recursion.
3. Iterative functions are generally faster than recursive ones, so if your program is suited to iteration and speed is important, you may want to consider the former.
4. A downside of recursion can be the stack limit. If this is relevant to your function, iteration may be preferable.

### Elements of Recursion

When creating a recursive function, we need to include the following elements:

1. A Base Case
    - Usually this is activated when a specific condition is met, for instance when the input reaches 0.
    - When the function reaches the base case, it stops calling itself and returns the result.
2. Logic to Reach Base Case
    - This is where the function performs logic that will bring us closer to the base case.
    - For instance, if the condition for the base case is that the input is equal to 0, this logic could be that 1 is subtracted from the input on each call.
    - Without this logic, we could get stuck in an infinite loop.
3. Recursive Call
    - The recursive call is where we call the function within itself.

![Spiral](./spiral.jpg)

*photo by [@benji3pr](https://unsplash.com/@benji3pr)*

### Examples of Recursive Functions

#### **Example 1: Recursively Sum Numbers From 1 to n**

In this example, we'll write a function that takes a number, *n*, and returns the sum of all the numbers from 1 to n:

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

When we call ```recursiveSumToN(5)```, we'll get the sum of 1 + 2 + 3 + 4 + 5, which equals 15.

How does this function work? As outlined above, we need a base case, logic to reach the base case, and a recursive call. We can see below which lines of code fulfil each of these responsibilities:

```javascript
const recursiveSumToN = (n) => {

  if (n <= 1) {
    // BASE CASE: We want to count the numbers from 1 to n, so we need to stop when n === 1.
    return n; 
  } else {
    // LOGIC TO REACH BASE CASE AND RECURSIVE CALL: If n is > 1, we haven't reached our base case, so we need to call our function again.
    return n + recursiveSumToN(n - 1); 
  }

}

recursiveSumToN(5);

// 15
```

So, for as long as *n*, i.e. the input, is more than 1, our function calls itself using *n - 1*. By continuously reducing *n* by 1, we are working towards the base case and so don't end up in an infinite loop.

The above function can be illustrated like so:

```javascript
recursiveSumToN(5)
  // this translates to:
  recursiveSumToN(4) + 5
    // =>
    recursiveSumToN(3) + 4
      // =>
      recursiveSumToN(2) + 3
        // =>
        recursiveSumToN(1) + 2
        // 1
```

The function works in two steps. It repeatedly calls recursiveSumToN until it reaches the base case. Once it fulfils this base case, it begins to resolve the other function calls.

It can also be useful to add some console.logs to our code to see the order in which things are happening:

```javascript
const recursiveSumToN = (n) => {

    console.log("n: " + n);

    if (n <= 1) {
        console.log("We've hit the base case!");
        return n;
    } else {;
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

So, *n* decreases by 1 each time until we hit our base case and the function returns our answer.

![Circles](./circles.jpg)

*photo by [@robertbye](https://unsplash.com/@robertbye)*

#### **Example 2: Recursively Reversing a String**

In this second example, we're going to look at a function that takes a string, *string*, and reverses it. This is a problem that can be solved in a number of ways, including iteratively, however we'll take a look at a potential recursive solution:

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

// olleh
```

As we can see, the output of this function is the reverse of the original *string*. In this case "hello" becomes "olleh".

Below, we can see the base case, logic, and recursive call.

```javascript
function recursiveReverseString(string) {

  if (string === "") {
    // BASE CASE: Once the string is empty, we have reached our base case.
    return "";
  }
  else {
    // LOGIC TO REACH BASE CASE AND RECURSIVE CALL: One character is removed each time the function is called until we reach our base case.
    return recursiveReverseString(string.substr(1)) + string.charAt(0);
  }
}

recursiveReverseString("hello");
// olleh
```

We can also add some console.logs to see how the string changes with each call:

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

Each time the recursiveReverseString function is called with one fewer character, until we have an empty string. The function then resolves each of the calls and finally outputs the reverse of the original string.

### Practice

Being able to implement recursion can be very useful, especially in a technical interview. [HackerRank](https://www.hackerrank.com/domains/algorithms?filters%5Bsubdomains%5D%5B%5D=recursion), [Codewars](https://www.codewars.com/collections/recursion-1), and [LeetCode](https://leetcode.com/explore/featured/card/recursion-i/) have a variety of recursion-based exercises for you to learn more, develop your skills, and practice.


### Sources

1. "[When To Use Recursion/When To Use Iteration](https://www.csie.ntu.edu.tw/~course/10420/Resources/lp/node37.html)", CSIE, Accessed November 6, 2020
2. "[Principle of Recursion](https://leetcode.com/explore/learn/card/recursion-i/250/principle-of-recursion/1439/)", LeetCode, Accessed November 6, 2020
3. "[What is the function of recursion? Why do we need recursion in programming?](https://www.quora.com/What-is-the-function-of-recursion-Why-do-we-need-recursion-in-programming)", Quora, Accessed November 6, 2020
4. "[Recursion Explained (with Examples)](https://dev.to/christinamcmahon/recursion-explained-with-examples-4k1m)", Christina McMahon on DEV, Accessed November 6, 2020
5. "[Recursion and Stack](https://javascript.info/recursion)", Christina McMahon on DEV, Accessed November 6, 2020