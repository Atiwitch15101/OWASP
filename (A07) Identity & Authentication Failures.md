# Identity & Authentication Failures

หมายถึงปัญหาที่เกิดขึ้นเมื่อระบบไม่สามารถยืนยันตัวตนของผู้ใช้ได้อย่างถูกต้องหรือไม่สามารถตรวจสอบสิทธิ์การเข้าถึงของผู้ใช้งานได้อย่างเหมาะสม ทำให้ผู้โจมตีสามารถปลอมแปลงตัวตนหรือเข้าถึงข้อมูลที่ไม่ควรเข้าถึงได้

## 1.Authentication Bypasses

Authentication Bypasses คือช่องโหว่ที่ทำให้ผู้โจมตีสามารถข้ามขั้นตอนการยืนยันตัวตนและเข้าถึงข้อมูลหรือฟังก์ชันที่ควรจะถูกป้องกันได้

  - **ตัวอย่าง**
  
    > การใช้ URL ที่ไม่ได้ป้องกันอย่างเหมาะสม เช่น /admin/dashboard ที่สามารถเข้าถึงได้โดยตรงโดยไม่ต้องยืนยันตัวตน
    
  - **ป้องกันอย่างไร**
    > - ใช้การตรวจสอบสิทธิ์ในทุกๆ หน้าของแอปพลิเคชัน
    > - ใช้การตรวจสอบสิทธิ์และการอนุญาตที่ถูกต้องสำหรับแต่ละบทบาทของผู้ใช้
    
___

# 2.Insecure Login

Insecure Login หมายถึงกระบวนการเข้าสู่ระบบที่ไม่ปลอดภัย ซึ่งสามารถทำให้ข้อมูลรับรองของผู้ใช้งานถูกขโมยได้

  - **ตัวอย่าง**
    > การส่งข้อมูลเข้าสู่ระบบผ่าน HTTP แทนที่จะใช้ HTTPS ซึ่งทำให้ข้อมูลสามารถถูกดักฟังได้ง่าย

  - **ป้องกันอย่างไร**
    > - ใช้การเข้ารหัส SSL/TLS ในการส่งข้อมูลที่สำคัญ
    > - ตรวจสอบให้แน่ใจว่าใช้ HTTPS ทุกครั้งที่มีการส่งข้อมูลที่สำคัญ

___

# 3.JWT Tokens

JSON Web Tokens (JWT) ใช้สำหรับการยืนยันตัวตนและส่งข้อมูลอย่างปลอดภัยระหว่างเซิร์ฟเวอร์และไคลเอนต์

  - **ตัวอย่าง**
    > การใช้ JWT โดยไม่มีการเข้ารหัสลับที่แข็งแรง ทำให้ผู้โจมตีสามารถแกะและเปลี่ยนแปลงข้อมูลใน JWT ได้
    
  - **ป้องกันอย่างไร**
    > - ใช้การเข้ารหัสลับที่แข็งแรงและการเซ็นชื่อที่ปลอดภัย
    > - ตั้งค่าให้ JWT หมดอายุในเวลาที่เหมาะสม
    > - ตรวจสอบความถูกต้องของ JWT ทุกครั้งที่ใช้

___

# 4.Password Reset

ช่องโหว่ในกระบวนการรีเซ็ตรหัสผ่านที่ทำให้ผู้โจมตีสามารถขโมยหรือเปลี่ยนรหัสผ่านของผู้ใช้งานได้

  - **ตัวอย่าง**
    > การส่งลิงก์รีเซ็ตรหัสผ่านที่ไม่ปลอดภัยหรือการใช้คำถามเพื่อความปลอดภัยที่ง่ายต่อการเดา
    
  - **ป้องกันอย่างไร**
    > - ใช้ลิงก์รีเซ็ตรหัสผ่านที่มีอายุการใช้งานจำกัด
    > - ใช้การยืนยันตัวตนเพิ่มเติม เช่น การส่งโค้ดยืนยันไปยังอีเมลหรือโทรศัพท์
    > - ใช้คำถามเพื่อความปลอดภัยที่แข็งแรงและไม่ง่ายต่อการคาดเดา

___

# 5.Secure Passwords

การจัดการรหัสผ่านที่ปลอดภัยเพื่อป้องกันการถูกเดาหรือแครก

  - **ตัวอย่าง**
    > การจัดการรหัสผ่านที่ปลอดภัยเพื่อป้องกันการถูกเดาหรือแครก
    
  - **ป้องกันอย่างไร**
    > - กำหนดนโยบายรหัสผ่านที่แข็งแรง เช่น การใช้ตัวอักษรพิเศษ ตัวเลข และอักษรใหญ่-เล็ก
    > - บังคับใช้การเปลี่ยนรหัสผ่านเป็นระยะ ๆ
    > - เก็บรหัสผ่านในรูปแบบที่เข้ารหัสลับและไม่เก็บในรูปแบบ Plaintext

___
