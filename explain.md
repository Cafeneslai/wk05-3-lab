# JavaScript Code Explanation

เอกสารนี้อธิบายการทำงานของโค้ด JavaScript ในแต่ละส่วนที่ระบุ พร้อมแสดงผลลัพธ์ที่ได้

## 📁 ไฟล์ทั้งหมด

| ไฟล์ | ลิงก์ |
|------|-------|
| 01-variables.js | [คลิกดูไฟล์](./01-variables.js) |
| 02-functions.js | [คลิกดูไฟล์](./02-functions.js) |
| 03-control-flow.js | [คลิกดูไฟล์](./03-control-flow.js) |
| 04-loops.js | [คลิกดูไฟล์](./04-loops.js) |
| 05-integration.js | [คลิกดูไฟล์](./05-integration.js) |

---

## 2.1 ไฟล์ [01-variables.js](./01-variables.js) - 6. Challenge: Create a Person Object

### โค้ด

```javascript
const student = {
  firstName: "Alice",
  lastName: "Smith",
  age: 20,
  gpa: 3.8,
  courses: ["HTML", "CSS", "JavaScript"],
  isActive: true,
  // Method (function in object)
  getFullName: function () {
    return `${this.firstName} ${this.lastName}`;
  },
  getInfo: function () {
    return `${this.getFullName()}, Age: ${this.age}, GPA: ${this.gpa}`;
  },
};
console.log("Student object:");
console.log(student);
console.log("Full name:", student.getFullName());
console.log("Info:", student.getInfo());
console.log("Courses:", student.courses.join(", "));
```

### ผลลัพธ์

```
Student object:
{
  firstName: 'Alice',
  lastName: 'Smith',
  age: 20,
  gpa: 3.8,
  courses: [ 'HTML', 'CSS', 'JavaScript' ],
  isActive: true,
  getFullName: [Function: getFullName],
  getInfo: [Function: getInfo]
}
Full name: Alice Smith
Info: Alice Smith, Age: 20, GPA: 3.8
Courses: HTML, CSS, JavaScript
```

### อธิบายการทำงาน

1. **สร้าง Object `student`**: สร้าง Object ที่มี Properties หลายชนิด
   - `firstName`, `lastName` เป็น String
   - `age`, `gpa` เป็น Number
   - `courses` เป็น Array ของ String
   - `isActive` เป็น Boolean

2. **Method `getFullName()`**: เป็นฟังก์ชันภายใน Object ที่ใช้ `this` เพื่ออ้างถึง Object ตัวเอง และคืนค่าชื่อเต็มโดยใช้ Template Literal `${this.firstName} ${this.lastName}`

3. **Method `getInfo()`**: เรียก `this.getFullName()` เพื่อนำชื่อเต็มมาใช้ และรวมกับข้อมูลอื่นๆ

4. **`courses.join(", ")`**: แปลง Array เป็น String โดยคั่นด้วย ", "

---

## 2.2 ไฟล์ [02-functions.js](./02-functions.js) - 8. Returning Objects

### โค้ด

```javascript
function createUser(firstName, lastName, age) {
  return {
    firstName, // shorthand for firstName: firstName
    lastName,
    age,
    email: `${firstName.toLowerCase()}.${lastName.toLowerCase()}@example.com`,
    getFullName() {
      // shorthand for getFullName: function() {}
      return `${this.firstName} ${this.lastName}`;
    },
    getAge() {
      return this.age;
    },
  };
}
console.log("\nReturning Objects:");
const newUser = createUser("John", "Doe", 30);
console.log(newUser);
console.log("Email:", newUser.email);
console.log("Full name:", newUser.getFullName());
```

### ผลลัพธ์

```
Returning Objects:
{
  firstName: 'John',
  lastName: 'Doe',
  age: 30,
  email: 'john.doe@example.com',
  getFullName: [Function: getFullName],
  getAge: [Function: getAge]
}
Email: john.doe@example.com
Full name: John Doe
```

### อธิบายการทำงาน

1. **Property Shorthand**: `firstName` คือการเขียนย่อของ `firstName: firstName` เมื่อชื่อ Property และ Variable เหมือนกัน

2. **Computed Property**: `email` ถูกคำนวณจาก `firstName` และ `lastName` โดยแปลงเป็นตัวพิมพ์เล็กด้วย `.toLowerCase()`

3. **Method Shorthand**: `getFullName()` คือการเขียนย่อของ `getFullName: function() {}`

4. **Return Object**: ฟังก์ชัน `createUser` คืนค่าเป็น Object ที่สร้างขึ้นใหม่พร้อม Properties และ Methods

---

## 2.2 ไฟล์ [02-functions.js](./02-functions.js) - 9. Function as Parameter (Callback)

### โค้ด

```javascript
function processArray(arr, callback) {
  const result = [];
  for (const item of arr) {
    result.push(callback(item));
  }
  return result;
}
const numbers = [1, 2, 3, 4, 5];
const doubled = processArray(numbers, (x) => x * 2);
const squared = processArray(numbers, (x) => x * x);
console.log("\nCallback Function:");
console.log("Original:", numbers);
console.log("Doubled:", doubled);
console.log("Squared:", squared);
```

### ผลลัพธ์

```
Callback Function:
Original: [ 1, 2, 3, 4, 5 ]
Doubled: [ 2, 4, 6, 8, 10 ]
Squared: [ 1, 4, 9, 16, 25 ]
```

### อธิบายการทำงาน

1. **Callback Function**: ฟังก์ชัน `processArray` รับ Array และ Callback Function เป็น Parameter

2. **การทำงาน**:
   - วนลูปแต่ละ item ใน Array
   - เรียก `callback(item)` กับแต่ละ item
   - เก็บผลลัพธ์ลงใน Array ใหม่

3. **Arrow Function เป็น Callback**:
   - `(x) => x * 2` คูณ 2: `[1,2,3,4,5]` → `[2,4,6,8,10]`
   - `(x) => x * x` ยกกำลังสอง: `[1,2,3,4,5]` → `[1,4,9,16,25]`

---

## 2.3 ไฟล์ [03-control-flow.js](./03-control-flow.js) - 5. Short-Circuit Evaluation

### โค้ด

```javascript
console.log("\nShort-Circuit Evaluation:");
const user = { name: "John", age: 25 };
const admin = null;
// OR: use default value
const userName = admin?.name || user.name || "Anonymous";
console.log("User name:", userName);
// AND: check before accessing
const userProfile = user && user.profile;
console.log("User profile:", userProfile);
```

### ผลลัพธ์

```
Short-Circuit Evaluation:
User name: John
User profile: undefined
```

### อธิบายการทำงาน

1. **Optional Chaining (`?.`)**: `admin?.name` ตรวจสอบว่า `admin` เป็น null/undefined หรือไม่
   - ถ้า `admin` เป็น null → คืน `undefined` (ไม่เกิด error)

2. **OR Short-Circuit (`||`)**:
   - `admin?.name` = `undefined` (falsy) → ข้ามไป
   - `user.name` = `"John"` (truthy) → ใช้ค่านี้
   - ผลลัพธ์: `"John"`

3. **AND Short-Circuit (`&&`)**:
   - `user` = Object (truthy) → ดำเนินการต่อ
   - `user.profile` = `undefined` (ไม่มี property นี้)
   - ผลลัพธ์: `undefined`

4. **หลักการ**:
   - `||` คืนค่าแรกที่เป็น truthy หรือค่าสุดท้าย
   - `&&` คืนค่าแรกที่เป็น falsy หรือค่าสุดท้าย

---

## 2.3 ไฟล์ [03-control-flow.js](./03-control-flow.js) - 7. Form Validation

### โค้ด

```javascript
function validateRegistration(formData) {
  const errors = [];
  // Validate name
  if (!formData.name || formData.name.trim() === "") {
    errors.push("Name is required");
  } else if (formData.name.length < 3) {
    errors.push("Name must be at least 3 characters");
  }
  // Validate email
  if (!formData.email || formData.email.indexOf("@") === -1) {
    errors.push("Valid email is required");
  }
  // Validate age
  if (!formData.age || formData.age < 18) {
    errors.push("Must be 18 or older");
  }
  // Validate password
  if (!formData.password || formData.password.length < 6) {
    errors.push("Password must be at least 6 characters");
  }
  // Check if agree to terms
  if (!formData.agreeToTerms) {
    errors.push("Must agree to terms");
  }
  return {
    isValid: errors.length === 0,
    errors: errors,
  };
}

const validUser = {
  name: "John Doe",
  email: "john@example.com",
  age: 25,
  password: "securepass123",
  agreeToTerms: true,
};
const invalidUser = {
  name: "Jo",
  email: "invalidemail",
  age: 15,
  password: "pass",
  agreeToTerms: false,
};
console.log("Valid user:", validateRegistration(validUser));
console.log("Invalid user:", validateRegistration(invalidUser));
```

### ผลลัพธ์

```
Form Validation:
Valid user: { isValid: true, errors: [] }
Invalid user: {
  isValid: false,
  errors: [
    'Name must be at least 3 characters',
    'Valid email is required',
    'Must be 18 or older',
    'Password must be at least 6 characters',
    'Must agree to terms'
  ]
}
```

### อธิบายการทำงาน

1. **สร้าง Array เก็บ errors**: เริ่มต้นด้วย Array ว่าง

2. **ตรวจสอบแต่ละ Field**:
   - **name**: ต้องมีและยาวอย่างน้อย 3 ตัวอักษร
   - **email**: ต้องมีและมีเครื่องหมาย `@`
   - **age**: ต้องมีและมากกว่าหรือเท่ากับ 18
   - **password**: ต้องมีและยาวอย่างน้อย 6 ตัวอักษร
   - **agreeToTerms**: ต้องเป็น `true`

3. **คืนค่า Object**:
   - `isValid`: `true` ถ้าไม่มี errors
   - `errors`: Array ของข้อผิดพลาดทั้งหมด

4. **ผลลัพธ์**:
   - `validUser` ผ่านทุกเงื่อนไข → `isValid: true`
   - `invalidUser` ไม่ผ่าน 5 เงื่อนไข → `isValid: false` พร้อม errors

---

## 2.4 ไฟล์ [04-loops.js](./04-loops.js) - 9. Chaining methods

### โค้ด

```javascript
console.log("\nMethod chaining:");
const data = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
// Filter even > map to string > join
const evenStrings = data
  .filter((n) => n % 2 === 0) // [2, 4, 6, 8, 10]
  .map((n) => `${n}²=${n * n}`) // ["2²=4", "4²=16", ...]
  .join(", "); // "2²=4, 4²=16, ..."
console.log("Even numbers squared:", evenStrings);

// Calculate average with reduce and length
const numbers2 = [10, 20, 30, 40, 50];
const average = numbers2.reduce((sum, n) => sum + n, 0) / numbers2.length;
console.log("Average:", average);
```

### ผลลัพธ์

```
Method chaining:
Even numbers squared: 2²=4, 4²=16, 6²=36, 8²=64, 10²=100
Average: 30
```

### อธิบายการทำงาน

1. **Method Chaining**: เรียกใช้หลาย Method ต่อกันในบรรทัดเดียว

2. **ขั้นตอนการทำงาน**:
   ```
   [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
           ↓ filter(n => n % 2 === 0)
   [2, 4, 6, 8, 10]
           ↓ map(n => `${n}²=${n * n}`)
   ["2²=4", "4²=16", "6²=36", "8²=64", "10²=100"]
           ↓ join(", ")
   "2²=4, 4²=16, 6²=36, 8²=64, 10²=100"
   ```

3. **คำนวณค่าเฉลี่ย**:
   - `reduce((sum, n) => sum + n, 0)` = 10+20+30+40+50 = 150
   - หารด้วย `length` = 5
   - ผลลัพธ์: 150 / 5 = 30

---

## 2.4 ไฟล์ [04-loops.js](./04-loops.js) - 10. Challenge: Student Grades

### โค้ด

```javascript
const students = [
  { name: "Alice", score: 95 },
  { name: "Bob", score: 75 },
  { name: "Charlie", score: 85 },
  { name: "Diana", score: 92 },
  { name: "Eve", score: 88 },
];
console.log("\nChallenge: Student Analysis");
console.log("Students:", students);

// 1. Get all names
const names = students.map((s) => s.name);
console.log("Names:", names.join(", "));

// 2. Filter high scorers (>= 85)
const highScorers = students.filter((s) => s.score >= 85);
console.log(
  "High scorers:",
  highScorers.map((s) => `${s.name} (${s.score})`).join(", ")
);

// 3. Calculate class average
const classAverage =
  students.reduce((sum, s) => sum + s.score, 0) / students.length;
console.log("Class average:", classAverage.toFixed(2));

// 4. Find top scorer
const topScorer = students.reduce((top, s) => (s.score > top.score ? s : top));
console.log("Top scorer:", `${topScorer.name} (${topScorer.score})`);

// 5. Create summary
const summary = students
  .map((s) => ({
    ...s,
    grade: s.score >= 90 ? "A" : s.score >= 80 ? "B" : "C",
  }))
  .sort((a, b) => b.score - a.score);
console.log("Summary (sorted):");
summary.forEach((s) => console.log(` ${s.name}: ${s.score} (${s.grade})`));
```

### ผลลัพธ์

```
Challenge: Student Analysis
Students: [
  { name: 'Alice', score: 95 },
  { name: 'Bob', score: 75 },
  { name: 'Charlie', score: 85 },
  { name: 'Diana', score: 92 },
  { name: 'Eve', score: 88 }
]
Names: Alice, Bob, Charlie, Diana, Eve
High scorers: Alice (95), Charlie (85), Diana (92), Eve (88)
Class average: 87.00
Top scorer: Alice (95)
Summary (sorted):
 Alice: 95 (A)
 Diana: 92 (A)
 Eve: 88 (B)
 Charlie: 85 (B)
 Bob: 75 (C)
```

### อธิบายการทำงาน

1. **`map()` ดึงชื่อ**: แปลง Array of Objects เป็น Array of Names

2. **`filter()` กรอง High Scorers**: เลือกเฉพาะคนที่คะแนน >= 85

3. **`reduce()` หาค่าเฉลี่ย**: รวมคะแนนทั้งหมด (95+75+85+92+88=435) หาร 5 = 87

4. **`reduce()` หาคะแนนสูงสุด**: เปรียบเทียบคะแนนแต่ละคน เก็บคนที่คะแนนสูงกว่า

5. **สร้าง Summary**:
   - `map()` เพิ่ม property `grade` ด้วย Spread Operator (`...s`)
   - `sort()` เรียงจากคะแนนสูงไปต่ำ (`b.score - a.score`)

---

## 2.5 ไฟล์ [05-integration.js](./05-integration.js) - Activity 5: Integration - Quiz Application

### โค้ด

```javascript
console.log("🎯 === QUIZ APPLICATION === 🎯\n");

// Quiz data
const quizzes = [
  {
    question: "What is 5 + 3?",
    options: ["8", "7", "6", "9"],
    correctAnswer: 0,
  },
  {
    question: "What is the capital of Thailand?",
    options: ["Phuket", "Bangkok", "Chiang Mai", "Pattaya"],
    correctAnswer: 1,
  },
  {
    question: "What is the largest planet?",
    options: ["Mars", "Saturn", "Jupiter", "Neptune"],
    correctAnswer: 2,
  },
  {
    question: "What is 2^8?",
    options: ["128", "256", "64", "512"],
    correctAnswer: 1,
  },
  {
    question: "Which is NOT a JavaScript data type?",
    options: ["string", "class", "symbol", "boolean"],
    correctAnswer: 1,
  },
];

let results = [];

// Process each quiz
quizzes.forEach((quiz, index) => {
  const userAnswer = Math.floor(Math.random() * 4); // จำลองการทำ quiz
  const isCorrect = userAnswer === quiz.correctAnswer;
  results.push({
    questionNum: index + 1,
    question: quiz.question,
    userAnswer: quiz.options[userAnswer],
    correctAnswer: quiz.options[quiz.correctAnswer],
    isCorrect: isCorrect,
  });
});

// Display results
console.log("QUIZ RESULTS:");
console.log("─".repeat(60));
results.forEach((result) => {
  const status = result.isCorrect ? "✅ CORRECT" : "❌ WRONG";
  console.log(`Q${result.questionNum}: ${result.question}`);
  console.log(` Your answer: ${result.userAnswer}`);
  if (!result.isCorrect) {
    console.log(` Correct answer: ${result.correctAnswer}`);
  }
  console.log(` ${status}`);
  console.log();
});

// Calculate score
const correctCount = results.filter((r) => r.isCorrect).length;
const score = (correctCount / results.length) * 100;

console.log("─".repeat(60));
console.log(`FINAL SCORE: ${correctCount}/${results.length} (${score.toFixed(1)}%)`);

// Grade assignment
let grade;
if (score >= 90) grade = "A";
else if (score >= 80) grade = "B";
else if (score >= 70) grade = "C";
else if (score >= 60) grade = "D";
else grade = "F";

console.log(`GRADE: ${grade}`);
```

### ผลลัพธ์ (ตัวอย่าง - ผลลัพธ์จะแตกต่างกันในแต่ละครั้งเนื่องจากใช้ Random)

```
🎯 === QUIZ APPLICATION === 🎯

QUIZ RESULTS:
────────────────────────────────────────────────────────────
Q1: What is 5 + 3?
 Your answer: 8
 ✅ CORRECT

Q2: What is the capital of Thailand?
 Your answer: Phuket
 Correct answer: Bangkok
 ❌ WRONG

Q3: What is the largest planet?
 Your answer: Jupiter
 ✅ CORRECT

Q4: What is 2^8?
 Your answer: 64
 Correct answer: 256
 ❌ WRONG

Q5: Which is NOT a JavaScript data type?
 Your answer: class
 ✅ CORRECT

────────────────────────────────────────────────────────────
FINAL SCORE: 3/5 (60.0%)
GRADE: D

FEEDBACK:
📚 Good effort. Review the material and try again.

📊 STATISTICS:
Total questions: 5
Correct: 3
Incorrect: 2
Success rate: 60.0%

Answer breakdown:
 ✅ Correct: 3
 ❌ Incorrect: 2
```

### อธิบายการทำงาน

1. **โครงสร้างข้อมูล Quiz**:
   - แต่ละ Quiz เป็น Object ที่มี `question`, `options` (Array), และ `correctAnswer` (index)

2. **จำลองการตอบ**: ใช้ `Math.floor(Math.random() * 4)` สุ่มคำตอบ 0-3

3. **เก็บผลลัพธ์**: สร้าง Object สำหรับแต่ละคำถาม และ push ลง Array `results`

4. **แสดงผลลัพธ์**: วนลูป `results` แสดงคำถาม, คำตอบผู้ใช้, และสถานะถูก/ผิด

5. **คำนวณคะแนน**:
   - `filter((r) => r.isCorrect)` หาจำนวนข้อที่ตอบถูก
   - คำนวณเปอร์เซ็นต์ = (ถูก / ทั้งหมด) × 100

6. **กำหนดเกรด**: ใช้ if-else ตรวจสอบช่วงคะแนน

7. **สถิติ**: ใช้ `reduce()` นับจำนวนถูก/ผิด โดยสร้าง Object `{ correct: 0, incorrect: 0 }`
