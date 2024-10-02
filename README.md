# ประเภทของ Load Balancing (Algorithms)
Nginx รองรับหลายรูปแบบของการกระจายโหลด:

## 1. Round Robin (ค่าเริ่มต้น)
Round Robin เป็นการกระจายคำร้องขอไปยัง Backend Servers ทีละตัว โดยวนไปเรื่อย ๆ

```bash
upstream backend {
    server 192.168.1.101;
    server 192.168.1.102;
    server 192.168.1.103;
}
```

## 2. Least Connections
Nginx จะส่งคำร้องขอไปยังเซิร์ฟเวอร์ที่มีการเชื่อมต่อน้อยที่สุดในขณะนั้น
```bash
upstream backend {
    least_conn;
    server 192.168.1.101;
    server 192.168.1.102;
    server 192.168.1.103;
}
```

## 3. IP Hash
Nginx จะกระจายคำร้องขอตาม IP ของผู้ร้องขอ เพื่อให้คำร้องขอจาก IP เดียวกันไปที่เซิร์ฟเวอร์เดิมเสมอ (เหมาะสำหรับการทำ Session Sticky)
```bash
upstream backend {
    ip_hash;
    server 192.168.1.101;
    server 192.168.1.102;
    server 192.168.1.103;
}
```

## 4. Weighted Load Balancing
กำหนดน้ำหนัก (weight) เพื่อให้เซิร์ฟเวอร์ที่มีความสามารถสูงกว่ารับคำร้องขอมากขึ้น
```bash
upstream backend {
    server 192.168.1.101 weight=3;  # เซิร์ฟเวอร์นี้รับคำขอมากกว่า
    server 192.168.1.102 weight=1;
    server 192.168.1.103 weight=1;
}
```
