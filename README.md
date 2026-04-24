# 🎮 Find Your Hat

เกม Terminal-based บน Node.js ผู้เล่นต้องเดินหาลูกบอล ⚾ โดยหลบหลุม ☢ และไม่ออกนอกแผนที่

> โปรเจกต์ฝึก JavaScript พื้นฐาน — Class, Array 2 มิติ, Loop, และการรับ Input จาก Terminal

---

## 📸 Preview

```
☝️  ✻  ✻  ⛳︎
✻  ⛳︎  ✻  ✻
✻  ✻  ⛑️  ✻
⛳︎  ✻  ✻  ⛳︎

Go go go [w = up] [s = down] [a = left] [d = right] :
```

**สัญลักษณ์ในเกม**

| Symbol | Meaning |
|:------:|---------|
| ☝️ | ผู้เล่น (Player) |
| ⛑️ | หมวก เป้าหมายที่ต้องไปให้ถึง |
| ⛳︎ | หลุม เหยียบแล้วแพ้ |
| ✻ | พื้นดิน เดินผ่านได้ |

---

## ✨ Features

- เดินได้ 4 ทิศทาง (ขึ้น / ลง / ซ้าย / ขวา) ด้วยปุ่ม `w` `a` `s` `d`
- ตรวจสอบการออกนอกแผนที่
- ตรวจสอบการตกหลุม
- ตรวจสอบเงื่อนไขชนะเมื่อเจอลูกบอล
- Render แผนที่ใหม่ทุกครั้งที่เดิน (ใช้ `console.clear()`)

---

## 🛠️ Technologies

- **Node.js** — Runtime สำหรับรัน JavaScript นอก browser
- **prompt-sync** — Library รับ input จาก terminal แบบ synchronous
- **JavaScript ES6+** — ใช้ Class, Arrow Function, และ Template Literal

---

## 🚀 Getting Started

### Prerequisites

ต้องมี [Node.js](https://nodejs.org) เวอร์ชัน 14 ขึ้นไป ติดตั้งในเครื่อง

### Installation

1. Clone repository หรือ download ไฟล์
   ```bash
   git clone <repository-url>
   cd find-your-hat
   ```

2. ติดตั้ง dependencies
   ```bash
   npm install
   ```

3. รันเกม
   ```bash
   node game.js
   ```

---

## 🎯 How to Play

1. ผู้เล่น ☝️ จะเริ่มที่มุมซ้ายบนของแผนที่
2. พิมพ์ตัวอักษรเพื่อเดิน แล้วกด Enter
   - `w` = เดินขึ้น
   - `s` = เดินลง
   - `a` = เดินซ้าย
   - `d` = เดินขวา
3. **เงื่อนไขจบเกม**
   - ✅ เดินไปเจอหมวก ⛑️ → **ชนะ**
   - ❌ เดินไปเหยียบหลุม ⛳︎ → **แพ้**
   - ❌ เดินออกนอกแผนที่ → **แพ้**

---

## 📂 Code Structure

```
find-your-hat/
├── node_modules/
├── game.js             # Logic ของเกมทั้งหมด
├── package.json
├── package-lock.json
└── README.md
```

### ภาพรวมของ `game.js`

```javascript
class Field {
  constructor(field) { ... }    // เก็บแผนที่และพิกัดของ player
  play() { ... }                // Loop หลักของเกม
}
```

**Flow การทำงานใน 1 รอบของ loop**

1. แสดงแผนที่
2. ลบ player ออกจากตำแหน่งเดิม (ทำให้เป็นพื้น)
3. รับ input จากผู้เล่น
4. อัปเดตพิกัด (`areaY`, `areaX`) ตามทิศที่เดิน
5. ตรวจสอบเงื่อนไขจบเกม (นอกแผนที่ / ตกหลุม / เจอลูกบอล)
6. ถ้ายังไม่จบ → วาง player ที่ตำแหน่งใหม่ แล้ววนกลับข้อ 1

---

## 🔮 Future Improvements

- [ ] Random map generation — สุ่มตำแหน่งหลุมและลูกบอลทุกเกม
- [ ] ปรับระดับความยาก (small / medium / large map)
- [ ] นับจำนวนก้าวเดินและแสดงเป็น score
- [ ] เพิ่ม validation สำหรับ input ที่ไม่ใช่ `w/a/s/d`
- [ ] แสดงแผนที่สุดท้ายก่อนจบเกม (เห็นว่า player ตกหลุมตรงไหน)
- [ ] ใช้ `readline` แบบ raw mode เพื่อให้ไม่ต้องกด Enter ทุกครั้ง

---

## 📝 What I Learned

- การใช้ **ES6 Class** และการเก็บ state ผ่าน `this`
- การจัดการ **Array 2 มิติ** โดยใช้ `field[Y][X]` เป็นพิกัด
- การใช้ `map()` + `join()` เพื่อแปลง array เป็น string สำหรับแสดงผล
- การออกแบบ **Game Loop** ด้วย `while (true)` และ `break`
- การใช้ `require()` เพื่อ import external library

----

## บันทึกกระบวนการคิด (สร้าง)

Setup
1. เตรียมโฟลเดอร์โปรเจกต์ → npm init -y → npm install prompt-sync
2. เตรียม Git repo → git init → git push

Import & Constants
3. require('prompt-sync') และส่ง option { sigint: true } เพื่อให้กด Ctrl+C ได้
4. ประกาศ const สำหรับสัญลักษณ์ 4 ตัว: hat ⛑️ / hole ⛳︎ / ground ✻ / player ☝️

Class Design
5. สร้าง class Field พร้อม constructor เก็บ field, areaY, areaX
6. กำหนด map ขนาด 4×4 (array 2 มิติ)

Game Loop (method play)
7. ใช้ while(true) วน loop จนกว่าจะ break
8. แต่ละรอบ:
   a. console.clear() + แสดงแผนที่
   b. ลบ player ที่ตำแหน่งเดิม (set เป็น ground)
   c. รับ input w/a/s/d จาก prompt
   d. ขยับพิกัด areaY / areaX ตามทิศที่กด
9. ตรวจเงื่อนไขจบเกมด้วย if (ไม่ใช่ฟังก์ชันแยก):
   - ออกนอกแผนที่ → break
   - ตกหลุม → break
   - เจอลูกบอล → break
10. ถ้ายังไม่จบเกม → วาง player ที่พิกัดใหม่ แล้ววน loop กลับไปข้อ 8

---

## 👤 Author

**Jakkrit**
Full Stack Developer in training | Former Civil Engineer

---

## 📄 License

MIT License — ใช้งานได้อย่างอิสระ
