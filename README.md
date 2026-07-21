# Com Med ปี 5 — เว็บติวสอบ

เว็บไซต์ทบทวนสำหรับรายวิชา Community Medicine ปี 5 ประกอบด้วย

| หน้า | เนื้อหา |
|---|---|
| `index.html` | หน้าแรก + ตาราง blueprint สัดส่วนข้อสอบ |
| `summary.html` | สรุปเนื้อหาครบ 22 เล็คเชอร์ (โหลดจาก `summary.md`) |
| `quiz.html` | MCQ 200 ข้อ 5 ตัวเลือก พร้อมเฉลยละเอียดภาษาไทย |
| `crq.html` | CRQ 10 ข้อ พิมพ์คำตอบเองแล้วเทียบแนวคำตอบ |

ทุกหน้าเป็น static HTML ไม่ต้องใช้ backend — เปิดจากไฟล์ก็ได้ หรือ deploy ขึ้น GitHub Pages

---

## สัดส่วนข้อสอบ (อ้างอิงคู่มือ commed ปี 5-2569 หมวดที่ 5)

ข้อสอบจริงคือ **MCQ 56 ข้อ (20% ของคะแนนรายวิชา)** และ **CRQ 4 ข้อ (10%)**
ชุดฝึกนี้ขยายตามสัดส่วนเดิมทุกหัวข้อ

| หัวข้อ | MCQ จริง | MCQ ชุดนี้ | CRQ ชุดนี้ |
|---|:---:|:---:|:---:|
| 1. Introduction to occupational medicine | 4 | 14 | – |
| 2. Occupational and environmental diseases | 24 | 86 | 3 |
| 5. Walkthrough survey + health risk assessment | 8 | 29 | 2 |
| 6. Emergency preparedness | 4 | 14 | – |
| 9. Palliative Medicine | 16 | 57 | 5 |
| **รวม** | **56** | **200** | **10** |

> **หมายเหตุ:** Community Project ไม่มีข้อสอบ MCQ ใน blueprint
> ประเมินจากรายงานกลุ่มและการนำเสนอแทน (20% ของคะแนนรวม)

---

## วิธี deploy ขึ้น GitHub Pages

### แบบที่ 1 — ผ่านเว็บ GitHub (ง่ายที่สุด ไม่ต้องใช้ command line)

1. เข้า <https://github.com/new> สร้าง repository ใหม่
   - **Repository name:** `commed-quiz` (หรือชื่ออื่นที่ต้องการ)
   - เลือก **Public** (GitHub Pages ฟรีต้องเป็น public)
   - **ไม่ต้อง** ติ๊ก "Add a README file"
   - กด **Create repository**

2. ในหน้า repo ที่เพิ่งสร้าง กด **uploading an existing file**

3. **ลากไฟล์ทั้งหมดในโฟลเดอร์ `site/` เข้าไปวาง** (index.html, quiz.html, crq.html,
   summary.html, summary.md, data.js, crq-data.js, README.md)

4. กด **Commit changes**

5. ไปที่แท็บ **Settings** → เมนูซ้าย **Pages**
   - **Source:** เลือก `Deploy from a branch`
   - **Branch:** เลือก `main` และโฟลเดอร์ `/ (root)` แล้วกด **Save**

6. รอประมาณ 1–2 นาที แล้วเข้าเว็บที่
   `https://<ชื่อผู้ใช้ github>.github.io/commed-quiz/`

---

### แบบที่ 2 — ผ่าน command line (git)

```bash
# 1. เข้าไปในโฟลเดอร์ site
cd site

# 2. เริ่ม git repo
git init
git add .
git commit -m "Com Med ปี 5: สรุปเนื้อหา + MCQ 200 ข้อ + CRQ 10 ข้อ"
git branch -M main

# 3. เชื่อมกับ repo บน GitHub (สร้าง repo เปล่าไว้ก่อนที่ github.com/new)
#    แก้ USERNAME และ REPO ให้ตรงกับของตัวเอง
git remote add origin https://github.com/USERNAME/REPO.git

# 4. push ขึ้นไป
git push -u origin main
```

จากนั้นไปเปิด GitHub Pages ตามขั้นตอนที่ 5–6 ของแบบที่ 1

---

### แบบที่ 3 — GitHub Desktop

1. เปิด GitHub Desktop → **File → New repository**
   - ตั้งชื่อ `commed-quiz`
   - **Local path:** เลือกที่เก็บ แล้วกด **Create repository**
2. เปิดโฟลเดอร์ที่สร้างขึ้น แล้ว **คัดลอกไฟล์ทั้งหมดจาก `site/` เข้าไปวาง**
3. กลับมาที่ GitHub Desktop จะเห็นไฟล์ทั้งหมดใน Changes
   - ใส่ข้อความ commit แล้วกด **Commit to main**
4. กด **Publish repository** (อย่าลืม **เอาติ๊ก "Keep this code private" ออก**)
5. เปิด GitHub Pages ตามขั้นตอนที่ 5–6 ของแบบที่ 1

---

## การแก้ไข/เพิ่มคำถามในภายหลัง

ไฟล์ต้นทางอยู่ในโฟลเดอร์แม่ (ไม่ต้อง upload ขึ้น GitHub)

| ไฟล์ | หน้าที่ |
|---|---|
| `bank.py` | คลัง MCQ — เพิ่มข้อใหม่ด้วย `Q(...)` ก่อนวงเล็บปิด `]` |
| `crq.py` | คลัง CRQ — เพิ่มข้อใหม่ด้วย `C(...)` |
| `build_site.py` | สคริปต์ build เว็บทั้งหมด |

หลังแก้ไขให้รัน

```bash
python3 build_site.py
```

ไฟล์ในโฟลเดอร์ `site/` จะถูกสร้างใหม่ทั้งหมด แล้ว push ขึ้น GitHub อีกครั้ง

> **สำคัญ:** `balance()` จะสลับตำแหน่งคำตอบถูกให้กระจาย A–E เท่าๆ กันทุกครั้งที่ build
> ดังนั้นลำดับตัวเลือกจะเปลี่ยนไปจากที่พิมพ์ใน `bank.py` — เป็นเรื่องปกติ

---

## หมายเหตุความถูกต้องของเนื้อหา

เนื้อหาสรุปและคำถามทั้งหมดสร้างจากไฟล์เล็คเชอร์ 22 ไฟล์ + คู่มือรายวิชา
มี **2 จุดที่สไลด์ไม่ได้ระบุรายละเอียดครบ** และเติมจากตำรามาตรฐาน
(มีเครื่องหมาย ⚠️ กำกับไว้ในหน้าสรุป) ควรยืนยันกับอาจารย์อีกครั้ง

1. **เครื่องมือ 7 ชิ้นในการศึกษาชุมชน** — สไลด์ระบุแค่หัวข้อ ไม่ได้แจกแจงรายชื่อ
2. **สูตร O.P.R. ของ Hanlon method** — สไลด์กล่าวถึงข้อดี/ข้อจำกัดแต่ไม่แสดงสูตรเต็ม
