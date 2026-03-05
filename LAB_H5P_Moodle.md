# ใบงานการทดลอง: สร้างสื่อ Interactive ด้วย H5P ใน Moodle
## หัวข้อ: Docker · GitHub Actions · CI/CD · Testing · YAML
---

## 🎯 วัตถุประสงค์
**นักศึกษาสามารถ**
1. สร้างสื่อการสอนแบบโต้ตอบด้วย H5P ตามรูปแบบที่กำหนดได้
2. ออกแบบ Branching Scenario จำลองสถานการณ์แก้ปัญหา CI/CD จริง
3. เชื่อมต่อ H5P Activity กับ Moodle Gradebook อย่างถูกต้อง

---
## การใช้งาน H5P ต้องเข้าไปโหลดโดย Admin ก่อนในครั้งแรก ครูผู้สอนจึงจะสามารถสร้าง H5P ตาม Content Types ที่ admin โหลดมา
1. admin เข้าไปสร้าง Activity H5P
2. เลือก Content type ที่ต้องการ เช่น Interactive video -> Get เพื่อดาวส์โหลด


## 📝 ส่วนที่ 1: Interactive Video — Docker Container Basics (10 คะแนน)

### แนวคิด

ฝังคำถามและคำอธิบายลงในวิดีโออธิบาย Docker  
ผู้เรียนต้องตอบคำถามในจุดที่กำหนดก่อนดูเนื้อหาต่อ

### ขั้นตอนการสร้าง

**ขั้นที่ 1 — เพิ่ม H5P Activity ในรายวิชา**

1. เข้า Moodle → รายวิชาของคุณ → คลิก **Turn editing on**
2. คลิก **+ Add an activity or resource** → เลือก **H5P** → **Add**
3. กรอกชื่อ Activity:

```
Description: วิดีโอแบบโต้ตอบแนะนำ Docker Container
             พร้อมคำถามทดสอบความเข้าใจ 3 ข้อ
Title: Docker
```

**ขั้นที่ 2 — เลือก Content Type**

คลิก **Create content** → เลือก **Interactive Video**

**ขั้นที่ 3 — (Step 1) ใส่วิดีโอ**

| ฟิลด์ | ค่าที่กรอก |
|-------|-----------|
| Video URL | `https://www.youtube.com/watch?v=Gjnup-PuquQ` (Docker in 100 Seconds) |
| Behavioural settings -> Start at | `0` |
| Behavioural settings -> Disable navigation | Forward (ไม่ให้ Forward Video)|

> 💡 หากวิดีโอ Embed ไม่ได้ ให้ใช้วิดีโอ Docker อื่นที่ Embed ได้ เช่น `https://youtu.be/3c-iBn73dDE`

**ขั้นที่ 4 — (Step 2)เพิ่ม Single Choice ที่ Timestamp 0:45 โดยเลื่อนเวลาไปที่ 0:45 แล้วเลือกรูปแบบ interactive จากเมนูบาร์ด้านบน ที่เป็น Single Choice Set**

```

  คำถามที่ 1  (Timestamp: 0:45)                             
══════════════════════════════════════════════════════════
  Display time : 0:45:00 - 0:46:00 (แสดง 1 วินาที หลังกดตอบ)  
  Pause video: ✓                                          
  Display as: Poster                                      
  Title: Docker Containner vs Virtual Machine             
  Question: Docker Container แตกต่างจาก Virtual Machine    
  อย่างไรในแง่ของทรัพยากร?                                    
                                                          
   ● Container ใช้ทรัพยากรน้อยกว่าเพราะแชร์ OS Kernel            
   ○ Container ใช้ทรัพยากรมากกว่า VM                           
   ○ Container และ VM ใช้ทรัพยากรเท่ากัน                        
   ○ Container ต้องการ Hardware จำเพาะ                       
  Feedback ถูก: "ถูกต้อง! Container ใช้ OS Kernel              
  ร่วมกับ Host ทำให้เบาและเร็วกว่า VM มาก"                      
  Feedback ผิด: "ลองคิดใหม่ — Container ต่างกับ VM              
  ตรงที่ไม่ต้องมี OS เป็นของตัวเอง"                               
══════════════════════════════════════════════════════════
```
**ทำการปรับขนาดของ Poster และตำแหน่งที่ต้องการให้แสดงบนหน้าจอ (ปรับให้เห็นข้อถามและคำตอบได้ครบถ้วน)**

**ขั้นที่ 5 — เพิ่ม Text Overlay ที่ Timestamp 1:10**

```

Text Overlay (Timestamp: 1:10 — แสดง 8 วินาที)            

💡 Docker Architecture                                  
 App A │ App B │ App C ← Containers     
    Docker Engine      ← Runtime        
       Host OS         ← Shared         
                 
```
**เลือก background color และปรับขนาดของ Poster และตำแหน่งที่ต้องการให้แสดงบนหน้าจอ**

**ขั้นที่ 6 — เพิ่ม Multiple Choice ที่ Timestamp 1:45**

```

  คำถามที่ 2  (Timestamp: 1:45)                             
══════════════════════════════════════════════════════════
  ตั้งค่าให้แสดง 1 วินาทีหลังจากตอบคำถาม                         
 Pause video และ เลือกรูปแบบ Poster                         
 Title: สร้าง Docker Image จาก Dockerfile?                 
 Question: คำสั่งใดใช้สร้าง Docker Image จาก Dockerfile?      
                                                          
  □ docker run -it ubuntu                                 
  ☑ docker build -t myapp:1.0 .                           
  □ docker pull myapp                                     
  □ docker start myapp                                    
                                                          
  Tip text: "มองหาคำสั่งที่ต้องการ Dockerfile เป็น Input"       
══════════════════════════════════════════════════════════
```
**ทำการปรับขนาดของ Poster และตำแหน่งที่ต้องการให้แสดงบนหน้าจอ**

**ขั้นที่ 7 — เพิ่ม Fill in the Blank ที่ Timestamp 2:00**

```

  Title: คำถามที่ 3 — Fill in the Blank (Timestamp: 2:00)   
  Task description: Fill in the missing words
  Line of text:
  คำสั่งดาวน์โหลด Image จาก Docker Hub คือ                    
  docker *pull* และคำสั่งรัน Container คือ                    
  docker *run*                                            

```

**ขั้นที่ 8 — Behavioural Settings**

```
✓ Start with bookmarks menu open เพื่อ bookmarks เมนูไว้ด้านข้าง เพื่อให้ง่ายในการใช้งาน
✓ Show button for rewinding 10 seconds มีปุ่มสำหรับกดย้อนกลับไป 10 วินาที   
Disable navigation: Forward ไม่ให้เลื่อน Video ไปข้างหน้า
Percentage to pass: 70
```

**ขั้นที่ 9 — Grade Settings ใน Moodle**

```
Grade category: แบบทดสอบ
Grade to pass: 7
Maximum grade: 10

```

---


## 📝 ส่วนที่ 2: Drag and Drop — YAML Structure Mapping (10 คะแนน)

### แนวคิด

ให้ผู้เรียนลากชิ้นส่วนโครงสร้าง YAML ไปวางในตำแหน่งที่ถูกต้องบน Workflow Diagram

### ขั้นตอนการสร้าง

**ขั้นที่ 1 — สร้าง Activity → เลือก Drag and Drop**

**ขั้นที่ 2 — อัปโหลด Background Image**

สร้างรูป "GitHub Actions Workflow Diagram" หรือใช้ Template ด้านล่าง:
**ใช้รูปที่อยู่ในโฟลเดอร์ images ได้**
```

┌──────────────────────────────────────────────────────┐
│              GitHub Actions Workflow                 │
│                                                      │
│  [ZONE A]           [ZONE B]          [ZONE C]       │
│  ──────────         ──────────        ──────────     │
│  Top-level Key      Job Config        Step Action    │
│                                                      │
│  ┌──────────┐   ┌──────────────┐   ┌──────────────┐  │
│  │          │   │              │   │              │  │
│  │ ???      │   │ ???          │   │ ???          │  │
│  │          │   │              │   │              │  │
│  └──────────┘   └──────────────┘   └──────────────┘  │
└──────────────────────────────────────────────────────┘

ขนาดแนะนำ: 900 x 500 px
```
**ขั้นที่ 2 — Task Description**

```
Description: ลาก YAML Keywords แต่ละรายการไปวางในหมวดหมู่
      ที่ถูกต้องตามโครงสร้าง GitHub Actions Workflow
Title: GitHub Actions Workflow
```
**ขั้นที่ 3**
  **Step 1: Add Background image**  
   Task size: 900 X 500

  **Step 2 Task: — สร้าง Drop Zones**

```
เลือก Add drop zone (icon แรก ที่เป็นรูปวงกลมซ้อนกัน) กำหนดรายละเอียดของแต่ละ drop zone ดังนี้

Drop Zone A
Label: "Top-level Keys"
  กดปุ่ม Done
  ปรับตำแหน่งด้วยการลากขยายขนาด และ Drag & Drop ลงในตำแหน่งกรอบสี่เหลี่ยม Zone A
  เลือก Enable Auto-Align ถ้าต้องการ Align อัตโนมัติ

Drop Zone B
Label: "Job Configuration"  
  กดปุ่ม Done
  ปรับตำแหน่งด้วยการลากขยายขนาด และ Drag & Drop ลงในตำแหน่งกรอบสี่เหลี่ยม Zone B

Drop Zone C
Label: "Step Actions"  
  กดปุ่ม Done
  ปรับตำแหน่งด้วยการลากขยายขนาด และ Drag & Drop ลงในตำแหน่งกรอบสี่เหลี่ยม Zone C

```

**ขั้นที่ 3 — สร้าง Draggable Elements**
เลือกที่ไอคอนรูปตัวอักษร (T) สร้าง text ของแต่ละ zone ดังข้อมูลด้านล่าง
```
YAML Keywords → Drop Zone A (Top-level Keys):
  ├── "name:"          → Select all
  ├── "on:"            → Select all
  ├── "jobs:"          → Select all
  └── "env:"           → Select all

Job Keywords → Drop Zone B (Job Config):
  ├── "runs-on:"       → Select all
  ├── "needs:"         → Select all
  └── "if:"            → Select all

Step Keywords → Drop Zone C (Step Actions):
  ├── "uses:"          → Select all
  ├── "run:"           → Select all
  └── "with:"          → Select all

```
**ขั้นที่ 4 แก้ไขแต่ละ drop zone เพื่อเลือกตัวเลือกที่ถูกต้องของแต่ละ zone**


**ขั้นที่ 5 — Overall Feedback**

```
0–49%:  "ลองศึกษาโครงสร้าง GitHub Actions YAML แล้วลองใหม่อีกครั้ง"
50–79%: "ดีมาก! แต่ยังมีบางคีย์ที่สับสน ตรวจสอบ Documentation อีกครั้ง"
80–100%: "ยอดเยี่ยม! คุณเข้าใจโครงสร้าง GitHub Actions YAML เป็นอย่างดี"
```

---

## 📝 ส่วนที่ 3: Fill in the Blanks — Docker Commands (5 คะแนน)

### ขั้นตอนการสร้าง

**ขั้นที่ 1 — สร้าง Activity → เลือก Fill in the Blanks**

**ขั้นที่ 2 — Text Block 1: Dockerfile Instructions**

```
Title: เติมคำสั่ง Dockerfile ในช่องว่างให้ถูกต้อง

Task description: เติมคำสั่ง Dockerfile ในช่องว่างให้ถูกต้อง

Text blocks:
การเขียน Dockerfile เริ่มด้วย *FROM* เพื่อระบุ Base Image
เช่น *FROM node:18-alpine* เพื่อใช้ Node.js บน Alpine Linux
คำสั่ง *WORKDIR /app* กำหนด Working Directory ภายใน Container
จากนั้นใช้ *COPY package*.json ./* เพื่อคัดลอก package files
รัน *RUN npm install* เพื่อติดตั้ง Dependencies
แล้วใช้ *COPY . .* เพื่อคัดลอกโค้ดทั้งหมด
สุดท้าย *EXPOSE 3000* เปิด Port และ *CMD ["node","app.js"]*
เพื่อสั่งรันแอปเมื่อ Container เริ่มทำงาน
```

**ขั้นที่ 3 — Text Block 2: docker-compose.yml**

```
Text:
ไฟล์ *docker-compose.yml* ใช้กำหนดและรันหลาย Container พร้อมกัน
ระดับบนสุดเริ่มด้วย *version: '3.8'* ตามด้วย *services:*
แต่ละ Service ระบุ *image:* หรือ *build:* เพื่อกำหนด Container Image
กำหนด *ports:* เพื่อ Map Port เช่น *"8080:80"*
กำหนด *volumes:* เพื่อ Mount ไดเร็กทอรี
และกำหนด *environment:* เพื่อส่งตัวแปร Environment
คำสั่ง *docker compose up -d* รัน Services ทั้งหมดใน Background
และ *docker compose down* หยุดและลบทุก Container
```

**ขั้นที่ 4 — Behavioural Settings**

```
✓ Enable "Retry" button
✓ Enable "Show solution" button  
Case sensitive: ✗ (ปิด)
```

---

## 📝 ส่วนที่ 4: Branching Scenario — Debug a Failed CI/CD Pipeline (15 คะแนน)

### แนวคิด

Branching Scenario สร้างสถานการณ์จำลองที่ผู้เรียนต้องตัดสินใจแก้ปัญหา Pipeline ล้มเหลว  
การเลือกคำตอบที่ต่างกันนำไปสู่ผลลัพธ์ที่ต่างกัน เหมือนเล่น Visual Novel
**ขั้นตอนในการทดลอง จำลองไว้เพียงบางส่วน ไม่ได้ทำ Scenario ครบทั้งหมด**
```
โครงสร้าง Branching Scenario:
                    ┌──────────────────┐
                    │  START: Pipeline │
                    │  Failed!         │
                    └────────┬─────────┘
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
        [ตรวจ Log]    [Restart]     [ตรวจ Code]
              │              │              │
       ┌──────┤        [Dead end]    ┌──────┤
       ▼      ▼                     ▼      ▼
   [ดู Error] [Skip]          [หา Bug]  [คาดเดา]
       │                          │
       ▼                          ▼
   [แก้ไข]                    [แก้ไข]
       │                          │
       └──────────┬───────────────┘
                  ▼
             [SUCCESS ✅]
```
**ขั้นตอนในการทดลอง จำลองไว้เพียงบางส่วน ไม่ได้ทำ Scenario ครบทั้งหมด**

### ขั้นตอนการสร้าง

**ขั้นที่ 1 — สร้าง Activity → เลือก Branching Scenario**

**ขั้นที่ 2 — ตั้งค่าภาพรวม**
คลิ๊กที่รูปเฟืองเพื่อตั้งค่า
```
[Configure starting screen]
   Course Title: CI/CD Pipeline Crisis!
   Course Detail:
      เวลา 14:00 น. ระบบ Production ล่ม คุณคือ DevOps Engineer คนเดียวที่อยู่ในออฟฟิศ
      Pipeline ล้มเหลว Deploy ไม่ผ่าน ทีมรอคุณแก้ปัญหา...
[Behavioural settings]
  ✓ Randomize Branching Question
```
**ขั้นที่ 3 — Scene 2: แจ้งเตือน Pipeline ล้มเหลว (Starting Scene)**

```
Content Type: Course Presentation
Title: 🔴 GitHub Actions: Build Failed

Text:
    GitHub Actions — Run #247 — FAILED ❌
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    Workflow:  CI Pipeline
    Trigger:   push to main
    Duration:  2m 34s
    Status:    ● FAILURE
    Jobs:
      ✅ checkout        — Success
      ✅ setup-python    — Success
      ❌ run-tests       — FAILED
      ⏭ build-docker    — Skipped
      ⏭ deploy          — Skipped
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

```
**ขั้นตอนที่ 4 Branching Question**
 ลาก Branching Question วางต่อจากหน้า Scene 2 และกำหนดค่าดังนี้
```
Question: คุณจะทำอะไรก่อน?
Branching choices:
  ดู Log ของ run-tests ทันที    → scene-2a
  Restart Workflow ก่อนโดยไม่ดู  → scene-2b
  ถาม Developer ว่าแก้อะไรมา   → scene-2c
```

**ขั้นที่ 5 — Scene 2a: ดู Log (เส้นทางถูกต้อง)**

```
Title: ✅ ดูหลักฐานก่อนแก้ — ดีมาก!

Text:
    Log จาก run-tests Job:
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    $ pytest tests/ -v
    FAILED tests/test_auth.py::test_login_success
    FAILED tests/test_auth.py::test_logout
    ======================== 2 failed ================
    E  AssertionError: assert 401 == 200
    E  Expected status code 200, got 401 Unauthorized
    Error: Process completed with exit code 1.
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
**ขั้นตอนที่ 6 Branching Question**
```
Question:พบว่า Login test ล้มเหลว: Status 401 Unauthorizedคุณจะทำอะไรต่อ?

Branching choices:
  เปิดไฟล์ test_auth.py ดู Test    → scene-3a
  เปิดไฟล์ auth.py ดู Source Code  → scene-3b
  เพิ่ม Secret Key ใน GitHub Repo  → scene-3c
```

**ขั้นที่ 8 — Scene 2b: Restart โดยไม่ดู Log (เส้นทางผิด)**

```
Scene ID: scene-2b
Title: ❌ Restart โดยไม่วิเคราะห์ — ไม่ถูกต้อง

Text:
      คุณกด "Re-run all jobs"...
      หลังรอ 3 นาที ผลลัพธ์คือ:
        ❌ run-tests — FAILED (อีกครั้ง!)
      ปัญหาเดิมกลับมา! การ Restart โดยไม่ดู Log
      เสียเวลาเปล่าและทีมรอนานขึ้น
      📌 บทเรียน: DevOps Engineer ที่ดีต้อง
        "ดู Log ก่อนแก้" เสมอ

[Advanced branching options]
  Special  action after this content: jump to another branch 
  Select a branch to jump to* → scene-2
```

**ขั้นที่ 9 — Scene 2c: ถาม Developer ก่อน**

```
Title: 💬 ถาม Developer — ได้ข้อมูลเพิ่มเติม

Text:
    Developer แจ้งว่า:
    "ผมเพิ่ง merge PR #89 เข้า main ครับ
    แก้ระบบ Authentication ให้ใช้ JWT แทน Session
    อาจต้องอัปเดต Test ด้วยครับ"

    ข้อมูลนี้มีประโยชน์ แต่คุณยังต้องดู Log เพื่อยืนยัน

Branching choices:
  ดู Log ของ run-tests ต่อ → scene-2a
  แก้ Test โดยตรงเลย      → scene-3-wrong
```

**ขั้นที่ 10 — Scene 3a: ดู Test File**

```
Scene ID: scene-3a
Title: 📄 ตรวจสอบ test_auth.py

Text:
    # tests/test_auth.py (เดิม)
    def test_login_success():
        response = client.post("/login", 
            data={"user": "admin", "pass": "1234"})
        assert response.status_code == 200
        assert "session_id" in response.cookies  # ← ปัญหา!

    พบว่า Test ยังตรวจสอบ session_id (ระบบเก่า)
    แต่ระบบใหม่ใช้ JWT Token แล้ว

Branching choices:
  แก้ Test ให้รองรับ JWT  → scene-4-fix
  Rollback โค้ดกลับเป็น Session  → scene-4-rollback
```

**ขั้นที่ 11 — Scene 4-fix: แก้ Test ให้ถูกต้อง (เส้นทาง Success)**

```
Title: 🔧 แก้ไข Test ให้รองรับ JWT

Text:
    คุณแก้ไข test_auth.py:
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    # tests/test_auth.py (แก้ใหม่)
    def test_login_success():
        response = client.post("/login", 
            json={"username": "admin", "password": "1234"})
        assert response.status_code == 200
        assert "access_token" in response.json()  # ✅ JWT
        assert response.json()["token_type"] == "bearer"
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    git add tests/test_auth.py
    git commit -m "fix: update auth tests for JWT"
    git push origin fix/jwt-tests"

Branching choices:
  รอดู Pipeline Results  → scene-success
```

**ขั้นที่ 12 — Scene Success: Pipeline ผ่าน!**

```
Title: 🎉 Pipeline PASSED!

Text:
    GitHub Actions — Run #248 — SUCCESS ✅
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
      ✅ checkout        — 2s
      ✅ setup-python    — 12s
      ✅ run-tests       — 34s  (2 passed!)
      ✅ build-docker    — 45s
      ✅ deploy-staging  — 28s
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    Duration: 1m 58s
    🏆 บทเรียนสำคัญจาก Scenario นี้:
      1. ดู Log ก่อนแก้เสมอ
      2. แก้ที่ Root Cause ของปัญหา
      3. Commit Message ต้องบอกว่าแก้อะไร
[Advanced branching options]
  Special  action after this content: Custom end scenario 
  Feedback title: จบขั้นตอนการฝึก
  Feedback text: ทำได้ดีมากครับ คุณสามารถแก้ไขปัญหาได้อย่างถูกต้อง
```
---

## 📝 ส่วนที่ 5: Mark the Words — YAML Syntax Identification (5 คะแนน)

### แนวคิด

ผู้เรียนคลิกเลือกคำหรือ Keyword ที่เข้าเงื่อนไขที่กำหนดในข้อความ YAML จริง

### ขั้นตอนการสร้าง

**ขั้นที่ 1 — สร้าง Activity → เลือก Mark the Words**

**ขั้นที่ 2 — คำถามชุดที่ 1: ระบุ Docker Instruction**

```
Title: Mark the words
Task description:
  คลิกเลือกเฉพาะคำที่เป็น "Dockerfile Instruction" (คำสั่งใน Dockerfile)

Textfield:
ในการเขียน *FROM* เพื่อระบุ Base Image นั้น เราจะระบุ
ชื่อ Image เช่น python หรือ node ตามด้วย Tag
คำสั่ง *WORKDIR* กำหนดโฟลเดอร์ทำงาน ส่วน *COPY*
และ *ADD* ใช้นำไฟล์เข้า Image แตกต่างกันที่
*ADD* รองรับ URL และ Auto-extract tar
คำสั่ง *RUN* รันคำสั่งขณะ Build เช่น npm install
*ENV* กำหนด Environment Variable และ *ARG* กำหนด
Build Argument ส่วน *EXPOSE* ประกาศ Port แต่ไม่ได้
Publish จริง ต้องใช้ -p ตอน docker run
สุดท้าย *CMD* และ *ENTRYPOINT* กำหนดคำสั่งเริ่มต้น
ต่างกันที่ *ENTRYPOINT* ไม่ถูก Override ง่าย ๆ

```

**ขั้นที่ 3 — Behavioural Settings**

```
✓ Enable "Check" button
✓ Enable "Show solution" button
✓ Enable "Retry" button
```

---

## 📝 ส่วนที่ 6: Sort the Paragraphs — CI/CD Pipeline Steps (5 คะแนน)

### แนวคิด

ผู้เรียนลากย่อหน้าที่สลับลำดับไปจัดเรียงใหม่ให้ถูกต้อง  
ใช้กับขั้นตอนที่มี Sequence สำคัญ เช่น การทำงานของ Pipeline

### ขั้นตอนการสร้าง

**ขั้นที่ 1 — สร้าง Activity → เลือก Sort the Paragraphs**

**ขั้นที่ 2 — ชุดที่ 1: ลำดับขั้นตอน CI/CD Pipeline**

```
Title: Sort the Paragraphs
Task description:
  เรียงลำดับขั้นตอนของ CI/CD Pipeline จากเริ่มต้นจนสำเร็จ

Paragraphs (ใส่ตามลำดับที่ถูกต้อง — H5P จะสลับให้อัตโนมัติ):

Paragraph 1 (ลำดับที่ 1):
  📁 Developer เขียนโค้ดและ Push ขึ้น Git Repository
  git add . && git commit -m "feat: new feature"
  git push origin feature/new-feature
  GitHub รับ Push Event และส่ง Webhook ไปยัง CI Server

Paragraph 2 (ลำดับที่ 2):
  🔄 GitHub Actions รับ Trigger และสร้าง Runner VM
  Runner ดาวน์โหลดโค้ดด้วย actions/checkout
  ติดตั้ง Environment ที่จำเป็น (Python, Node, Java ฯลฯ)
  ติดตั้ง Dependencies จาก requirements.txt หรือ package.json

Paragraph 3 (ลำดับที่ 3):
  🧪 Runner รัน Test Suite อัตโนมัติ
  pytest tests/ -v --cov=app (Unit + Integration Tests)
  ตรวจสอบ Code Coverage ต้องไม่ต่ำกว่า 80%
  รัน Linter และ Security Scanner

Paragraph 4 (ลำดับที่ 4):
  🐳 เมื่อผ่าน Test ทั้งหมด Build Docker Image
  docker build -t myapp:${{ github.sha }} .
  รัน Container Test เพื่อตรวจสอบ Image
  Tag Image และ Push ขึ้น Container Registry

Paragraph 5 (ลำดับที่ 5):
  🚀 Deploy Image ขึ้น Staging Environment
  อัปเดต Kubernetes Deployment หรือ docker-compose
  รัน Smoke Test บน Staging ตรวจสอบ Health Endpoint
  แจ้งทีมผ่าน Slack / Email ว่า Deploy สำเร็จ

Paragraph 6 (ลำดับที่ 6):
  ✅ Pipeline เสร็จสมบูรณ์ — สถานะ: SUCCESS
  GitHub แสดง Green Checkmark ที่ Commit
  Pull Request สามารถ Merge ได้หากผ่านทุก Check
  ทีมรับรู้ว่าโค้ดพร้อมสำหรับ Production
```
**ขั้นที่ 3 — Behavioural Settings**

```
Scoring mode: Correctly placed paragraph
✓ Enable "Retry" button
✓ Enable "Show solution" button
```

---

## 📎 แหล่งเรียนรู้เพิ่มเติม

| หัวข้อ | แหล่งอ้างอิง |
|--------|-------------|
| H5P Documentation | https://h5p.org/documentation |
| GitHub Actions Docs | https://docs.github.com/en/actions |
| Docker Documentation | https://docs.docker.com |
| Docker Curriculum | https://docker-curriculum.com |
| pytest Documentation | https://pytest.org |
| YAML Specification | https://yaml.org/spec |
| DevOps Roadmap | https://roadmap.sh/devops |

---

