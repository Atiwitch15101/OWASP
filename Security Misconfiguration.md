# Security Misconfiguration

ecurity misconfiguration จะสอนให้เราเห็นถึงผลกระทบของการตั้งค่าระบบที่ไม่ถูกต้องหรือไม่เหมาะสม โดยจะมีตัวอย่างการโจมตีที่เกิดจากการตั้งค่าที่ผิดพลาด

  - การใช้ค่าตั้งต้นที่ไม่ปลอดภัย (default settings) เช่น การใช้รหัสผ่านที่ตั้งค่าไว้เริ่มต้น
  - การเปิดเผยข้อมูลที่ไม่จำเป็น เช่น ข้อความแสดงข้อผิดพลาดที่ให้ข้อมูลมากเกินไป
  - การไม่อัปเดตแพตช์ความปลอดภัย ทำให้ระบบมีช่องโหว่ที่เป็นที่รู้จักและสามารถถูกโจมตีได้

# XXE

ในหัวข้อย่อย XXE ของเรื่อง security misconfiguration บน WebGoat เราจะศึกษาเกี่ยวกับการโจมตีที่ใช้ XML External Entities เพื่อเข้าถึงข้อมูลที่ไม่ควรเข้าถึงหรือทำให้ระบบทำงานผิดปกติ โดยการโจมตีแบบ XXE เกิดขึ้นเมื่อแอปพลิเคชันที่ประมวลผล XML อนุญาตให้มีการอ้างอิงถึง external entities

  - **ตัวอย่างการโจมตี XXE**

  ```
  <?xml version="1.0" encoding="ISO-8859-1"?>
  <!DOCTYPE foo [
    <!ELEMENT foo ANY >
    <!ENTITY xxe SYSTEM "file:///etc/passwd" >]>
  <foo>&xxe;</foo>
  ```

  > ในตัวอย่างนี้ external entity xxe ถูกกำหนดให้ชี้ไปที่ไฟล์ /etc/passwd บนเซิร์ฟเวอร์ เมื่อ XML นี้ถูกประมวลผล แอปพลิเคชันจะอ่านเนื้อหาของไฟล์นั้นและแสดงผลออกมา

  - **วิธีการป้องกัน**
    1. ปิดการใช้งาน external entities: การตั้งค่า parser ของ XML ให้ไม่รองรับการใช้งาน external entities จะช่วยป้องกันการโจมตีนี้ได้

    ```
    DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
    dbf.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true);
    dbf.setFeature("http://xml.org/sax/features/external-general-entities", false);
    dbf.setFeature("http://xml.org/sax/features/external-parameter-entities", false);
    ```
    2. ใช้ parser ที่ปลอดภัย: เลือกใช้ XML parser ที่มีการรักษาความปลอดภัยในตัว เช่น SAXParser หรือ StAXParser ที่มีการตั้งค่าป้องกันการใช้งาน external entities

    3. ตรวจสอบและวิเคราะห์ XML: ตรวจสอบ XML input ที่รับเข้ามาอย่างรอบคอบ และใช้วิธีการ validate ข้อมูลที่รับเข้ามาเพื่อป้องกันการโจมตี

___
