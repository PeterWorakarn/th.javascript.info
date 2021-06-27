# การแตกแขนงแบบมีเงื่อนไข: if, '?'

บางครั้ง เราจำเป็นต้องดำเนินการต่างๆ ตามเงื่อนไขที่แตกต่างกัน

ในการทำเช่นนั้น เราสามารถใช้คำสั่ง `if` และตัวดำเนินการแบบเงื่อนไข (conditional operator) `?` ซึ่งเรียกอีกอย่างว่าโอเปอเรเตอร์ "เครื่องหมายคำถาม (question mark)"

## คำสั่ง "if"

คำสั่ง `if(...)` จะประเมินเงื่อนไขในวงเล็บและรันบล็อกของโค้ดหากผลลัพธ์เป็น `จริง`

ตัวอย่าง:

```js run
let year = prompt('In which year was ECMAScript-2015 specification published?', '');

*!*
if (year == 2015) alert( 'You are right!' );
*/!*
```

ในตัวอย่างข้างต้น เงื่อนไขคือการตรวจความเท่ากันแบบง่ายๆ (`year == 2015`) แต่เราสามารถทำได้ซับซ้อนกว่านี้มาก

หากเราต้องการดำเนินการมากกว่าหนึ่งคำสั่ง เราต้องล้อมบล็อคโค้ดของเราไว้ในวงเล็บปีกกา:

```js
if (year == 2015) {
  alert( "That's correct!" );
  alert( "You're so smart!" );
}
```

เราแนะนำให้ล้อมบล็อคโค้ดด้วยวงเล็บปีกกา `{}` ทุกครั้งที่ใช้คำสั่ง `if` แม้ว่าจะมีเพียงคำสั่งเดียวให้ดำเนินการก็ตาม การทำเช่นนี้จะช่วยให้โค้ดอ่านง่ายขึ้น

## การแปลงค่าชนิดอื่นเป็นบูลีน (Boolean conversion)

คำสั่ง `if (…)` จะประเมินนิพจน์ (expression) ในวงเล็บและแปลงค่าใดๆก็ตามเป็นบูลีน

ทบทวนความจำได้จากบทนี้ <info:type-conversions>:

- เลข `0`, สตริงว่าง `""`, `null` `undefined` และ `NaN` จะกลายเป็น `false` เราจะเรียกค่าเหล่านี้ว่า "falsy"
- ส่วนที่เหลือจะเป็น `true` เราจะเรียกค่าเหล่านี้ส่า "truly"

ดังนั้นโค้ดภายใต้เงื่อนไขนี้จะไม่ทำงาน:

```js
if (0) { // 0 is falsy
  ...
}
```

...และภายใต้เงื่อนไขนี้โค้ดจะทำงานส่วนที่อยู่ในบล็อค (วงเล็บปีกกา) ต่อไป

```js
if (1) { // 1 is truthy
  ...
}
```

นอกจากนี้เรายังสามารถส่งค่าบูลีนที่ประเมินล่วงหน้า (pre-evaluated) ไปยังคำสั่ง `if` ได้ดังนี้:

```js
let cond = (year == 2015); // บรรทัดนี้หาก year เป็น 2015 จะเป็น `true` หากไม่จะเป็น `false` เก็บไว้ในตัวแปร

if (cond) {
  ...
}
```

## The "else" clause

The `if` statement may contain an optional "else" block. It executes when the condition is falsy.

For example:
```js run
let year = prompt('In which year was the ECMAScript-2015 specification published?', '');

if (year == 2015) {
  alert( 'You guessed it right!' );
} else {
  alert( 'How can you be so wrong?' ); // any value except 2015
}
```

## Several conditions: "else if"

Sometimes, we'd like to test several variants of a condition. The `else if` clause lets us do that.

For example:

```js run
let year = prompt('In which year was the ECMAScript-2015 specification published?', '');

if (year < 2015) {
  alert( 'Too early...' );
} else if (year > 2015) {
  alert( 'Too late' );
} else {
  alert( 'Exactly!' );
}
```

In the code above, JavaScript first checks `year < 2015`. If that is falsy, it goes to the next condition `year > 2015`. If that is also falsy, it shows the last `alert`.

There can be more `else if` blocks. The final `else` is optional.

## Conditional operator '?'

Sometimes, we need to assign a variable depending on a condition.

For instance:

```js run no-beautify
let accessAllowed;
let age = prompt('How old are you?', '');

*!*
if (age > 18) {
  accessAllowed = true;
} else {
  accessAllowed = false;
}
*/!*

alert(accessAllowed);
```

The so-called "conditional" or "question mark" operator lets us do that in a shorter and simpler way.

The operator is represented by a question mark `?`. Sometimes it's called "ternary", because the operator has three operands. It is actually the one and only operator in JavaScript which has that many.

The syntax is:
```js
let result = condition ? value1 : value2;
```

The `condition` is evaluated: if it's truthy then `value1` is returned, otherwise -- `value2`.

For example:

```js
let accessAllowed = (age > 18) ? true : false;
```

Technically, we can omit the parentheses around `age > 18`. The question mark operator has a low precedence, so it executes after the comparison `>`.

This example will do the same thing as the previous one:

```js
// the comparison operator "age > 18" executes first anyway
// (no need to wrap it into parentheses)
let accessAllowed = age > 18 ? true : false;
```

But parentheses make the code more readable, so we recommend using them.

````smart
In the example above, you can avoid using the question mark operator because the comparison itself returns `true/false`:

```js
// the same
let accessAllowed = age > 18;
```
````

## Multiple '?'

A sequence of question mark operators `?` can return a value that depends on more than one condition.

For instance:
```js run
let age = prompt('age?', 18);

let message = (age < 3) ? 'Hi, baby!' :
  (age < 18) ? 'Hello!' :
  (age < 100) ? 'Greetings!' :
  'What an unusual age!';

alert( message );
```

It may be difficult at first to grasp what's going on. But after a closer look, we can see that it's just an ordinary sequence of tests:

1. The first question mark checks whether `age < 3`.
2. If true -- it returns `'Hi, baby!'`. Otherwise, it continues to the expression after the colon '":"', checking `age < 18`.
3. If that's true -- it returns `'Hello!'`. Otherwise, it continues to the expression after the next colon '":"', checking `age < 100`.
4. If that's true -- it returns `'Greetings!'`. Otherwise, it continues to the expression after the last colon '":"', returning `'What an unusual age!'`.

Here's how this looks using `if..else`:

```js
if (age < 3) {
  message = 'Hi, baby!';
} else if (age < 18) {
  message = 'Hello!';
} else if (age < 100) {
  message = 'Greetings!';
} else {
  message = 'What an unusual age!';
}
```

## Non-traditional use of '?'

Sometimes the question mark `?` is used as a replacement for `if`:

```js run no-beautify
let company = prompt('Which company created JavaScript?', '');

*!*
(company == 'Netscape') ?
   alert('Right!') : alert('Wrong.');
*/!*
```

Depending on the condition `company == 'Netscape'`, either the first or the second expression after the `?` gets executed and shows an alert.

We don't assign a result to a variable here. Instead, we execute different code depending on the condition.

**It's not recommended to use the question mark operator in this way.**

The notation is shorter than the equivalent `if` statement, which appeals to some programmers. But it is less readable.

Here is the same code using `if` for comparison:

```js run no-beautify
let company = prompt('Which company created JavaScript?', '');

*!*
if (company == 'Netscape') {
  alert('Right!');
} else {
  alert('Wrong.');
}
*/!*
```

Our eyes scan the code vertically. Code blocks which span several lines are easier to understand than a long, horizontal instruction set.

The purpose of the question mark operator `?` is to return one value or another depending on its condition. Please use it for exactly that. Use `if` when you need to execute different branches of code.
