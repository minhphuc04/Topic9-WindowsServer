#Topic 9 Windows Server
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
