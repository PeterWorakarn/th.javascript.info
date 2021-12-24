# จาวาสคริปต์พิเศษ

ในบทนี้เราจะสรุปฟีเจอร์ของจาวาสคริปต์ ที่เราเรียนรู้กันไปจากบทที่ผ่านๆมาแบบสั้นๆ แต่จะใส่ใจรายละเอียดเล็กๆน้อยๆเป็นพิเศษ

## โค้ดสร้างภาษา

คำสั่ง (Statements) แต่ละคำสั่งคั่นด้วย semicolon (;) เสมอ

```js run no-beautify
alert('Hello'); alert('World');
```

และการเว้นละบรรทัดก็ถือว่าเป็นการคั่นคำสั่งอย่างหนึ่ง เราสามารถใช้ได้เช่นกัน

```js run no-beautify
alert('Hello')
alert('World')
```

โดยจาวาสคริปต์จะทำการใส่ semicolon (;) ให้เองโดยอัตโนมัติ แต่บางครั้งเราก็ไม่สามารถเว้นบรรทัดแบบนี้ได้ เช่น

```js run
alert("There will be an error after this message")

[1, 2].forEach(alert)
```

ดังนั้นคู่มือจาวาสคริปต์ส่วนใหญ่จึงแนะนำให้ใส่ semicolon (;) คั่นคำสั่งทุกครั้ง

เราไม่จำเป็นต้องใส่ semicolon (;) ข้างหลัง code block `{...}` หรือรูปประโยคแบบ `for...loop`:

```js
function f() {
  // ไม่จำเป็นต้องใส่ semicolon (;) หลังจากการประกาศฟังก์ชัน
}

for(;;) {
  // ไม่จำเป็นต้องใส่ semicolon (;) หลังลูบ
}
```

...แต่ถ้าเราเผลอไปใส่ ก็จะไม่มีข้อผิดพลาด และsemicolon (;) จะถูกละเลยไป จาวาสคริปต์ก็ยังทำงานของมันได้ 

อ่านเพิ่มเติมได้ในบท: <info:structure>.

## Strict mode

เพื่อเปิดใช้งานฟีเจอร์ทั้งหมดของจาวาสคริปจ์สมัยใหม่อย่างสมบูรณ์ เราควรเริ่มสคริปต์ด้วย `"use strict"`

```js
'use strict';

...
```

คำสั่งต้องอยู่ที่ด้านบนสุดของสคริปต์หรือด้านบนสุดของฟังก์ชัน

หากไม่ใส่ `"use strict"` โปรแกรมก็ยังคงทำงานได้ แต่เราจะใช้ได้แต่ฟีเจอร์เก่าๆ

ฟีเจอร์ใหม่ๆ (อย่างเช่น class เราจะเขียนไปในบทถัดไป) จะเปิดใช้งานเฉพาะ Strict mode เท่สนั้น

ดูเพิ่มเติมได้ที่: <info:strict-mode>.

## ตัวแปร (Variables)

สามารถประกาศได้โดยใช้:

- `let`
- `const` (constant, can't be changed)
- `var` (old-style, will see later)

ชื่อตัวแปรสามารถมี:
- ตัวอักษรและตัวเลข แต่ตัวอักษรตัวแรกต้องไม่เป็นตัวเลข
- สามารถใช้อักขระพิเศษอย่าง `$` และ `_` ได้เทียบเท่ากับตัวอักษร.
- อนุญาตให้ใช้ตัวอักษรที่ไม่ใช่ละตินรวมถึงอักษรอียิปต์โบราณ แต่ไม่เป็นที่นิยม

ตัวแปรสามารถเก็บข้อมูลอะไรก็ได้ หรือ ข้อมูลชนิดใดๆก็ได้

```js
let x = 5;
x = "John";
```

มีข้อมูลทั้งหมด 8 ชนิด:

- `number` สำหรับทั้งเลขทศนิยมและจำนวนเต็ม
- `bigint` สำหรับจำนวนเต็มหรือตัวเลขที่มีค่าเกิน `2^53 - 1`
- `string` สำหรับสตริง
- `boolean` สำหรับค่าทางตรรกะ: `true/false`,
- `null` -- ชนิดที่มีค่าเดียวคือ `null` หมายถึง "ค่าว่าง" หรือ "ค่านั้นไม่มีอยู่"
- `undefined` -- ชนิดที่มีค่าเดียวคือ `undefined` หมายถึง "ยังไม่ถูกกำหนดค่า",
- `object` และ `symbol` -- สำหรับโครงสร้างข้อมูลที่ซับซ้อนและ unique identifiers ซึ่งเราจะได้เรียนกันในบทถัดๆไป

ตัวดำเนินการ `typeof` ส่งคืนประเภทของค่า โดยมีข้อยกเว้นสองประการ:
```js
typeof null == "object" // ได้ true เป็นบัคของภาษา
typeof function(){} == "function" // ได้ function
```

อ่านเพิ่มเติมได้ในบท: <info:variables> และ <info:types>

## ปฏิสัมพันธ์ (Interaction)

การปฎิสัมพันธ์เกิดขึ้นบนเบราเซอร์ มีฟังก์ชันพื้นฐานดังนี้:

[`prompt(question, [default])`](mdn:api/Window/prompt)
: ถามคำถาม `question` และส่งคืนสิ่งที่ผู้ใช้ป้อนหรือส่ง `null` หากผู้ใช้กด "cancel"

[`confirm(question)`](mdn:api/Window/confirm)
: ถามคำถาม `question` ให้ผู้ใช้เลือกระหว่าง Ok หรือ Cancel หากกด Ok จะส่ง `true` กลับ หากกด Cancel จะส่ง `false`

[`alert(message)`](mdn:api/Window/alert)
: แสดง `message`

ฟังก์ชั่นเหล่านี้จะเปิด *modal* ซึ่งจะหยุดการทำงานโค้ดและไม่ให้ผู้ใช้ตอบโต้กับหน้าเว็บชั่วคราว จนกว่าผู้ใช้จะตอบคำถามผ่าน *modal*

ตัวอย่างเช่น:

```js run
let userName = prompt("Your name?", "Alice");
let isTeaWanted = confirm("Do you want some tea?");

alert( "Visitor: " + userName ); // Alice
alert( "Tea wanted: " + isTeaWanted ); // true
```

อ่านเพิ่มเติมในบท: <info:alert-prompt-confirm>.

## ตัวดำเนินการ (Operators)

จาวาสคริปต์มีตัวดำเนินการดังนี้:

ตัวดำเนินการทางคณิตศาสคร์
: ได้แก่ `* + - /` รวมถึง `%` สำหรับหาเศษเหลือจากการหาร `**` สำหรับการยกกำลัง

    การใช้ `+` รวมสตริงสองตัวไว้ด้วยกัน และหากตัวถูกดำเนินการหนึ่งตัวเป็นสตริง ไม่ว่าจะอีกตัวจะเป็นข้อมูลชนิดใดจะถูกแปลงให้เป็นสตริงด้วย

    ```js run
    alert( '1' + 2 ); // '12' เป็นสตริง
    alert( 1 + '2' ); // '12' เป็นสตริง
    ```

การกำหนดค่า
: รูปประโยคการกำหนดค่ามีหน้าตาแบบนี้ `a = b` หรือจะใช้คู่กับตัวดำเนินการทางคณิตศาสคร์ก็ได้อย่าง `a *= 2`

การแปลงเป็นไบนารี
: ตัวดำเนินการแปลงเป็นไบนารีทำงานกับจำนวนเต็ม 32 บิตที่ระดับบิตต่ำสุด: โปรดดู [เอกสาร](mdn:/JavaScript/Guide/Expressions_and_Operators#Bitwise) เมื่อต้องใช้การแปลงเป็นไบนารี

เงื่อนไข
: ตัวดำเนินการเดียวที่ใช้สามพารามิเตอร์: `cond ? resultA : resultB` หาก `cond` เป็นจริงจะส่ง `resultA` กลับ หากไม่จะส่ง `resultB` กลับ

ตัวดำเนินการทางตรรกะ
: ตัว AND `&&` และ OR `||` จะใช้การประเมินผลแบบสั้น (Short-circuit evaluation) ส่งค่ากลับทันทีที่ค่าเป็นไปตามเกณฑ์ (ไม่จำเป็นว่าต้องเป็น `true`/`false`) ตัว NOT `!` จะแปลงค่าที่ถูกดำเนินการเป็นบูลีน จากนั่นจะส่งค่าที่กลับข้ามกลับไป

ตัวดำเนินการรวมเป็นโมฆะ (Nullish coalescing operator)
: ตัวดำเนินการ `??` จัดเตรียมวิธีการเลือกค่าที่กำหนดจากรายการตัวแปร ผลลัพธ์ของ `a ?? b` คือ `a` เว้นแต่จะเป็น `null/undefined` ตามด้วย `b`

การเปรียบเทียบ
: การเปรียบเทียบจะใช้ `==` สำหรับค่าที่แตกต่างกัน จะแปลงค่าท้ังสองเป็นตัวเลข (ยกเว้น `null` และ `undefined` ที่ทั้งค่านี้จะเท่ากัน แต่จะไม่เท่ากับค่าชนิดอื่นๆ)

    ```js run
    alert( 0 == false ); // true
    alert( 0 == '' ); // true
    ```

    การเปรียบเทียบจะแปลงค่าจะแปลงค่าท้ังสองเป็นตัวเลข

    ตัวดำเนินการเปรียบเทียบอีกตัวอย่าง `===` จะไม่แปลงค่าทั้งสองเป็นตัวเลข: หากค่าทั้งสองมีชนิดแตกต่างกัน จะถือว่าไม่เท่ากันในทันที

    ค่า `null` และ `undefined` เป็นค่าพิเศษ: ซึ่งหากเราเปรียบเทียบด้วย `==` ทั้งสองจะเท่ากัน แต่จะไม่เท่ากับค่าชนิดอื่นๆ

    การเปรียบเทียบมากน้อย เมื่อนำไปใช้กับสตริง มันจะค่อยๆจับเท่ากันไปทีละตัวอักษร ส่วนค่าชนิดอื่นๆที่ไม่ใช่สตริงจะถูกแปลงเป็นตัวเลข

ตัวดำเนินการอื่นๆ
: มีอีกสองสามอย่าง เช่น ตัวดำเนินการจุลภาค

สามารถดูเพิ่มเติมได้ใน: <info:operators>, <info:comparison>, <info:logical-operators>, <info:nullish-coalescing-operator>.

## ลูป

- เราได้พูดถึงลูป 3 ประเภท:

    ```js
    // 1
    while (condition) {
      ...
    }

    // 2
    do {
      ...
    } while (condition);

    // 3
    for(let i = 0; i < 10; i++) {
      ...
    }
    ```

- The variable declared in `for(let...)` loop is visible only inside the loop. But we can also omit `let` and reuse an existing variable.
- Directives `break/continue` allow to exit the whole loop/current iteration. Use labels to break nested loops.

Details in: <info:while-for>.

Later we'll study more types of loops to deal with objects.

## The "switch" construct

The "switch" construct can replace multiple `if` checks. It uses `===` (strict equality) for comparisons.

For instance:

```js run
let age = prompt('Your age?', 18);

switch (age) {
  case 18:
    alert("Won't work"); // the result of prompt is a string, not a number
    break;

  case "18":
    alert("This works!");
    break;

  default:
    alert("Any value not equal to one above");
}
```

Details in: <info:switch>.

## Functions

We covered three ways to create a function in JavaScript:

1. Function Declaration: the function in the main code flow

    ```js
    function sum(a, b) {
      let result = a + b;

      return result;
    }
    ```

2. Function Expression: the function in the context of an expression

    ```js
    let sum = function(a, b) {
      let result = a + b;

      return result;
    };
    ```

3. Arrow functions:

    ```js
    // expression at the right side
    let sum = (a, b) => a + b;

    // or multi-line syntax with { ... }, need return here:
    let sum = (a, b) => {
      // ...
      return a + b;
    }

    // without arguments
    let sayHi = () => alert("Hello");

    // with a single argument
    let double = n => n * 2;
    ```


- Functions may have local variables: those declared inside its body or its parameter list. Such variables are only visible inside the function.
- Parameters can have default values: `function sum(a = 1, b = 2) {...}`.
- Functions always return something. If there's no `return` statement, then the result is `undefined`.

Details: see <info:function-basics>, <info:arrow-functions-basics>.

## More to come

That was a brief list of JavaScript features. As of now we've studied only basics. Further in the tutorial you'll find more specials and advanced features of JavaScript.
