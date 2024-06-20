# Identity & Authentication Failures

หมายถึงปัญหาที่เกิดขึ้นเมื่อระบบไม่สามารถยืนยันตัวตนของผู้ใช้ได้อย่างถูกต้องหรือไม่สามารถตรวจสอบสิทธิ์การเข้าถึงของผู้ใช้งานได้อย่างเหมาะสม ทำให้ผู้โจมตีสามารถปลอมแปลงตัวตนหรือเข้าถึงข้อมูลที่ไม่ควรเข้าถึงได้

## 1.Authentication Bypasses

Authentication Bypasses คือช่องโหว่ที่ทำให้ผู้โจมตีสามารถข้ามขั้นตอนการยืนยันตัวตนและเข้าถึงข้อมูลหรือฟังก์ชันที่ควรจะถูกป้องกันได้

  ### ตัวอย่าง
  > การใช้ URL ที่ไม่ได้ป้องกันอย่างเหมาะสม เช่น /admin/dashboard ที่สามารถเข้าถึงได้โดยตรงโดยไม่ต้องยืนยันตัวตน
    
  ### ป้องกันอย่างไร
  
    > - ใช้การตรวจสอบสิทธิ์ในทุกๆ หน้าของแอปพลิเคชัน
    > - ใช้การตรวจสอบสิทธิ์และการอนุญาตที่ถูกต้องสำหรับแต่ละบทบาทของผู้ใช้
    
___

# 2.Insecure Direct Object References (IDOR)

การอ้างอิงวัตถุโดยไม่ปลอดภัย (Insecure Direct Object References) สิ่งนี้เกิดขึ้นเมื่อระบบไม่ตรวจสอบสิทธิ์การเข้าถึงข้อมูลโดยตรง ทำให้ผู้ใช้สามารถเข้าถึงข้อมูลที่ไม่ควรได้เช่นข้อมูลของผู้อื่นหรือข้อมูลที่มีความลับ

  - **ตัวอย่าง**
    > สมมติว่าคุณสามารถเข้าถึงโปรไฟล์ของคุณเองได้ผ่าน URL เช่น https://example.com/user?id=123 ถ้าผู้โจมตีเปลี่ยนเลข ID ใน URL เป็น https://example.com/user?id=124 แล้วสามารถเข้าถึงข้อมูลของผู้ใช้คนอื่นได้

  - **ป้องกันอย่างไร**
    > ตรวจสอบสิทธิ์ของผู้ใช้ทุกครั้งที่มีการเข้าถึงข้อมูลหรือวัตถุโดยตรง และไม่ควรใช้อ้างอิงโดยตรงใน URL

___

# 3.Missing Function Level Access Control:

การควบคุมการเข้าถึงฟังก์ชันที่ขาดหายไป (Missing Function Level Access Control) นี่เกิดขึ้นเมื่อระบบไม่มีการตรวจสอบสิทธิ์ของผู้ใช้เมื่อมีการเรียกใช้งานฟังก์ชันหรือการกระทำที่ต้องการสิทธิ์พิเศษ ทำให้ผู้ไม่ประสงค์ดีสามารถเข้าถึงฟังก์ชันนั้นได้โดยไม่ได้รับอนุญาต

  - **ตัวอย่าง**
    >สมมติว่ามีฟังก์ชันที่เฉพาะผู้ดูแลระบบเท่านั้นที่ควรเข้าถึงได้ เช่น การลบผู้ใช้ แต่ผู้ใช้ทั่วไปสามารถเข้าถึง URL ของฟังก์ชันนี้ได้และทำการลบผู้ใช้อื่น ๆ
    
  - **ป้องกันอย่างไร**
    > กำหนดการตรวจสอบสิทธิ์ในทุกฟังก์ชันที่มีความสำคัญ และตรวจสอบสิทธิ์ของผู้ใช้ก่อนการเข้าถึงฟังก์ชันนั้น ๆ

___

# 4.Spoofing an Authentication Cookie:

การปลอมแปลงคุกกี้การตรวจสอบและรับรองตัวตน (Spoofing an Authentication Cookie) สิ่งนี้เกิดขึ้นเมื่อผู้ไม่ประสงค์ดีสร้างคุกกี้การตรวจสอบและรับรองตัวตนปลอมแปลงเพื่อให้ระบบคิดว่าเป็นผู้ใช้ที่ถูกต้องและให้สิทธิ์เข้าถึงที่ไม่เหมาะสม

  - **ตัวอย่าง**
    > ผู้โจมตีสามารถสร้างหรือแก้ไขคุกกี้ที่เก็บข้อมูลการยืนยันตัวตนเพื่อทำให้ระบบเชื่อว่าผู้โจมตีเป็นผู้ใช้ที่มีสิทธิ์สูงกว่า เช่น ผู้ดูแลระบบ
    
  - **ป้องกันอย่างไร**
    > ใช้การเข้ารหัสคุกกี้และตรวจสอบความถูกต้องของคุกกี้อย่างสม่ำเสมอ เช่น การใช้ HMAC (Hash-based Message Authentication Code)

___