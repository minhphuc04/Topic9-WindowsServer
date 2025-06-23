# Topic 9 Windows Server
---
 Bước 1: Cài đặt Remmina
 sudo apt update
sudo apt install remmina remmina-plugin-rdp
Bước 2: Mở Remmina
remmina
Bước 3: Connect theo thông tin đã cấp
1. Mở port (ví dụ: port 80 - HTTP)
netsh advfirewall firewall add rule name="Allow Port 80" dir=in action=allow protocol=TCP localport=80
2. Cho phép IP cụ thể truy cập port
netsh advfirewall firewall add rule name="Allow IP" dir=in action=allow remoteip=192.168.1.100 protocol=TCP localport=80
3. Chặn port cụ thể (ví dụ: port 21 - FTP)
netsh advfirewall firewall add rule name="Block Port 21" dir=in action=block protocol=TCP localport=21
4. Chặn IP cụ thể (ví dụ: 192.168.1.101)
netsh advfirewall firewall add rule name="Block IP" dir=in action=block remoteip=192.168.1.101
5. Giới hạn truy cập từ một IP duy nhất (ví dụ: cho phép IP hiện tại tôi dùng)
netsh advfirewall firewall set rule name="Allow Port 3389" new remoteip=222.255.214.39
6. Kiểm tra lại các rule đã tạo
netsh advfirewall firewall show rule name=all | findstr "Allow"
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
## Cài đặt SQL Server 2016 
1. Tải từ link https://software.vietnix.tech/datastore/sources/SQL_Server/sql2016/
2. Mount file ISO
Click chuột phải vào file en_sql_server_2016...iso → chọn Mount
4. Chạy file cài đặt
Vào ổ đĩa mới vừa được Mount ra → chạy setup.exe
5. Chọn tab Installation
6. Chọn dòng đầu tiên:
New SQL Server stand-alone installation or add features to an existing installation
Sau đó làm theo các bước sau:
| Bước | Mục                           | Hành động                                                               |
| ---- | ----------------------------- | ----------------------------------------------------------------------- |
| 1️⃣  | Product Key                   | Chọn Evaluation hoặc để mặc định nếu không có key                       |
| 2️⃣  | License Terms                 | Tick "I accept" → Next                                                  |
| 3️⃣  | Microsoft Updates             | Giữ mặc định hoặc bỏ tick → Next                                        |
| 4️⃣  | Install Setup Files           | Chờ kiểm tra xong → Next                                                |
| 5️⃣  | Feature Selection             | Tick: ✅ **Database Engine Services** + **Client Tools Connectivity**    |
| 6️⃣  | Instance Configuration        | Chọn: **Default Instance** → Next                                       |
| 7️⃣  | Server Configuration          | Giữ nguyên → Next                                                       |
| 8️⃣  | Database Engine Configuration | Chọn **Mixed Mode**, nhập mật khẩu cho `sa` + nhấn **Add Current User** |
| 9️⃣  | Ready to Install              | Kiểm tra lại rồi nhấn **Install**                                       |
## Cài đặt MySQL
1. Cài từ trang chính
Link: https://dev.mysql.com/downloads/mysql/
Cài bản MSI Installer (64-bit)
Trong quá trình cài:
    Chọn Developer Default
    Thiết lập mật khẩu cho user root
2. Cài đặt MySQL
Chạy file cài đặt → làm theo hướng dẫn sau:
| Bước                         | Hành động                                                         |
| ---------------------------- | ----------------------------------------------------------------- |
| **1. Setup Type**            | Chọn **Developer Default** (bao gồm server, workbench, tools...)  |
| **2. Check Requirements**    | Nếu thiếu Visual C++ → cài thêm, rồi nhấn Next lại                |
| **3. Installation**          | Nhấn **Execute** để bắt đầu cài các thành phần                    |
| **4. Product Configuration** | Chọn cấu hình mặc định → nhấn **Next**                            |
| **5. Authentication Mode**   | Chọn **Use Legacy Authentication Method** *(tương thích với PHP)* |
| **6. Tạo user**              | Tạo mật khẩu cho tài khoản `root`, ghi nhớ lại!                   |
| **7. Services**              | Giữ mặc định: MySQL chạy như dịch vụ Windows → **Next**           |
| **8. Apply Configuration**   | Nhấn **Execute** → chờ hoàn tất                                   |
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
3. Thêm PHP vào PATH
## Cài mã nguồn WordPress
1. Tải bản mới nhất tại: https://wordpress.org/latest.zip
2. Giải nén WordPress

    Nhấn chuột phải vào wordpress-6.8.1.zip → Chọn Extract All...

    Giải nén vào thư mục:

    C:\inetpub\wwwroot\wordpress

    (Tạo thư mục wordpress nếu chưa có)

    📌 Nếu thư mục C:\inetpub\wwwroot không tồn tại → IIS chưa được cài hoàn chỉnh → Cần kiểm tra lại trong Server Manager.
3. Cấp quyền thư mục

    Chuột phải vào C:\inetpub\wwwroot\wordpress

    Chọn Properties → Tab Security

    Nhấn Edit → Add

        Gõ IUSR, bấm OK

        Gõ IIS_IUSRS, bấm OK

    Cấp quyền Read & Execute + Modify
4. Tạo website trong IIS
4.1. Mở IIS Manager

4.2. Chuột phải vào Sites → Add Website

    Site name: wordpress

    Physical path: C:\inetpub\wwwroot\wordpress

Nhấn OK

   
