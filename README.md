# Topic 9 Windows Server
---
 Bước 1: Cài đặt Remmina
 sudo apt update
sudo apt install remmina remmina-plugin-rdp
Bước 2: Mở Remmina
remmina
Bước 3: Connect theo thông tin đã cấp
1. Mở port (ví dụ: port 80 - HTTP)
```
netsh advfirewall firewall add rule name="Allow Port 80" dir=in action=allow protocol=TCP localport=80
```
2. Cho phép IP cụ thể truy cập port
```
netsh advfirewall firewall add rule name="Allow IP" dir=in action=allow remoteip=192.168.1.100 protocol=TCP localport=80
```
3. Chặn port cụ thể (ví dụ: port 21 - FTP)
```
netsh advfirewall firewall add rule name="Block Port 21" dir=in action=block protocol=TCP localport=21
```
4. Chặn IP cụ thể (ví dụ: 192.168.1.101)
```
netsh advfirewall firewall add rule name="Block IP" dir=in action=block remoteip=192.168.1.101
```
5. Giới hạn truy cập từ một IP duy nhất (ví dụ: cho phép IP hiện tại tôi dùng)
```
netsh advfirewall firewall set rule name="Allow Port 3389" new remoteip=222.255.214.39
```
6. Kiểm tra lại các rule đã tạo
```
netsh advfirewall firewall show rule name=all | findstr "Allow"
```
## Cài đặt IIS Webserver
1. Mở Server Manager
2. Chọn: Manage → Add Roles and Features

Thực hiện các bước sau:

    Role-based or feature-based installation → Next

    Chọn server mặc định đang hiển thị → Next

    Tick chọn: Web Server (IIS)
    Khi popup hiện ra → Nhấn Add Features → rồi nhấn Next

    Tiếp tục nhấn Next cho đến khi thấy nút Install → Nhấn Install
3. Sau khi cài xong vào Server Manager nhấn vào Tools chọn "Internet Information Servics (IIS) Manager"
# Hướng dẫn cài đặt SQL Server 2016 & MySQL

##  Cài đặt SQL Server 2016

### 1. Tải về
- Link: [SQL Server 2016 ISO](https://software.vietnix.tech/datastore/sources/SQL_Server/sql2016/)

### 2. Mount file ISO
- Nhấn chuột phải vào file `en_sql_server_2016...iso` → chọn **Mount**

### 3. Chạy cài đặt
- Mở ổ đĩa mới vừa được mount → chạy `setup.exe`

### 4. Cài đặt
- Chọn tab **Installation**
- Nhấn vào dòng đầu tiên:
New SQL Server stand-alone installation or add features to an existing installation

### 5. Làm theo hướng dẫn sau:

| Bước | Mục                           | Hành động                                                               |
| ---- | ----------------------------- | ----------------------------------------------------------------------- |
| 1️⃣  | Product Key                   | Chọn **Evaluation** hoặc để mặc định nếu không có key                   |
| 2️⃣  | License Terms                 | Tick **"I accept"** → **Next**                                          |
| 3️⃣  | Microsoft Updates             | Giữ mặc định hoặc bỏ tick → **Next**                                    |
| 4️⃣  | Install Setup Files           | Chờ kiểm tra xong → **Next**                                            |
| 5️⃣  | Feature Selection             | Tick: ✅ **Database Engine Services** + **Client Tools Connectivity**    |
| 6️⃣  | Instance Configuration        | Chọn: **Default Instance** → **Next**                                   |
| 7️⃣  | Server Configuration          | Giữ nguyên → **Next**                                                   |
| 8️⃣  | Database Engine Configuration | Chọn **Mixed Mode**, nhập mật khẩu cho `sa` + nhấn **Add Current User** |
| 9️⃣  | Ready to Install              | Kiểm tra lại → nhấn **Install**                                         |

---

##  Cài đặt MySQL

### 1. Tải về
- Truy cập trang chính thức: [MySQL Downloads](https://dev.mysql.com/downloads/mysql/)
- Chọn bản: **Windows (x86, 64-bit), MSI Installer**

### 2. Cài đặt
- Chạy file `.msi` → làm theo hướng dẫn sau:

| Bước                         | Hành động                                                         |
| ---------------------------- | ----------------------------------------------------------------- |
| **1. Setup Type**            | Chọn **Developer Default** (gồm server, workbench, tools...)      |
| **2. Check Requirements**    | Nếu thiếu Visual C++ → cài thêm rồi nhấn **Next** lại             |
| **3. Installation**          | Nhấn **Execute** để bắt đầu cài các thành phần                    |
| **4. Product Configuration** | Giữ cấu hình mặc định → nhấn **Next**                             |
| **5. Authentication Mode**   | Chọn **Use Legacy Authentication Method** *(tương thích với PHP)* |
| **6. Tạo user**              | Đặt mật khẩu cho tài khoản `root`, **ghi nhớ lại!**               |
| **7. Services**              | Giữ mặc định: MySQL chạy như dịch vụ Windows → **Next**           |
| **8. Apply Configuration**   | Nhấn **Execute** → chờ hoàn tất                                   |

---

3.  MySQL Configuration Wizard
 3.1. Type and Networking

    Chọn: Standalone MySQL Server / Development Machine

    Port: để mặc định 3306 → Next

🔹 3.2. Authentication Method

    Chọn: ✅ Use Legacy Authentication Method
    (rất quan trọng để WordPress/PHP kết nối)
    → Next

🔹 3.3. Accounts and Roles

    Nhập mật khẩu cho user root

        ⚠️ Ghi nhớ mật khẩu này — bạn sẽ dùng trong bước cài WordPress sau.

→ Next
🔹 3.4. Windows Service

    Để mặc định:

        Tên dịch vụ: MySQL93

        ✅ “Start the server at system startup” → Next

🔹 3.5. Apply Configuration

    Nhấn Execute → chờ hoàn tất

    Nếu mọi thứ đều hiện ✔️, nhấn Finish
![image](https://github.com/user-attachments/assets/bb9109fc-5921-4436-90ef-b056217acddd)
## Cài đặt PHP
1. Truy cập đường dẫn sau để tải tool:
https://www.microsoft.com/web/downloads/platform.aspx
2. Giải nén
3. Thêm biến môi trường PHP vào PATH
## Cài mã nguồn WordPress
1. Tải bản mới nhất tại: https://wordpress.org/latest.zip
2. Giải nén WordPress

    Nhấn chuột phải vào wordpress-6.8.1.zip → Chọn Extract All...

    Giải nén vào thư mục:
```
    C:\inetpub\wwwroot\wordpress
```

3. Cấp quyền thư mục

    Chuột phải vào C:\inetpub\wwwroot\wordpress

    Chọn Properties → Tab Security

    Nhấn Edit → Add

        Gõ IUSR, bấm OK

        Gõ IIS_IUSRS, bấm OK

    Cấp quyền Read & Execute + Modify
4. Tạo website trong IIS
 
     4.1. Trước tiên truy cập vào C:\Windows\System32\drivers\etc\hosts thêm
     ```
     222.255.214.39    mphuc.wp.vietnix.tech
     ```
     ![image](https://github.com/user-attachments/assets/01e0368f-6f9b-47f0-b554-98c5f495a9bd)

     4.2. Mở IIS Manager
     
     4.3. Chuột phải vào Sites → Add Website
     
         Site name: dùng Default Web Site
     
         Physical path: C:\inetpub\wwwroot\wordpress
     Nhấn OK
     
     ---
     4.4. Thêm index.php vào Default Document
     
     4.5. Restart lại Web trong IIS
     
     4.6. Truy cập web với http://mphuc.wp.vietnix.tech/wp-admin/)
     
     4.7. Config wordpress connect đến database 
     ![image](https://github.com/user-attachments/assets/ab9b2409-8766-4dc2-b46b-456ae83a5ba4)
     
     4.8 Nhấn vào "Run the installation" để tiếp tục cài đặt.
     ![image](https://github.com/user-attachments/assets/bb00089d-25b8-475c-9de0-3b2e25b0c53c)
     
     4.9. Điền thông tin cho website của bạn
     ![image](https://github.com/user-attachments/assets/69deefb6-c0b4-4799-96df-69a4763af152)
     
     4.10. Login vào tài khoản vừa thiết lập
     min![image](https://github.com/user-attachments/assets/2b222048-9d85-4a0c-8763-bac8ffcd11b5)
     
     4.11. Hoàn tất Website
     ![image](https://github.com/user-attachments/assets/9c7cf0b9-b5f6-4098-b373-5a3f17d812c7)


## Cài SSL cho Website
 Gán chứng chỉ ZeroSSL cho trang WordPress trên IIS
1. Truy cập vào Linux tạo SSL từ 3 file crt có sẵn từ ZeroSSL
```
openssl pkcs12 -export \
  -inkey /home/minhphuc/Desktop/cert/mphuc.wp.vietnix.tech/private.key \
  -in /home/minhphuc/Desktop/cert/mphuc.wp.vietnix.tech/certificate.crt \
  -certfile /home/minhphuc/Desktop/cert/mphuc.wp.vietnix.tech/ca_bundle.crt \
  -out /home/minhphuc/Desktop/cert/mphuc.wp.vietnix.tech/mphuc.wp.vietnix.tech.pfx \
  -passout pass:123456 \
  -legacy
```
2. Duy chuyển file mphuc.wp.vietnix.tech.pfx vừa tạo sang Windows Server
3. Mở IIS Manager --> chọn Server Certificates
![image](https://github.com/user-attachments/assets/cb728c1b-bdff-4dcd-8302-a4faa34d8e50)
4. Chọn import
![image](https://github.com/user-attachments/assets/e4e0dda1-dd11-410f-afb3-954136e14ab2)
5. Chọn đường dẫn đến chứng chỉ mphuc.wp.vietnix.tech.pfx sau đó nhập password khi tạo file
![image](https://github.com/user-attachments/assets/11e81a68-5223-4c97-80ed-a02639c044bd)
6. Import ZeroSSL thành công
7. Quay về  IIS Manager chọn Bindings chọn SSL Certificate vừa tạo
![image](https://github.com/user-attachments/assets/2ef1a80c-6243-4add-9d75-5f0821da32d6)
8. Hoàn tất.

### Kết quả khi Import ZeroSSL cho domain mphuc.wp.vietnix.tech
![image](https://github.com/user-attachments/assets/d6b85258-280a-4886-b9dd-1df818bd8823)




