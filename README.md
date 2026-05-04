# Parasite Egg Classification Project

---

# 🧠 1. Problem Description (อธิบายโจทย์)

## 🇹🇭 ภาษาไทย

โจทย์นี้เป็นปัญหาเกี่ยวกับ **Computer Vision (การมองเห็นด้วยคอมพิวเตอร์)** โดยมีเป้าหมายคือ:

> 🔍 **จำแนกชนิดของไข่พยาธิจากภาพกล้องจุลทรรศน์**

### 📌 ข้อมูลจากโจทย์
- ใช้ dataset: **chula-parasite-dataset**
- มีทั้งหมด **11 classes (ชนิดของพยาธิ)**
- รูปภาพเป็นภาพจากกล้องจุลทรรศน์

### 📌 ความท้าทายหลัก
จากสไลด์หน้า 3–4:

1. ❗ **Train และ Test มาจากคนละสภาพแวดล้อม**
   - เช่น แสง สี กล้อง ต่างกัน
2. ❗ มี **Unknown classes**
   - พยาธิที่ไม่อยู่ใน 11 class
3. ❗ มี **Background (no-egg)**
   - รูปที่ไม่มีไข่พยาธิเลย
4. ❗ ต้องสามารถ “Reject” ได้
   - ไม่ใช่แค่ classify แต่ต้องบอกว่า "ไม่ใช่" ด้วย

### 📌 Evaluation
- ใช้ **F1-score (macro)**
  - ให้ความสำคัญทุก class เท่ากัน
- จำกัดส่ง **4 ครั้งต่อวัน**

---

## 🇬🇧 English

This problem is a **Computer Vision classification task** with the objective:

> 🔍 **Classify parasite eggs from microscopic images**

### 📌 Dataset Info
- Dataset: **Chula Parasite Dataset**
- Total **11 classes of parasite eggs**

### 📌 Key Challenges

1. ❗ **Domain Shift**
   - Training and testing data come from different conditions
2. ❗ **Unknown Classes**
   - Parasites not included in training classes
3. ❗ **Background (No Egg)**
   - Images without parasite eggs
4. ❗ **Rejection Requirement**
   - Model must detect “unknown” or “no egg”

### 📌 Evaluation
- Metric: **Macro F1-score**
- Submission limit: **4 per day**

---

# ⚙️ 2. Pipeline Overview (ภาพรวม Pipeline)

## 🇹🇭 ภาษาไทย

Pipeline ของระบบนี้สามารถแบ่งเป็น 6 ขั้นตอนหลัก:
1.  Data Collection
2.  Data Preprocessing
3.  Data Augmentation
4.  Model Training
5.  Unknown Handling
6.  Evaluation

---

# 🔍 3. Detailed Pipeline (อธิบาย Pipeline แบบละเอียด)

---

## 3.1 Data Collection (การรวบรวมข้อมูล)

### 🇹🇭
- ใช้ dataset หลัก (11 classes)
- เพิ่ม dataset จาก Kaggle เพื่อสร้าง class:
  - **Unknown (-1)**
- รวม:
  - Known classes (11)
  - Unknown classes
  - Background (no egg)

### 🇬🇧
- Use main dataset (11 classes)
- Add external datasets (e.g., Kaggle)
- Create:
  - Known classes
  - Unknown class (-1)
  - Background class

---

## 3.2 Data Preprocessing (การเตรียมข้อมูล)

### 🇹🇭
- Resize ภาพ เช่น 224x224
- Normalize pixel (0–1)
- Label Encoding:
  - 0–10 = Known classes
  - -1 = Unknown

### 🇬🇧
- Resize images (e.g., 224x224)
- Normalize pixel values
- Encode labels:
  - 0–10 for known classes
  - -1 for unknown

---

## 3.3 Data Augmentation (เพิ่มความหลากหลายข้อมูล)

### 🇹🇭
ช่วยแก้ปัญหา domain shift:
- Random rotation
- Flip
- Brightness/contrast
- Noise

### 🇬🇧
To improve generalization:
- Rotation
- Flipping
- Brightness/contrast
- Noise injection

---

## 3.4 Model Training (การฝึกโมเดล)

### 🇹🇭
ใช้ Deep Learning เช่น:
- CNN
- ResNet / EfficientNet

Loss Function:
- CrossEntropy Loss

### 🇬🇧
Use deep learning models:
- CNN / ResNet / EfficientNet

Loss:
- CrossEntropy Loss

---

## 3.5 Unknown Detection (การจัดการ Unknown)

### 🇹🇭 (สำคัญมาก 🔥)

วิธี:
1. **Threshold Softmax**
   - ถ้า confidence < threshold → Unknown
2. **Add Unknown Class**
   - train model ให้รู้จัก Unknown
3. **Out-of-Distribution Detection**

### 🇬🇧

Methods:
1. Softmax thresholding
2. Explicit unknown class training
3. Out-of-distribution detection

---

## 3.6 Evaluation (การประเมินผล)

### 🇹🇭
ใช้:
- **F1-score (macro)**

เหตุผล:
- class ไม่ balance
- ต้องการ fairness

### 🇬🇧
Metric:
- **Macro F1-score**

Reason:
- Handles class imbalance
- Treats all classes equally

---

# 🚀 4. Key Insights (สรุปแนวคิดสำคัญ)

## 🇹🇭
- ปัญหานี้ **ไม่ใช่แค่ classification ธรรมดา**
- ต้อง:
  - แยก Unknown
  - รับมือ domain shift
- Data สำคัญมากกว่าตัว model

## 🇬🇧
- This is **not just a classification task**
- Must:
  - Detect unknowns
  - Handle domain shift
- Data quality > model complexity

---

# ✅ Conclusion

## 🇹🇭
โจทย์นี้เป็นงานที่ท้าทายเพราะต้องจัดการ:
- ความไม่เหมือนของข้อมูล
- Unknown class
- Background noise

## 🇬🇧
This is a challenging task due to:
- Domain differences
- Unknown classes
- Background noise

---

