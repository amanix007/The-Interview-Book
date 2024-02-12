# Data Structure and Algorithms

[**Sorting Algorithm**](DSA/Sorting_Algorithm.md)

[**Search Algorithm**](DSA/Search_Algorithm.md)



# **Fibonacci**

**Question:** How do get nth Fibonacci number?

**Answer:** I create an array and start from iterate through.

Fibonacci series is one of the most popular interview question for beginners. so, you have to learn this one.

# **try 1**

```jsx
function fibonacci(n){
  var fibo = [0, 1];

  if (n <= 2) return 1;

  for (var i = 2; i <=n; i++ ){
   fibo[i] = fibo[i-1]+fibo[i-2];
  }

 return fibo[n];
}

> fibonacci(12);
  = 144
```

**Interviewer:** What is the run time complexity?

**you:** O(n)

**Interviewer:** can you make it recursive?

# **try 2**

```jsx
function fibonacci(n){
  if(n<=1)
    return n;
  else
    return fibonacci(n-1) + fibonacci (n-2);
}

> fibonacci(12);
  = 144

```

**Interviewer:** What is the run time complexity?

**You:** O(2n). [detail about complexity](http://stackoverflow.com/a/360773/1535443)

# **4. Greatest Common Divisor**

**Question:** How would you find the greatest common divisor of two numbers?

```jsx
function greatestCommonDivisor(a, b){
  var divisor = 2,
      greatestDivisor = 1;

  //if u pass a -ve number this will not work. fix it dude!!
  if (a < 2 || b < 2)
     return 1;

  while(a >= divisor && b >= divisor){
   if(a %divisor == 0 && b% divisor ==0){
      greatestDivisor = divisor;
    }
   divisor++;
  }
  return greatestDivisor;
}

> greatestCommonDivisor(14, 21);
  =7
> greatestCommonDivisor(69, 169);
  = 1

```

# **fancy algorithm**

**Sorry.** can't explain it. As i myself dont understand it 80% of the times. my algorithm analysis instructor told about this and stole if from class note (i am a good student, btw!)

```jsx
function greatestCommonDivisor(a, b){
   if(b == 0)
     return a;
   else
     return greatestCommonDivisor(b, a%b);
}

```

**Note:** use your brain to understand it.

# **5. remove Duplicate**

**Question:** How would you remove duplicate members from an array?

**Answer:** will start a while looping and keep an object/ associated array. If i find an element for the first time i will set its value as true (that will tell me element added once.). if i find a element in the exists object, i will not insert it into the return array.

```jsx
function removeDuplicate(arr){
  var exists ={},
      outArr = [],
      elm;

  for(var i =0; i<arr.length; i++){
    elm = arr[i];
    if(!exists[elm]){
      outArr.push(elm);
      exists[elm] = true;
   }
  }
  return outArr;
}

> removeDuplicate([1,3,3,3,1,5,6,7,8,1]);
  = [1, 3, 5, 6, 7, 8]

```

# **6. merge two sorted array**

**Question:** How would you merge two sorted array?

**Answer:** I will keep a pointer for each array and (read the code. and be careful about this one.)

```jsx
function mergeSortedArray(a, b){
  var merged = [],
      aElm = a[0],
      bElm = b[0],
      i = 1,
      j = 1;

  if(a.length ==0)
    return b;
  if(b.length ==0)
    return a;
  /*
  if aElm or bElm exists we will insert to merged array
  (will go inside while loop)
   to insert: aElm exists and bElm doesn't exists
             or both exists and aElm < bElm
    this is the critical part of the example
  */
  while(aElm || bElm){
   if((aElm && !bElm) || aElm < bElm){
     merged.push(aElm);
     aElm = a[i++];
   }
   else {
     merged.push(bElm);
     bElm = b[j++];
   }
  }
  return merged;
}

> mergeSortedArray([2,5,6,9], [1,2,3,29]);
 = [1, 2, 2, 3, 5, 6, 9, 29]

```

# **7. swap number without temp**

**Question:** How would you swap two numbers without using a temporary variable?

**Answer:** Waste time about thinking it. though u know the answer, act like you are thinking and take your time to answer this one.

```coffeescript
function swapNumb(a, b){
  console.log('before swap: ','a: ', a, 'b: ', b);
  b = b -a;
  a = a+ b;
  b = a-b;
  console.log('after swap: ','a: ', a, 'b: ', b);
}

> swapNumb(2, 3);
   = before swap:  a:  2 b:  3
   = after swap:  a:  3 b:  2

```

**bit manipulation**: Sorry, i can't explain this to you. Kinjal Dave suggested [logical conjunction](https://en.wikipedia.org/wiki/Logical_conjunction) to understand it. Waste 30 min there at your own risk.

```coffeescript
function swapNumb(a, b){
  console.log("a: " + a + " and b: " + b);
  a = a ^ b;
  b = a ^ b;
  a = a ^ b;
  console.log("a: " + a + " and b: " + b);
}

> swapNumb(2, 3);
  = a: 2 and b: 3
  = a: 3 and b: 2

```

# **8. string reverse**

**Question:** How would you reverse a string in JavaScript?

**Answer:** I can loop through the string and concatenate letters to a new string

# **try 1**

```jsx
function reverse(str){
  var rtnStr = '';
  for(var i = str.length-1; i>=0;i--){
    rtnStr +=str[i];
  }
  return rtnStr;
}

> reverse('you are a nice dude');
  = "edud ecin a era uoy"

```

**Interviewer:** You know concatenation performed well in modern browsers but becomes slow in older browsers like IE8. Is there any different way, you can reverse a string?

**Answer:** sure. i can use an array and also add some checking. if string is null or other than string this will fail. let me do some type check as well. Using this array is like using string buffer in some server side languages.

# **try 2**

```jsx
function reverse(str){
  var rtnStr = [];
  if(!str || typeof str != 'string' || str.length < 2 ) return str;

  for(var i = str.length-1; i>=0;i--){
    rtnStr.push(str[i]);
  }
  return rtnStr.join('');
}

```

**Interviewer:** What is the run time complexity?

**You:** O(n)

**Interviewer:** Can you make this better?

**You:** I can loop through half of the index and it will save little bit. (this is kind of useless, might not impress interviewer)

# **try 3**

```jsx
function reverse(str) {
  str = str.split('');
  var len = str.length,
      halfIndex = Math.floor(len / 2) - 1,
      revStr;
  for (var i = 0; i <= halfIndex; i++) {
    revStr = str[len - i - 1];
    str[len - i - 1] = str[i];
    str[i] = revStr;
  }
  return str.join('');
}

```

**Interviewer:** That works, but can u do it in a recursive way?

**You:** sure.

# **try 4**

```jsx
function reverse (str) {
    if (str === "") {
        return "";
    } else {
        return reverse(str.substr(1)) + str.charAt(0);
    }
}

```

# **try 5**

**Interviewer:** Can you use any build in method to make it little cleaner?

**You:** yes.

```jsx
function reverse(str){
  if(!str || str.length <2) return str;

  return str.split('').reverse().join('');
}

```

# **try 6**

**Question:** Can you make reverse function as string extension?

**Answer:** I need to add this function to the String.prototype and instead of using str as parameter, i need to use this

```jsx

String.prototype.reverse = function (){
  if(!this || this.length <2) return this;

  return this.split('').reverse().join('');
}

> 'abc'.reverse();
  = 'cba'

```

# **9. reverse words**

**Question:** How would you reverse words in a sentence?

**Answer:** You have to check for white space and walk through the string. Ask is there could be multiple whitespace.

```jsx
//have a tailing white space
//fix this later
//now i m sleepy
function reverseWords(str){
 var rev = [],
     wordLen = 0;
 for(var i = str.length-1; i>=0; i--){
   if(str[i]==' ' || i==0){
     rev.push(str.substr(i,wordLen+1));
     wordLen = 0;
   }
   else
     wordLen++;
 }
 return rev.join(' ');
}

```

**A quick solution with build in methods:**

```jsx
function reverseWords(str){
  return str.split(' ').reverse();
}

```

# **10. reverse in place**

**Question:** If you have a string like "I am the good boy". How can you generate "I ma eht doog yob"? Please note that the words are in place but reverse.

**Answer:** To do this, i have to do both string reverse and word reverse.

```jsx
function reverseInPlace(str){
  return str.split(' ').reverse().join(' ').split('').reverse().join('');
}

> reverseInPlace('I am the good boy');
 = "I ma eht doog yob"

```

**Interviewer:** ok. fine. can you do it without using build in reverse function?

**you:** (you mumbled): what the heck!!

```coffeescript
//sum two methods.
//you can simply split words by ' '
//and for each words, call reverse function
//put reverse in a separate function

//if u cant do this,
//have a glass of water, and sleep

```

# **11. First non repeating char**

**Question:** How could you find the first non repeating char in a string?

**Answer:** You must ask follow up questions.

**Clarification:** Is it case sensitive?

**Interviewer:** interviewer might say no.

**Clarification:** is it very long string or couple hundred?

**Interviewer:** Why does that matter

**you:** for example, if it is a very long string say a million characters and i want to check whether 26 English characters are repeating. I might check whether all characters are duplicated in every 200 letters (for example) other than looping through the whole string. this will save computation time.

**Interviewer:** For simplicity, you string is "the quick brown fox jumps then quickly blow air"

**Clarification:** (silly question) ascii or unicode.

```jsx
function firstNonRepeatChar(str){
  var len = str.length,
      char,
      charCount = {};
  for(var i =0; i<len; i++){
    char = str[i];
    if(charCount[char]){
      charCount[char]++;
    }
    else
      charCount[char] = 1;
  }
  for (var j in charCount){
    if (charCount[j]==1)
       return j;
  }
}

>firstNonRepeatChar('the quick brown fox jumps then quickly blow air');
 = "f"

```

this has one problem. It is not guaranteed that for in loop will be executed in order.

# **12. remove duplicate char**

**Question:** How will you remove duplicate characters from a sting?

**You:** This is very similar to first non repeating char. You will asks similar question. Is it case sensitive.

If interviewer says, this is case sensitive then life become easier you. If he says no. you can either use string.toLowercase() to make whole string lower. he might not like it. because return string will not posses the same case. So

```jsx
function removeDuplicateChar(str){
  var len = str.length,
      char,
      charCount = {},
      newStr = [];
  for(var i =0; i<len; i++){
    char = str[i];
    if(charCount[char]){
      charCount[char]++;
    }
    else
      charCount[char] = 1;
  }
  for (var j in charCount){
    if (charCount[j]==1)
       newStr.push(j);
  }
  return newStr.join('');
}

> removeDuplicateChar('Learn more javascript dude');
  = "Lnmojvsciptu"

```

**Note:**this has one problem. It is not guaranteed that for in loop will be executed in order.

**For case insensitive:** when u r setting property of charCount or increase counter, just make the char.toLowerCase(). or you can do something fancy with charCode (if you can deal with it.)

# **13. check palindrome**

**Question:** How will you verify a word as palindrome?

**Answer:** if you reverse a word and it becomes same as the previous word, it is called palindrome.

```jsx
function isPalindrome(str){
  var i, len = str.length;
  for(i =0; i<len/2; i++){
    if (str[i]!== str[len -1 -i])
       return false;
  }
  return true;
}

> isPalindrome('madam')
  = true
> isPalindrome('toyota')
  = false

```

or you can use build in method

```jsx
function checkPalindrom(str) {
    return str == str.split('').reverse().join('');
}

```

**Similar:** Find whether a string contains a contiguous palindromic substring in O(n) time. Can you solve the problem in O(1) time?

# **14. random between 5 to 7**

**Question:**If you have a function that generate random number between 1 to 5 how could u generate random number 1 to 7 by using that function?

**Answer:** Very simple. think of some basic arithmetic and you will get it.

```jsx
function rand5(){
   return 1 + Math.random() * 4;
}

function rand7(){
  return 5 + rand5() / 5 * 2;
}

```

# **15. missing number**

**Question:** from a unsorted array of numbers 1 to 100 excluding one number, how will you find that number.

**Explanation:** You have an array of numbers 1 to 100 in an array. Only one number is missing in the array. The array is unsorted. Find the missing number.

**Answer:** You have to act like you are thinking a lot. and then talk about the sum of a linear series of n numbers = n*(n+1)/2

```jsx
function missingNumber(arr){
  var n = arr.length+1,
  sum = 0,
  expectedSum = n* (n+1)/2;

  for(var i = 0, len = arr.length; i < len; i++){
    sum += arr[i];
  }

  return expectedSum - sum;
}

> missingNumber([5, 2, 6, 1, 3]);
  = 4

```

**Note:** this one will give u missing one number in any array of length

# **16. Sum of two**

**Question:** From a unsorted array, check whether there are any two numbers that will sum up to a given number?

**Answer:** Simplest thing in the world. double loop

```jsx
function sumFinder(arr, sum){
  var len = arr.length;

  for(var i =0; i<len-1; i++){
     for(var j = i+1;j<len; j++){
        if (arr[i] + arr[j] == sum)
            return true;
     }
  }

  return false;
}

> sumFinder([6,4,3,2,1,7], 9);
  = true
> sumFinder([6,4,3,2,1,7], 2);
  = false

```

**Interviewer:** What is the time complexity of this function

**You:** O(n2)

**Interviewer:** Can you make this better

**You:** Let me see. I can have an object where i will store the difference of sum and element. And then when i get to a new element and if i find the difference is the object, then i have a pair that sums up to the desired sum.

# **try 2**

```jsx
function sumFinder(arr, sum){
  var differ = {},
      len = arr.length,
      substract;

  for(var i =0; i<len; i++){
     substract = sum - arr[i];

     if(differ[substract])
       return true;
     else
       differ[arr[i]] = true;
  }

  return false;
}

> sumFinder([6,4,3,2,1,7], 9);
  = true
> sumFinder([6,4,3,2,1,7], 2);
  = false

```

similar problem: find the maximum difference of two numbers in an array [max difference](http://programmingpraxis.com/2011/04/01/maximum-difference-in-an-array/)

**Even tougher**[Finding three elements in an array whose sum is closest to an given number](http://stackoverflow.com/questions/2070359/finding-three-elements-in-an-array-whose-sum-is-closest-to-an-given-number)

# **17. Largest Sum**

**Question:** How would you find the largest sum of any two elements?

**Answer:** this is actually very simple and straight forward. Just find the two largest number and return sum of them

```jsx
function topSum(arr){

  var biggest = arr[0],
      second = arr[1],
      len = arr.length,
      i = 2;

  if (len<2) return null;

  if (biggest<second){
    biggest = arr[1];
    second = arr[0];
  }

  for(; i<len; i++){

   if(arr[i] > biggest){
      second = biggest;
      biggest = arr[i];
    }
   else if (arr[i]>second){
      second = arr[i];
   }

 }
 return biggest + second;
}

```

# **18. Counting Zeros**

**Question:** Count Total number of zeros from 1 upto n?

**Answer:** If n = 50. number of 0 would be 11 (0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100). Please note that 100 has two 0. This one looks simple but little tricky

**Explanation:** So the tick here is. if you have a number 1 to 50 the value is 5. just 50 divided by 10. However, if the value is 100. the value is 11. you will get by 100/10 = 10 and 10/10. Thats how you will get in the more zeros in one number like (100, 200, 1000)

```jsx
function countZero(n){
  var count = 0;
  while(n>0){
   count += Math.floor(n/10);
   n = n/10;
  }
  return count;
}

> countZero(2014);
  = 223

```

# **19. subString**

**Question:** How can you match substring of a sting?

**Answer:** Will use to pointer (one for string and another for the substring) while iterating the string. And will have another variable to hold the starting index of the initial match.

```jsx
function subStringFinder(str, subStr){
  var idx = 0,
      i = 0,
      j = 0,
      len = str.length,
      subLen = subStr.length;

   for(; i<len; i++){

      if(str[i] == subStr[j])
         j++;
      else
         j = 0;

      //check starting point or a match
      if(j == 0)
        idx = i;
      else if (j == subLen)
        return idx;
  }

  return -1;
}

> subStringFinder('abbcdabbbbbck', 'ab')
  = 0
> subStringFinder('abbcdabbbbbck', 'bck')
  = 9

//doesn't work for this one.
> subStringFinder('abbcdabbbbbck', 'bbbck')
  = -1

```

**Question:** How can you fix the last problem?

**Answer:** figure out yourself.

# **20. Permutations**

**Question:** How would you create all permutation of a string?

**Answer:** This could be a tough one based on you level of knowledge about algorithm.

```jsx
function permutations(str){
var arr = str.split(''),
    len = arr.length,
    perms = [],
    rest,
    picked,
    restPerms,
    next;

    if (len == 0)
        return [str];

    for (var i=0; i<len; i++)
    {
        rest = Object.create(arr);
        picked = rest.splice(i, 1);

        restPerms = permutations(rest.join(''));

       for (var j=0, jLen = restPerms.length; j< jLen; j++)
       {
           next = picked.concat(restPerms[j]);
           perms.push(next.join(''));
       }
    }
   return perms;
}

```

**Explanation:**

- **Idea:** Idea is very simple. We will convert the string to an array. from the array we will pick one character and then permute rest of it. After getting the permutation of the rest of the characters, we will concatenate each of them with the character we have picked.
- **step-1** First copy original array to avoid changing it while picking elements
- **step-2** Use splice to removed element from the copied array. We copied the array because splice will remove the item from the array. We will need the picked item in the next iteration.
- **step-3** [1,2,3,4].splice(2,1) will return [3] and remaining array = [1,2,4]
- **step-4** Use recursive method to get the permutation of the rest of the elements by passing array as string

# **Stack and Queue**

**Question:** How will you implement stack and queue with JavaScript?

**Answer:** stack is already implemented in JavaScritp array. you can simply call `push` and `pop` method.

```jsx
var myStack = [];

//push
myStack.push(1);
myStack.push(2);
myStack.push(3);

//pop
myStack.pop(); //3
myStack.pop(); //2
myStack.pop(); //1

```

### **Queue**

Queue is pretty much same. other than calling `pop` you will use `shift` method to get the element in the front side of your array.

```jsx
var myQueue = [];

//push
myQueue.push(1);
myQueue.push(2);
myQueue.push(3);

//pop
myQueue.shift(); //1
myQueue.shift(); //2
myQueue.shift(); //3

```

# **Priority Queue**

you have to use a maximizing heap to manage a priority queue. Hence while extracting, you just get the one on the top and while inserting you will do it at the bottom

```jsx
//for now read the link.

```

ref: i have implemented simplified version of [priorityQueueJS](https://github.com/janogonzalez/priorityqueuejs/blob/master/index.js)

# **Singly Linked List**

**Question:** How will you create a linked list in JavaScript?

**Answer:** if you don't have any idea about linked list. read: [wiki: linked list](https://en.wikipedia.org/wiki/Linked_list)

to have linked list, you need a node object that will point to the next. you need one pointers (head) to point the first node of your linked list. Besides, you need methods to add and remove node from your linked list

let's get started. We have an object LinkedList and that has one property head (a pointer)

```jsx
function LinkedList(){
  this.head = null;
}

```

to create add elements, will use a push method in the prototype of the object. push method will take value and will create a node object. if there is no head, then node will be the value of head. if there is a head. then we have to walk through the linked list chain to read the tail (tail is where the next node is null). We will simple set the of next at the tail to node.

```jsx

LinkedList.prototype.push = function(val){
    var node = {
       value: val,
       next: null
    }
    if(!this.head){
      this.head = node;
    }
    else{
      current = this.head;
      while(current.next){
        current = current.next;
      }
      current.next = node;
    }
  }

```

Now. create a linked list and push values in it.

```coffeescript
var sll = new LinkedList();

//push node
sll.push(2);
sll.push(3);
sll.push(4);

//check values by traversing LinkedList
sll.head; //Object {data: 2, next: Object}
sll.head.next; //Object {data: 3, next: Object}
sll.head.next.next; //Object {data: 4, next: null}

```

read: [Advantage and disadvantage of linked list](https://en.wikipedia.org/wiki/Linked_list)

copied from: [Nicholas Zakas: linked list](http://www.nczonline.net/blog/2009/04/13/computer-science-in-javascript-linked-list/)

# **Doubly Linked List**

for doubly linked list there will be a link backward to the previous element. Your node object will look like

```coffeescript
var node = {
  value: val,
  next: null,
  previous: null
}

```

```jsx
function DoublyLinkedList(){
   this.head = null;
}

DoublyLinkedList.prototype.push = function(val){
   var head = this.head,
       current = head,
       previous = head;
  if(!head){
      this.head = {value: val, previous:null, next:null };
  }
  else{
      while(current && current.next){
         previous = current;
         current = current.next;
      }
     current.next = {value: val, previous:current, next:null}
  }
}

```

```jsx
//test at least once
var dll = new DoublyLinkedList();
dll.push(2);
dll.push(3);
dll.push(4);
dll.push(5);
//trust me it works

```

get most of it from: [doubly linked list](https://github.com/nzakas/computer-science-in-javascript/blob/master/data-structures/doubly-linked-list/doubly-linked-list.js)

# **Remove Node from Singly LL**

**Question:** How could you write an extension to remove a node from a LL

If you want to remove a node from your linked list you have to find the node. There are three conditions here

- case -1: your targeted node is in the head. you have to replace the head with the next node
- case -2: your targeted node is in the tail. you just have to remove it from the tail. Hence next of the node before the tail will be null.
- case-3: your targeted node is in the middle of the LinkedList, you have to make the node after your targeted node to be the next node of the node before your targeted node.

let's do it

```jsx

LinkedList.prototype.remove = function(val){
    var current = this.head;
    //case-1
    if(current.value == val){
       this.head = current.next;
    }
    else{
      var previous = current;

      while(current.next){
        //case-3
        if(current.value == val){
          previous.next = current.next;
          break;
        }
        previous = current;
        current = current.next;
      }
      //case -2
      if(current.value == val){
        previous.next == null;
      }
    }
  }

```

Now if you want to remove you can just pass the value

```

sll.remove(3);
sll.remove(1);

```

### **remove last element doesnt work**

# **Reverse Singly Linked List**

**Question:** How would you reverse a singly LL (no loop)?

**Answer:** Just walk through the LL and put the nodes in an array. This would be easier other than using remove function (if LL have one), because to remove a single item from the end of the SLL you have to walk all way to the end of the SLL every single time. Here you are just walking once.

### **Iterative**

```jsx
function reversesll(sll){

  if(!sll.head || !sll.head.next) return sll;

  var nodes=[],
    current = sll.head;
  //storing all the nodes in an array
  while(current){
    nodes.push(current);
    current = current.next;
  }

  var reversedLL = new LinkedList();

  reversedLL.head = nodes.pop();
  current = reversedLL.head;

  var node = nodes.pop();
  //make sure to make next of the newly inserted node to be null
  //other wise the last node of your SLL will retain its old next.
  while(node){
     node.next = null;
     current.next = node;

     current = current.next;
     node = nodes.pop();
  }
  return reversedLL;
}

```

test at least once.

```coffeescript
//create the LL
var sll = new LinkedList();
sll.push(1);
sll.push(2);
sll.push(3);
sll.push(4);
sll.push(5);

//test it
reversesll(sll);
//{head: {value:5, next:{value: 4, next: {value: 3, next: {value:2, next:{value:1, next: null}}}}}}

```

### **Recursive**

```jsx
//search it and implement it

```

**question**Given number k, for Singly linked list, skip k nodes and then reverse k nodes, till the end.

# **Reverse Doubly LL**

**Question:** reverse the doubly linked list without using extra space

**Answer:**

```jsx
function reverseDoublyLL(dll){
   var head = dll.head,
       current = dll.head,
       tmp;
   while(current){
      tmp = current.next;
      current.next = current.previous;
      current.previous = tmp;
      if(!tmp){
         //set the last node as header
         dll.head = current;
      }
      current = tmp;
   }
  return dll;
}

```

```jsx
//test it at least once
//or trust me it works

```

ref: [career cup](http://www.careercup.com/question?id=5313007689138176)

# **kth node from End**

**Question:** How could you get the Kth node from the end (no loop)

**Answer:**

```jsx
function kthFromEnd(sll, k){
   var node = sll.head,
       i = 1,
       kthNode;
   //handle, 0 or negative value of k
   if(k<=0) return;

    while(node){
      if(i == k) kthNode = sll.head;
      else if(i-k>0){
       kthNode = kthNode.next;
      }
      i++;

      node = node.next;
    }
   return kthNode;
}

```

```coffeescript
//create the LL
var sll = new LinkedList();
sll.push(1);
sll.push(2);
sll.push(3);
sll.push(4);
sll.push(5);

//test at least once
kthFromEnd(sll, 1); //Object {value: 5, next: null}
kthFromEnd(sll, 3); //Object {value: 3, next: Object}

```

# **Delete kth node from the end**

**Question:** How could you delete kth node from the end of a singly LL (no loop)

```jsx
function deleteKthFromEnd(sll, k){
   var node = sll.head,
       i = 1,
       kthNode,
       previous;
   if(k<=0) return sll;

    while(node){
      if(i == k) kthNode = sll.head;
      else if(i-k>0){
       previous = kthNode;
       kthNode = kthNode.next;
      }
      i++;

      node = node.next;
    }
    //kth node is the head
    if(!previous)
       sll.head = sll.head.next;
    else{
     previous.next = kthNode.next;
   }
   return sll;
}

```

test at least once

```coffeescript
//test at least once
var sll = new LinkedList();
sll.push(1);
sll.push(2);
sll.push(3);
sll.push(4);
sll.push(5);

deleteKthFromEnd(sll, 2);
//{head: {value:1, next:{value: 2, next: {value: 3, next: {value:1, next:null}}}}}

```

# **Delete a node from doubly LL**

**Question:** How could you delete a node from a doubly linked list?

**Answer:** there could be four cases

**delete head:** very simple, make the second node as head. and dont forget to set previous of new head to null.

**node in the middle:** skip break the chain, skip current node. hence next of previous node would be the next of the current node. Besides, previous of the next node would be previous node

**delete tail:** its also simple, make the next of previous as null.

**didn't find:** dont do anything

```jsx
function deleteNodeDLL(val){
   var current = dll.head,
       previous;

   //delete head
   if(current.value == val){
      dll.head = current.next;
      //if there is only one node, then dll.head is null
      if(dll.head) dll.head.previous = null;
      return dll;
   }

   while(current.next){
      if(current.value == val){
         previous.next = current.next;
         current.next.previous = previous;
         return dll;
     }
     previous = current;
     current = current.next;
   }

   //delete last node
   if(current.value == val){
     previous.next = null;
   }
   return dll;
}

```

**Detect a loop in Singly Linked List**

`function detectLoop(sll){
   var slowPointer = sll.head, 
       fastPointer = sll.head;

   while(slowPointer && fastPointer && fastPointer.next){
     slowPointer = slowPointer.next;
     fastPointer = fastPointer.next.next;

     if(slowPointer == fastPointer){
        return true;
     }
   }
   return false;
}`
        

`//test at least once
var sll = new LinkedList();
sll.push(1);
sll.push(2);
sll.push(3);
sll.push(4);
sll.push(5);

detectLoop(sll); //false

//create a loop manually. point next of 5 to point 3
sll.head.next.next.next.next.next = sll.head.next.next

detectLoop(sll); //true`

# **Detect Node where loop started**

**Question:**

**Answer:** you will have two pointer slow and fast like you had to detect loop and they will meet somewhere. if fast one hit null (if thee is a way to hit null, fast one should hit if before the slower. because fast one moves fast (recally physics theories!)), there is no loop and returns null.

if there is a null and whenever both pointers meet, set slow pointer as head. Move both the pointer move by one step at a time

At the time of meet, fast one moved twice as much as slow one.

**think about it and find a way to explain it**

```coffeescript
function findLoopStart(sll){
    var slow = sll.head,
        fast = sll.head;
    while(slow && fast){
       slow = slow.next;

       //if hits null, then there is no loop
       if(!fast.next){
          return null;
       }

       fast = fast.next.next;
       if(slow == fast){
           slow = sll.head;
           while(slow != fast){
              slow = slow.next;
              fast = fast.next;
           }
           return slow;
       }
   }
}

```

ref: [detect where loop started](http://umairsaeed.com/2011/06/23/finding-the-start-of-a-loop-in-a-circular-linked-list/)

# **Find middle**

**Question:** How could you detect middle of a LL?

**Answer:** need two pointer one will move two step another one. when two step will hit null. you will get middle for the singly. think about it.

```jsx
//If you cant figure it out ourself. don't read further, do something else

```

# **Length of a Singly LL**

**Question:** there could be loop in the singly LL

**Answer:**

```jsx
//doesnt work.. somewhere gets stack overflow
//debug and find fix it
function getLength(sll){
   var head = sll.head,
       current = head,
       pointer = head,
       anotherPtr,
       len = 0;
    //use the previously written function
    var loopStartNode = findLoopStart(sll);
    if(!loopStartNode){
       while(current){
          current= current.next;
          len++;
       }
       return len;
    }
    else{
       anotherPtr = loopStartNode;
       while(pointer != anotherPtr){
          len += 2;
          pointer = pointer.next;
          anotherPtr = anotherPtr.next;
       }
       return len;
    }
}

```

# **Loop with duplicate**

**Question:** Write a function that will return true if a circular singly linked list has duplicate values

**Answer:**

```jsx
//code it man! dont be lazy

```

Similar question: [Find the length of a linked list which contains cycle.](http://www.careercup.com/question?id=68277)

```jsx
//just start a counter instead of checking duplicate

```

ref: [career cup](http://www.careercup.com/question?id=15026777)

# **Rotate by Kth Node**

**Question:** How could you rotate a Linked List by Kth Node?

or

**Question:**[Append the last n nodes of a linked list to the beginning of the list](http://www.careercup.com/question?id=15434720)

**Answer:** if the given linked list is: 1->2->3->4->5 and k is 3,the list should be modified to: 4->5->1->2->3.

```jsx
//will not work for k less than length-1
function rotateByKthNode(sll, k){
   var prevHead = sll.head,
       previous = sll.head,
       current = sll.head,
       i = 1;
   while(current.next){
     if(i==k+1){
       sll.head = current;
       previous.next = null;
     }
     previous = current;
     current = current.next;
     i++;
  }
  current.next = prevHead;
  return sll;
}

```

```coffeescript

rotateByKthNode(sll,3);
//{head: {value:4, next:{value: 5, next: {value: 1, next: {value:2, next:{value:3, next: null}}}}}}

```

ref: [rotate by kth Node](http://www.crazyforcode.com/rotate-linked-list-k-nodes/)

# **Insert Node to Sorted LL**

**Question:** Insert node in a sorted LL

**Answer:**

```coffeescript
function pushSorted(sll, val){
   var head = sll.head,
       current = head,
       previous;
   //value lower than head value
   if(val < sll.head.value){
      sll.head = {value: val, next: head};
      return sll;
   }

   while(current){
      if(current.value > val){
         previous.next = {value: val, next: current};
         return sll;
      }
      previous = current;
      current = current.next;
   }
   //value higher than the last node value
   previous.next = {value:val, next: null};
   return sll;
}

```

```coffeescript
var sll = new LinkedList();
sll.push(5);
sll.push(7);
sll.push(10);
sll.push(14);

pushSorted(sll, 9);
//{head: {value: 5, next: {value: 7, next: {value: 9, next: {value: 10, next: {value: 14, next: null}}}}}}

```

# **merge two unsorted array**

**Question:** How would you merge two unsorted linked list?

**Answer:**

ref: [merge two unsorted linked list to one sorted LL](http://www.careercup.com/question?id=15421981)

easier question: [merge two LL in alternate position](http://www.crazyforcode.com/merge-linked-list-linked-list-alternate-positions/)

# **Intersect of two LL**

**Question:** How could you find intersect of two SLL in single iteration?

**Answer:**

ref: [most detail: have 6 methods](http://www.geeksforgeeks.org/write-a-function-to-get-the-intersection-point-of-two-linked-lists/) or [has some animation](http://twistedoakstudios.com/blog/Post3280_intersecting-linked-lists-faster) or [intersection of two LL](http://www.crazyforcode.com/write-function-intersection-point-linked-lists-y-shape-2/) or [career cup](http://www.careercup.com/question?id=14952616)

# **sort Linked list**

**Question:** How would you sort a linked list?

**Answer:** you can use bubble, merge or similar sort

```

```

ref: [sort LL](https://vijayinterviewquestions.blogspot.com/2007/05/sorting-linked-list.html)

### **toggle as hard questions**

# **special sort**

**Question:** Given an integer linked list of which both first half and second half are sorted independently. Write a function to merge the two parts to create one single sorted linked list in place [do not use any extra space].

**Answer:**

ref: [career cup](http://www.careercup.com/question?id=5724466092965888)

# **Remove duplicate from unsorted LL**

**Question:** Delete the repeated elements in a unsorted singly linked list in O(n) time complexity without using extra space.

**Answer:**

```coffeescript
//get a crystal clear concept about space complexity
//also this question is in cracking the coding interview

```

ref: [career cup](http://www.careercup.com/question?id=5740629665513472)

# **circular Linked List**

If the next pointer of the last node points to the head node, it becomes circular linked list. On Singly or Doubly Linked List, you will know you hit the tail when you hit null. For circular linked list, you will know you hit the tail when you hit the head (the next of last one pointed to head).

```jsx
function CircularLinkedList(){
  this.head = null;
}

CircularLinkedList.prototype.push = function(val){
   var head = this.head,
       current = head,
       node = {value: val, next: null, previous: null};

   if(!head){
      node.next = node;
      node.previous = node;
      this.head = node;
   }
   else{
      while(current.next != head){
         current = current.next;
      }

      node.next = head;
      node.previous = current;

      head.previous = node;
      current.next = node;
   }
}

```

```jsx
var cll = new CircularLinkedList();
cll.push(3);
cll.push(4);
cll.push(5);
//trust me dude, it works

```

Now you can play with it to remove, sort, or insert into sorted or remove duplicate, blah blah blah

ref: [circular linked list](http://www.martinbroadhurst.com/articles/circular-linked-list.html)

# **Check whether a linked list is a palindrome**

**Question:**

**Answer:**

```jsx
//get the solution from cracking the coding interview
//or ggl it

```