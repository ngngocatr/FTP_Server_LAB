# DỰNG FTP-SERVER ĐỂ LƯU TRỮ FILE
## 1. SETUP
### 1. Cấu hình IP tĩnh cho FTP Server
Thiết lập trong `Control Panel`
<img src="./images/2026-03-12-17-30-05.png" style="display: block; margin: 0 auto;">

<img src="./images/2026-03-12-17-44-51.png" style="display: block; margin: 0 auto;">

<br>
<img src="./images/2026-03-12-17-44-55.png" style="display: block; margin: 0 auto;">

<br>
<img src="./images/2026-03-12-17-46-24.png" style="display: block; margin: 0 auto;">

Tích chọn `Use the following IP address`\
Thiết lập các trường `IP address`, `Subnet mask`, `Default Gateway`\
Nhấn `OK` để hoàn tất thiết lập IP

<img src="./images/2026-03-12-17-50-26.png" style="display: block; margin: 0 auto;">

Dùng `ipconfig` ta thấy máy đã có IP `192.168.30.15`


### 2. Thiết lập `IIS` cho FTP
<img src="./images/2026-03-13-21-16-53.png" style="display: block; margin: 0 auto;">

Vào `Server Manager` --> `Add roless and features`

<img src="./images/2026-03-13-21-17-56.png" style="display: block; margin: 0 auto;">
<br>
<img src="./images/2026-03-13-21-25-10.png" style="display: block; margin: 0 auto;">
<br>
<img src="./images/2026-03-13-21-26-27.png" style="display: block; margin: 0 auto;">
<br>
<img src="./images/2026-03-13-21-31-23.png" style="display: block; margin: 0 auto;">

<br>
<img src="./images/2026-03-14-09-21-37.png" style="display: block; margin: 0 auto;">

Sau khi cài đặt xong sẽ xuất hiện 1 ô có tên `IIS`

<img src="./images/2026-03-14-09-24-42.png" style="display: block; margin: 0 auto;">

Vào `Internet Information Services (IIS) Manager` ta sẽ thấy được cấu hình như trên

<img src="./images/2026-03-14-09-28-05.png" style="display: block; margin: 0 auto;">

Tạo 1 folder để chứa dữ liệu của FTP Server

<img src="./images/2026-03-14-09-26-29.png" style="display: block; margin: 0 auto;">

Chuột phải vào `Site` chọn `Add FTP Site`

<img src="./images/2026-03-14-09-29-13.png" style="display: block; margin: 0 auto;">

Nhập `Site Name` và đường dẫn lưu trữ data 

<img src="./images/2026-03-14-09-30-21.png" style="display: block; margin: 0 auto;">

Chọn IP dùng để truy cập\
Do lab cơ bản nên ta không cần mã hóa dữ liệu --> chọn `No SSL`

<img src="./images/2026-03-14-09-31-40.png" style="display: block; margin: 0 auto;">

Phần này cho phép truy cập bằng tài khoản nào và IP nào\
Ta cho phép cả *tài khoản người dùng thông thường*(`Basic`) và *tài khoản khách*(`Anonymous`)

<img src="./images/2026-03-14-09-37-30.png" style="display: block; margin: 0 auto;">

Kiểm tra thử ta đã thấy mạng được thông giữa các máy

## 2. Thao tác Client và Server
### 1. Win 10
**1. GUI (File Explorer)**
<img src="./images/2026-03-14-10-23-50.png" style="display: block; margin: 0 auto;">

Lệnh để truy cập ftp thông qua `File Explorer`:

`ftp://user:password0@IP`

--> `ftp://Administrator:Password123%40@192.168.30.15`

<img src="./images/2026-03-14-10-24-22.png" style="display: block; margin: 0 auto;">

Sau khi truy cập ta có thể thao tác với file dưới quyền của tài khoản `Administrator`

<img src="./images/2026-03-14-10-26-09.png" style="display: block; margin: 0 auto;">

Ta có thể coppy, delete, add file/folder 


**2. CLI (CMD)**
<img src="./images/2026-03-14-10-30-15.png" style="display: block; margin: 0 auto;">

Cú pháp trên CMD:
`ftp IP_address`

--> `ftp 192.168.30.15`

Sau đó nó cho ta mìn hình chờ đăng nhập

<img src="./images/2026-03-14-10-32-13.png" style="display: block; margin: 0 auto;">

Ta có thể đăng nhập bằng lệnh: `USER username password`

<img src="./images/2026-03-14-10-32-47.png" style="display: block; margin: 0 auto;">

Sau khi đăng nhập, ta cũng có những thao tác tương tự như GUI với tài khoản `Administrator`

### 2. Linux
**Terminal**
<img src="./images/2026-03-14-10-45-24.png" style="display: block; margin: 0 auto;">

Tương tự như như `CMD` trên Windows, lệnh truy cập của Linux là:
`ftp IP_address`

--> `ftp 192.168.30.15`

Phương thức đăng nhập cũng tương tự như CLI của Window

**Thực hiện một số thao tác:**

*Xem cấu trúc thư mục*: `ls`

<img src="./images/2026-03-14-10-48-42.png" style="display: block; margin: 0 auto;">
<br>

*Di chuyển*: `cd`

<img src="./images/2026-03-14-10-49-36.png" style="display: block; margin: 0 auto;">
<br>

*Di chuyển trên máy cục bộ*: `lcd`

<img src="./images/2026-03-14-10-50-26.png" style="display: block; margin: 0 auto;">
<br>

*Coppy*: `get   [source_file_server] [des_folder_local]`\
*Coppy nhiều file*: `mget [file1] [file2] [des_folder_local]`\
Ví dụ muốn coppy file `test.txt` vào thư mục `/home`:

`get test.txt /home`

<img src="./images/2026-03-14-10-54-12.png" style="display: block; margin: 0 auto;">
<br>

*Upload file*: `put [local_file] [server_file_path]`

<img src="./images/2026-03-14-11-03-08.png" style="display: block; margin: 0 auto;">
<br>

*Delete file*: `delete [server_file_path]`

<img src="./images/2026-03-14-11-06-25.png" style="display: block; margin: 0 auto;">



