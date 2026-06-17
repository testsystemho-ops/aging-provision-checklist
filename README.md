# 📋 Aging Provision Checklist — CP Axtra / Makro

> ระบบตรวจสอบสต็อกสินค้า Aging Provision พร้อม Firebase Realtime Database

---

## 🚀 วิธี Deploy บน GitHub Pages + Firebase (ทำครั้งเดียว ~10 นาที)

### ไฟล์ที่ต้องการ
```
📁 aging-provision-deploy/
  ├── index.html          ← แอปหลัก (Firebase Realtime)
  ├── aging_items.js      ← ฐานข้อมูลสินค้า 135,111 รายการ
  └── database.rules.json ← Firebase Security Rules
```

---

## ขั้นตอนที่ 1 — ตั้งค่า Firebase Realtime Database

1. ไปที่ [Firebase Console](https://console.firebase.google.com/) → เลือก project **aging-provision-checklist**
2. เมนูซ้าย → **Build** → **Realtime Database**
3. คลิก **Rules** แล้วแทนที่ด้วย:
```json
{
  "rules": {
    "aging_rows": {
      ".read": true,
      ".write": true,
      "$rowId": {
        ".validate": "newData.hasChildren(['id','store','itemno'])"
      }
    }
  }
}
```
4. คลิก **Publish** ✅

---

## ขั้นตอนที่ 2 — Upload ขึ้น GitHub Pages

### วิธีที่ 1: Drag & Drop (ง่ายที่สุด ไม่ต้องใช้ Git)

1. ไปที่ [github.com](https://github.com) → สร้าง Repository ใหม่ ตั้งชื่อ `aging-provision`
   - ✅ Public
   - ✅ Add README
2. เปิด Repository → คลิก **Add file** → **Upload files**
3. **Drag** ไฟล์ทั้ง 3 ไฟล์ (`index.html`, `aging_items.js`, `database.rules.json`) ลงไป
4. คลิก **Commit changes** (กดตกลง)
5. ไปที่ **Settings** → **Pages** → Source: **Deploy from branch** → Branch: **main** → Folder: **/ (root)**
6. คลิก **Save**

⏳ รอ ~2 นาที แล้วเข้าใช้งานที่:
```
https://[your-username].github.io/aging-provision/
```

### วิธีที่ 2: GitHub CLI (สำหรับคนที่มี Git)
```bash
git clone https://github.com/[your-username]/aging-provision.git
cp index.html aging_items.js database.rules.json aging-provision/
cd aging-provision
git add .
git commit -m "deploy aging provision checklist"
git push
```

---

## ✅ ตรวจสอบว่าระบบทำงานถูกต้อง

1. เปิด URL จาก GitHub Pages
2. Login ด้วย `admin` / `adminho`
3. สังเกต **🟢 Realtime** ที่ Header → แสดงว่า Firebase เชื่อมต่อสำเร็จ
4. เพิ่มรายการ → เปิดอีก Browser หรืออีกเครื่อง → ข้อมูลควรปรากฏทันที

---

## 👤 ผู้ใช้งาน

| Username | Password | สิทธิ์ |
|----------|----------|--------|
| `soa` | `makroho` | บันทึก + แก้ไข (ลบไม่ได้) |
| `admin` | `adminho` | บันทึก + แก้ไข + **ลบ** |

---

## 🔥 Firebase Project Info

- **Project**: aging-provision-checklist
- **Database URL**: https://aging-provision-checklist-default-rtdb.asia-southeast1.firebasedatabase.app/
- **Region**: asia-southeast1 (Singapore)

---

## 📱 รองรับทุกอุปกรณ์

- ✅ Mobile (iOS/Android)
- ✅ Tablet
- ✅ Desktop PC
- ✅ 3 Theme: White / Dark / Navy Blue

---

## 🗂️ โครงสร้างข้อมูลใน Firebase

```
aging_rows/
  {autoId}/
    id: "timestamp_random"
    store: "11"
    date: "2026-06-17"
    auditor: "SOA User"
    dept: "7"
    itemno: "125356"
    desc: "องุ่นน้ำมันถั่วเหลืองปี๊บ"
    price: 199
    aging: "FP"
    com: 167
    count: 160
    diff: -7
    display: "yes"
    priceyn: "no"
    rmPrice: "ราคาไม่ตรง"
    cond: "yes"
    storeName: "บมจ.ซีพี แอ็กซ์ตร้า สาขาพิษณุโลก 11"
    zone: "Zone2"
    regional: "Regional 1"
    sm: "คุณ ธีระพงษ์ อินจุ้มสาย"
    am: "Pongsiri Kamsaengdee"
```
