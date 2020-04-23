# Stacks and Queues

>It is useful to also know that you can use a JavaScript array to implement a stack and/or a queue. In JavaScript, the array push() and pop() methods more or less resemble the operations in a stack. Therefore, you may see implementations of a stack and its operations in JavaScript using JavaScript arrays. Javascript arrays also provide the shift() method that can be used to implement the dequeue operation in a queue. For the purpose of this lesson, we will not use the built-in array methods to implement stack or queue, we will be using a singly linked list (as shown in the above code) to implement a stack, and doubly linked list to implement a queue.

## 1. Create a stack class
 Walk through the Stack class in the curriculum and understand it well. Then write a Stack class with its core functions (push, pop) from scratch.

```js
class _Node {
  constructor(value, next) {
    this.value = value;
    this.next = next;
  }
}

class Stack {
  constructor() {
    this.top = null;
  }

  push(value) {
    this.top = new _Node(value, this.top);
  }

  pop() {
    const top = this.top;
    this.top = this.top.next; // Remove top from the stack

    return top;
  }

  peek() {
    return this.top;
  }

  isEmpty() {
    return !(!!this.top);
  }
}

function testStack() {
  const myStack = new Stack;
  console.log('Is empty: ' + myStack.isEmpty())
  myStack.push('foo')
  console.log('Is empty: ' + myStack.isEmpty())
  console.log(myStack.peek())
  myStack.pop()
  console.log('Is empty: ' + myStack.isEmpty())
  myStack.push('')

  
}
testStack()
```

Create a stack called starTrek and add Kirk, Spock, McCoy, and Scotty to the stack.

```js
const starTrek = new Stack;

starTrek.push('Kirk')
starTrek.push('Spock')
starTrek.push('McCoy')
starTrek.push('Scotty')
```

## 2. Useful methods for a stack
Using the Stack class above, implement the following helper functions outside of the class:
peek(): allows you to look at the top of the stack without removing it
isEmpty(): allows you to check if the stack is empty or not
display(): to display the stack - what is the 1st item in your stack?

Remove McCoy from your stack and display the stack

```js
const stackHelpers = {
  peek: function(stack) {
    return stack.top;
  },
  isEmpty: function(stack) {
    return !(!!stack.top);
  },
  display: function(stack) {
    let currentNode = stack.top;
    while (currentNode) {
      console.log(currentNode.value)
      currentNode = currentNode.next;
    }
  }
}

starTrek.pop()
starTrek.pop()
stackHelpers.display(starTrek)
```

## 3. Check for palindromes using a stack
A palindrome is a word, phrase, or number that is spelled the same forward and backward. For example, “dad” is a palindrome; “A man, a plan, a canal: Panama” is a palindrome if you take out the spaces and ignore the punctuation; and 1,001 is a numeric palindrome. We can use a stack to determine whether or not a given string is a palindrome.

Write an algorithm that uses a stack to determine whether a given input is palindrome or not. Use the following template as a starting point.

```js
function is_palindrome(s) {
    s = s.toLowerCase().replace(/[^a-zA-Z0-9]/g, "");
    
    const stack = new Stack;

    for (let char of s) { // Push every character onto the stack
      stack.push(char);
    }

    let sReversed = '';

    while (!stackHelpers.isEmpty(stack)) { 
      // Pop every character off the stack, effectively reversing the characters.
      sReversed += stack.pop().value;
    }

    return s === sReversed;
}

// True, true, true, false
console.log(is_palindrome("dad"));
console.log(is_palindrome("A man, a plan, a canal: Panama"));
console.log(is_palindrome("1001"));
console.log(is_palindrome("Tauhida"));
```

## 4. Matching parentheses in an expression
A stack can be used to ensure that an arithmetic expression has balanced parentheses. Write a function that takes an arithmetic expression as an argument and returns true or false based on matching parenthesis. As a bonus provide a meaningful error message to the user as to what's missing. For example, you are missing a ( or missing a ")".

For version 1, the parentheses you need to consider are ( and ). Finding a close parenthesis without an open parenthesis is an error (report the location of the close); reaching the end of the string while still "holding" an open parenthesis is also an error (report the location of the open).
```js
function parenthesesCheck(s) {
  const stack = new Stack;

  let openingIndex = [];
  let index = 0;
  for (let char of s) {
    if (char.match(/[(]/g)) {
      stack.push(char);
      openingIndex.push(index);
    }

    if (char.match(/[)]/g)) {
      if (!stack.peek() || !stack.peek().value === '(') {
        return 'Missing ( at index ' + index;
      } else {
        stack.pop();
        openingIndex.pop();
      }
    }

    index++;
  }

  if (!stack.isEmpty()) {return 'Missing ) at index ' + openingIndex[openingIndex.length - 1]}

  return 'All parentheses are closed';
}
parenthesesCheck('(1)+ 1')
```

## 5. Sort stack
Write a program to sort a stack such that the smallest items are on the top (in ascending order). You can use an additional stack, but you may not use any other data structure (such as an array, or linked list).
```js
function sortStack(stack) {
  const tempStack = new Stack;
  let temp; // We need one variable to grasp a node temporarily so that we can alter the chain of nodes moving from one stack to the other

  stackHelpers.display(stack)

  temp = stack.pop().value
  tempStack.push(temp)

  while (!stackHelpers.isEmpty(stack)) {
    temp = stack.pop().value
    while (tempStack.peek() && tempStack.peek().value < temp) {
      stack.push(tempStack.pop().value)
    }
    tempStack.push(temp)
  }

  stackHelpers.display(tempStack)
  return tempStack;
}

function testSortStack() {
  const stack = new Stack;

  stack.push(3)
  stack.push(1)
  stack.push(2)
  stack.push(7)
  stack.push(9)
  stack.push(5)

  let sortedStack = sortStack(stack);

}
testSortStack();
```

## 6. Create a queue using Singly linked list
Walk through the Queue class in the curriculum and understand it well. Then write a Queue class with its core functions (enqueue(), dequeue()) from scratch.

Create a queue called starTrekQ and add Kirk, Spock, Uhura, Sulu, and Checkov to the queue.
Implement a peek() function outside of the Queue class that lets you take a peek at what the 1st item in the queue is.
Implement a isEmpty() function outside the Queue class that allows you to check if the queue is empty or not
Implement a display() function outside of the Queue class that lets you display what's in the queue.
Remove Spock from the queue and display the resulting queue.
## 7. Create a queue class using Doubly linked List
Use the items listed in #6 and enqueue them to your queue.

Check to see who is first one on the Queue?
## 8. Queue implementation using a stack
There are many ways to implement a queue. You have learned using singly linked list, and doubly linked list. Keeping the concept of a queue in mind, implement a queue using 2 stacks and no other data structure. (You are not allowed to use a doubly linked list or array. Use your stack implementation with a linked list from above to solve this problem.)

## 9. Square dance pairing
As people come to the dance floor, they should be paired off as quickly as possible: man with woman, man with woman, all the way down the line. If several men arrive in a row, they should be paired in the order they came, and likewise if several women do. Maintain a queue of "spares" (men for whom you have no women yet, or vice versa), and pair them as appropriate.

F Jane

M Frank

M John

M Sherlock

F Madonna

M David

M Christopher

F Beyonce

Female dancer is Jane, and the male dancer is Frank
Female dancer is Madonna, and the male dancer is John
Female dancer is Beyonce, and the male dancer is Sherlock
There are 2 male dancers waiting to dance

## 10. The Ophidian Bank
At the Ophidian Bank, a single teller serves a long queue of people. New customers join the end of the queue, and the teller will serve a customer only if they have all of the appropriate paperwork. Write a representation of this queue; 25% of the time (random), a customer's paperwork isn't quite right, and it's back to the end of the queue. Show what a few minutes of the bank's lobby would look like.