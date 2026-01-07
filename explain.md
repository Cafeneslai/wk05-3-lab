# 📚 อธิบายการทำงานของโค้ด JavaScript

เอกสารนี้อธิบายการทำงานของโค้ดในแต่ละไฟล์ พร้อมแสดงผลลัพธ์ที่ได้

---

## 2.1 ไฟล์ `01-variables.js` - Challenge: Create a Person Object

### 📝 โค้ด

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

### 📤 ผลลัพธ์

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

### 💡 อธิบายการทำงาน

1. **สร้าง Object `student`** - เก็บข้อมูลนักศึกษาที่ประกอบด้วย:
   - `firstName`, `lastName` - ชื่อและนามสกุล (String)
   - `age` - อายุ (Number)
   - `gpa` - เกรดเฉลี่ย (Number)
   - `courses` - วิชาที่เรียน (Array)
   - `isActive` - สถานะการเรียน (Boolean)

2. **Method `getFullName()`** - ฟังก์ชันภายใน Object ที่ใช้ `this` เพื่อเข้าถึง properties ของ Object ตัวเอง
   - `this.firstName` คืนค่า "Alice"
   - `this.lastName` คืนค่า "Smith"
   - ใช้ Template Literal `` `${...}` `` รวมเป็น "Alice Smith"

3. **Method `getInfo()`** - เรียกใช้ `this.getFullName()` เพื่อดึงชื่อเต็ม แล้วรวมกับข้อมูลอื่น

4. **`courses.join(", ")`** - แปลง Array เป็น String โดยคั่นด้วย ", "

---

## 2.2 ไฟล์ `02-functions.js`

### 8. Returning Objects

#### 📝 โค้ด

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
const newUser = createUser("John", "Doe", 30);
console.log(newUser);
console.log("Email:", newUser.email);
console.log("Full name:", newUser.getFullName());
```

#### 📤 ผลลัพธ์

```
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

#### 💡 อธิบายการทำงาน

1. **ฟังก์ชัน `createUser`** รับ 3 parameters: `firstName`, `lastName`, `age`

2. **Property Shorthand** - เมื่อชื่อ property ตรงกับชื่อ variable สามารถเขียนย่อได้:
   ```javascript
   // แทนที่จะเขียน
   { firstName: firstName, lastName: lastName }
   // เขียนสั้นๆ ได้เป็น
   { firstName, lastName }
   ```

3. **สร้าง Email อัตโนมัติ** - ใช้ `toLowerCase()` แปลงเป็นตัวพิมพ์เล็ก แล้วรวมเป็นรูปแบบ email

4. **Method Shorthand** - แทนที่จะเขียน `getFullName: function() {}` สามารถเขียนย่อเป็น `getFullName() {}`

5. **ผลลัพธ์** - ฟังก์ชันคืนค่า Object ใหม่ที่มีข้อมูลและ methods พร้อมใช้งาน

---

### 9. Function as Parameter (Callback)

#### 📝 โค้ด

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
console.log("Original:", numbers);
console.log("Doubled:", doubled);
console.log("Squared:", squared);
```

#### 📤 ผลลัพธ์

```
Original: [ 1, 2, 3, 4, 5 ]
Doubled: [ 2, 4, 6, 8, 10 ]
Squared: [ 1, 4, 9, 16, 25 ]
```

#### 💡 อธิบายการทำงาน

1. **Callback Function** คือ ฟังก์ชันที่ส่งเป็น parameter ให้กับฟังก์ชันอื่น

2. **ฟังก์ชัน `processArray`** รับ 2 parameters:
   - `arr` - Array ที่ต้องการประมวลผล
   - `callback` - ฟังก์ชันที่จะทำกับแต่ละ element

3. **การทำงานทีละขั้น (Doubled)**:
   | รอบที่ | item | callback(item) = x * 2 | result |
   |--------|------|------------------------|--------|
   | 1 | 1 | 1 * 2 = 2 | [2] |
   | 2 | 2 | 2 * 2 = 4 | [2, 4] |
   | 3 | 3 | 3 * 2 = 6 | [2, 4, 6] |
   | 4 | 4 | 4 * 2 = 8 | [2, 4, 6, 8] |
   | 5 | 5 | 5 * 2 = 10 | [2, 4, 6, 8, 10] |

4. **ความยืดหยุ่น** - ใช้ฟังก์ชันเดียวกัน แค่เปลี่ยน callback ก็ได้ผลลัพธ์ต่างกัน

---

## 2.3 ไฟล์ `03-control-flow.js`

### 5. Short-Circuit Evaluation

#### 📝 โค้ด

```javascript
const user = { name: "John", age: 25 };
const admin = null;

// OR: use default value
const userName = admin?.name || user.name || "Anonymous";
console.log("User name:", userName);

// AND: check before accessing
const userProfile = user && user.profile;
console.log("User profile:", userProfile);
```

#### 📤 ผลลัพธ์

```
User name: John
User profile: undefined
```

#### 💡 อธิบายการทำงาน

**Short-Circuit Evaluation** คือ JavaScript หยุดประเมินค่าเมื่อรู้ผลลัพธ์แล้ว

1. **Optional Chaining (`?.`)** - เข้าถึง property อย่างปลอดภัย:
   - `admin?.name` → admin เป็น `null` → คืนค่า `undefined` (ไม่ error)

2. **OR (`||`) Operator** - คืนค่าแรกที่เป็น truthy:
   ```
   admin?.name  →  undefined (falsy) → ข้ามไป
   user.name    →  "John" (truthy)   → ใช้ค่านี้!
   "Anonymous"  →  ไม่ถูกประเมิน
   ```
   **ผลลัพธ์**: `"John"`

3. **AND (`&&`) Operator** - คืนค่าแรกที่เป็น falsy หรือค่าสุดท้าย:
   ```
   user         →  { name: "John", age: 25 } (truthy) → ไปต่อ
   user.profile →  undefined (falsy)                   → คืนค่านี้
   ```
   **ผลลัพธ์**: `undefined`

---

### 7. Form Validation

#### 📝 โค้ด

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

#### 📤 ผลลัพธ์

```
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

#### 💡 อธิบายการทำงาน

1. **สร้าง Array `errors`** เพื่อเก็บข้อผิดพลาดที่พบ

2. **ตรวจสอบแต่ละ field**:

   | Field | Valid User | Invalid User | ผลการตรวจสอบ |
   |-------|------------|--------------|--------------|
   | name | "John Doe" (8 ตัว) ✅ | "Jo" (2 ตัว) ❌ | ต้องมีอย่างน้อย 3 ตัวอักษร |
   | email | "john@example.com" ✅ | "invalidemail" ❌ | ต้องมี @ |
   | age | 25 ✅ | 15 ❌ | ต้อง >= 18 |
   | password | "securepass123" (13 ตัว) ✅ | "pass" (4 ตัว) ❌ | ต้องมีอย่างน้อย 6 ตัวอักษร |
   | agreeToTerms | true ✅ | false ❌ | ต้องยอมรับเงื่อนไข |

3. **คืนค่า Object** ที่มี:
   - `isValid` - เป็น `true` เมื่อไม่มี errors
   - `errors` - Array ของข้อผิดพลาดทั้งหมด

---

## 2.4 ไฟล์ `04-loops.js`

### 9. Chaining Methods

#### 📝 โค้ด

```javascript
const data = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

const evenStrings = data
  .filter((n) => n % 2 === 0)    // [2, 4, 6, 8, 10]
  .map((n) => `${n}²=${n * n}`)  // ["2²=4", "4²=16", ...]
  .join(", ");                    // "2²=4, 4²=16, ..."

console.log("Even numbers squared:", evenStrings);

const numbers2 = [10, 20, 30, 40, 50];
const average = numbers2.reduce((sum, n) => sum + n, 0) / numbers2.length;
console.log("Average:", average);
```

#### 📤 ผลลัพธ์

```
Even numbers squared: 2²=4, 4²=16, 6²=36, 8²=64, 10²=100
Average: 30
```

#### 💡 อธิบายการทำงาน

**Method Chaining** คือการเรียก method ต่อเนื่องกัน เพราะแต่ละ method คืนค่าที่สามารถเรียก method ต่อได้

1. **ขั้นตอนที่ 1: `filter()`**
   ```
   [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
   ↓ กรองเฉพาะเลขคู่ (n % 2 === 0)
   [2, 4, 6, 8, 10]
   ```

2. **ขั้นตอนที่ 2: `map()`**
   ```
   [2, 4, 6, 8, 10]
   ↓ แปลงเป็น string แสดงกำลังสอง
   ["2²=4", "4²=16", "6²=36", "8²=64", "10²=100"]
   ```

3. **ขั้นตอนที่ 3: `join()`**
   ```
   ["2²=4", "4²=16", "6²=36", "8²=64", "10²=100"]
   ↓ รวมด้วย ", "
   "2²=4, 4²=16, 6²=36, 8²=64, 10²=100"
   ```

4. **การคำนวณ Average**:
   ```
   reduce: 10 + 20 + 30 + 40 + 50 = 150
   average: 150 / 5 = 30
   ```

---

### 10. Challenge: Student Grades

#### 📝 โค้ด

```javascript
const students = [
  { name: "Alice", score: 95 },
  { name: "Bob", score: 75 },
  { name: "Charlie", score: 85 },
  { name: "Diana", score: 92 },
  { name: "Eve", score: 88 },
];

// 1. Get all names
const names = students.map((s) => s.name);
console.log("Names:", names.join(", "));

// 2. Filter high scorers (>= 85)
const highScorers = students.filter((s) => s.score >= 85);
console.log("High scorers:", highScorers.map((s) => `${s.name} (${s.score})`).join(", "));

// 3. Calculate class average
const classAverage = students.reduce((sum, s) => sum + s.score, 0) / students.length;
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

#### 📤 ผลลัพธ์

```
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

#### 💡 อธิบายการทำงาน

1. **ดึงชื่อทั้งหมด (`map`)**:
   ```
   students.map((s) => s.name)
   → ["Alice", "Bob", "Charlie", "Diana", "Eve"]
   ```

2. **กรองคนที่ได้คะแนนสูง (`filter`)**:
   | นักเรียน | คะแนน | >= 85? |
   |----------|-------|--------|
   | Alice | 95 | ✅ |
   | Bob | 75 | ❌ |
   | Charlie | 85 | ✅ |
   | Diana | 92 | ✅ |
   | Eve | 88 | ✅ |

3. **คำนวณค่าเฉลี่ย (`reduce`)**:
   ```
   (95 + 75 + 85 + 92 + 88) / 5 = 435 / 5 = 87.00
   ```

4. **หาคนที่ได้คะแนนสูงสุด (`reduce`)**:
   | เปรียบเทียบ | top | s | ผลลัพธ์ |
   |-------------|-----|---|---------|
   | รอบ 1 | Alice(95) | Bob(75) | Alice(95) |
   | รอบ 2 | Alice(95) | Charlie(85) | Alice(95) |
   | รอบ 3 | Alice(95) | Diana(92) | Alice(95) |
   | รอบ 4 | Alice(95) | Eve(88) | Alice(95) |

5. **สร้างสรุปพร้อมเกรด**:
   - ใช้ **Spread Operator** (`...s`) เพื่อ copy properties เดิม
   - เพิ่ม property `grade` ด้วย **Ternary Operator**
   - เรียงลำดับด้วย `sort()` จากคะแนนสูงไปต่ำ

---

## 2.5 ไฟล์ `05-integration.js` - Quiz Application

### 📝 โค้ด

```javascript
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

// Quiz results
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
results.forEach((result) => {
  const status = result.isCorrect ? "✅ CORRECT" : "❌ WRONG";
  console.log(`Q${result.questionNum}: ${result.question}`);
  console.log(` Your answer: ${result.userAnswer}`);
  if (!result.isCorrect) {
    console.log(` Correct answer: ${result.correctAnswer}`);
  }
  console.log(` ${status}`);
});

// Calculate score
const correctCount = results.filter((r) => r.isCorrect).length;
const score = (correctCount / results.length) * 100;
console.log(`FINAL SCORE: ${correctCount}/${results.length} (${score.toFixed(1)}%)`);

// Grade assignment
let grade;
if (score >= 90) grade = "A";
else if (score >= 80) grade = "B";
else if (score >= 70) grade = "C";
else if (score >= 60) grade = "D";
else grade = "F";
console.log(`GRADE: ${grade}`);

// Statistics using reduce
const byCorrectness = results.reduce(
  (acc, r) => {
    acc[r.isCorrect ? "correct" : "incorrect"]++;
    return acc;
  },
  { correct: 0, incorrect: 0 }
);
console.log("Answer breakdown:");
console.log(` ✅ Correct: ${byCorrectness.correct}`);
console.log(` ❌ Incorrect: ${byCorrectness.incorrect}`);
```

### 📤 ผลลัพธ์ (ตัวอย่าง - ค่าจะแตกต่างกันในแต่ละครั้งเพราะใช้ random)

```
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

### 💡 อธิบายการทำงาน

#### 1. โครงสร้างข้อมูล Quiz

```javascript
{
  question: "What is 5 + 3?",
  options: ["8", "7", "6", "9"],  // index: 0, 1, 2, 3
  correctAnswer: 0                 // คำตอบที่ถูกคือ index 0 = "8"
}
```

#### 2. การประมวลผล Quiz (`forEach`)

```
สำหรับแต่ละข้อ:
1. สุ่มคำตอบ: Math.floor(Math.random() * 4) → 0, 1, 2, หรือ 3
2. ตรวจสอบ: userAnswer === quiz.correctAnswer
3. บันทึกผลลัพธ์ลง results array
```

#### 3. การคำนวณคะแนน

```javascript
// นับจำนวนข้อที่ตอบถูก
const correctCount = results.filter((r) => r.isCorrect).length;

// คำนวณเปอร์เซ็นต์
const score = (correctCount / results.length) * 100;
// ถ้าถูก 3 จาก 5: (3 / 5) * 100 = 60%
```

#### 4. การกำหนดเกรด (Control Flow)

| คะแนน | เกรด |
|-------|------|
| >= 90% | A |
| >= 80% | B |
| >= 70% | C |
| >= 60% | D |
| < 60% | F |

#### 5. สถิติด้วย Reduce

```javascript
results.reduce(
  (acc, r) => {
    acc[r.isCorrect ? "correct" : "incorrect"]++;
    return acc;
  },
  { correct: 0, incorrect: 0 }
);
```

**การทำงาน**:
| รอบ | isCorrect | acc (ก่อน) | acc (หลัง) |
|-----|-----------|------------|------------|
| 1 | true | {correct: 0, incorrect: 0} | {correct: 1, incorrect: 0} |
| 2 | false | {correct: 1, incorrect: 0} | {correct: 1, incorrect: 1} |
| 3 | true | {correct: 1, incorrect: 1} | {correct: 2, incorrect: 1} |
| ... | ... | ... | ... |

---

## 📌 สรุป Concepts ที่สำคัญ

| Concept | ใช้ใน | คำอธิบาย |
|---------|-------|----------|
| **Object Methods** | 2.1, 2.2 | ฟังก์ชันภายใน Object ที่ใช้ `this` เข้าถึง properties |
| **Property Shorthand** | 2.2 | เขียน `{ name }` แทน `{ name: name }` |
| **Callback Function** | 2.2 | ส่งฟังก์ชันเป็น parameter ให้ฟังก์ชันอื่น |
| **Short-Circuit** | 2.3 | `\|\|` และ `&&` หยุดประเมินเมื่อรู้ผลลัพธ์ |
| **Optional Chaining** | 2.3 | `?.` เข้าถึง property อย่างปลอดภัย |
| **Method Chaining** | 2.4 | เรียก method ต่อเนื่องกัน |
| **Array Methods** | 2.4, 2.5 | `map`, `filter`, `reduce`, `forEach` |
| **Spread Operator** | 2.4 | `...obj` copy properties ทั้งหมด |
| **Ternary Operator** | 2.4, 2.5 | `condition ? valueIfTrue : valueIfFalse` |
