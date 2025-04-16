# I. CÀI ĐẶT VÀ CẤU HÌNH OWNCLOUD TRÊN VPS SOTRAGE


### 1. ownCloud là gì?

ownCloud là ứng dụng web lưu trữ tệp, đồng bộ tệp và cộng tác nội dung nguồn mở cho phép người dùng lưu trữ và chia sẻ nội dung cá nhân trên máy chủ riêng. Khả năng tương thích đa nền tảng của ownCloud cho phép bạn truy cập tệp ở bất kỳ đâu và vì ứng dụng này chạy trên máy chủ riêng của bạn nên không cần sử dụng dịch vụ lưu trữ đám mây của bên thứ ba.

Tương tự như các dịch vụ lưu trữ đám mây như Dropbox, Google Drive, One Drive cùng nhiều dịch vụ khác, ownCloud cho phép bạn lưu trữ tệp và chia sẻ chúng với bất kỳ ai trên Internet.

*Kính chào quý khách,*

Sau đây sẽ là hướng dẫn cài đặt và cấu hình ownCloud trên máy chủ ảo Cloud VPS. Quý khách vui lòng thực hiện theo các bước sau:

### Bước 1: Cài đặt MySQL trên Ubuntu

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/001.png?raw=true" alt="Demo Image" width="800"/>
</div>

### Bước 2: Tạo cơ sở dữ liệu MySQL

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/002.png?raw=true" alt="Demo Image" width="800"/>
</div>


ownCloud yêu cầu cơ sở dữ liệu MySQL. Để tạo cơ sở dữ liệu, hãy đăng nhập vào bảng điều khiển MySQL, bằng lệnh *mysql -u root -p*

Nhập mật khẩu root MySQL mà bạn đã tạo trước đó khi được yêu cầu. Sau khi đăng nhập, quý khách hãy làm theo các bước sau:

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/003.png?raw=true" alt="Demo Image" width="800"/>
</div>

**1. Tạo cơ sở dữ liệu mới cho ownCloud**
**2. Tạo người dùng cơ sở dữ liệu mới và gán mật khẩu**
**3. Cấp cho người dùng mới toàn quyền đối với cơ sở dữ liệu ownCloud**
**4. Làm mới quyền của người dùng MySQL**
**5. Thoát**

## Bước 3: Cài đặt PHP 

Quý cần cài đặt PHP cùng với tất cả các module cần thiết mà ownCloud yêu cầu. Quý khách có thể sử dụng câu lệnh 
*apt install php7.4 php7.4-cli php7.4-common php7.4-curl php7.4-gd php7.4-mysql php7.4-xml php7.4-zip php7.4-mbstring php7.4-bcmath php7.4-intl php7.4-imagick php7.4-apcu php7.4-redis php7.4-soap libapache2-mod-php7.4 -y*

Ở hướng dẫn này là cài đặt **PHP 7.4**.

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/004.png?raw=true" alt="Demo Image" width="800"/>
</div>

### Bước 4: Cào đặt Owncloud

Quý khách phải vào trang chủ của ownCloud (https://owncloud.com/) sau đó chọn vào *Download Server* và copy đường dẫn.

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/005.png?raw=true" alt="Demo Image" width="800"/>
</div>

Với phần mềm máy chủ web, máy chủ cơ sở dữ liệu và tiện ích mở rộng PHP được cài đặt trên máy chủ của quý khách, Owncloud hiện có thể chạy mà không gặp bất kỳ khó khăn nào. Để bắt đầu cài đặt thông qua trình duyệt web, quý khách phải tải xuống phiên bản mới nhất của Owncloud bằng wget trên máy chủ Ubuntu của mình.

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/006.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Sau khi tải về, di chuyển tệp quý khách đã tải xuống tới */var/www/html*

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/007.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Sau đó *cd /var/www/html/* và dùng lệnh *ls* để xác nhận sự tồn tại của tập tin đã di chuyển.

- Cài đặt *unzip* để hỗ trợ giải nén tệp

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/008.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Quý khách chạy lệnh *sudo unzip **tên tệp vừa tải xuống*** để giải nén tệp.

- Tiếp theo, quý khách cấp cho Apache quyền đọc và ghi vào thư mục mới bằng lệnh *sudo chown -R www-data:www-data owncloud/*

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/009.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Tiếp theo chỉnh sửa tệp cấu hình máy chủ ảo Apache mặc định 000-default.confvà tạo **/var/www/html/owncloud/** thư mục gốc cho tên miền của bạn. Thay thế *cloud.example.com* bằng tên miền thực tế của quý khách.
Quý khách chạy lệnh **sudo nano /etc/apache2/sites-available/000-default.conf** để chỉnh sửa.

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/010.png?raw=true" alt="Demo Image" width="800"/>
</div>

**1. Thay đổi bằng tên miền thực tế của quý khách**
**2. Chọn thư mục gốc**

- Sau đó, quý khách lưu và đóng tệp.

- Khởi động lại Apche để những thay đổi có hiệu lực.
<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/011.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Tiếp theo, hãy mở trình duyệt web trên máy tính cá nhân và nhập tên miền đã đăng ký hoặc chỉ cần nhập địa chỉ IP công khai của máy chủ vào thanh URL.

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/012.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Sau đó quý khách đăng ký tài khoản admin
   - **Database user:** Quý khách đăng nhập bằng user đã tạo khi tạo người dùng cơ sở dữ liệu
   - **Database password:** Quý khách đăng nhập bằng password đã tạo khi tạo người dùng cơ sở dữ liệu
   - **Database name:** Quý khách nhập tên cơ sở dữ liệu đã tạo ở trên
- Sau đó quý khách chọn *Finish setup* để kết thúc.

- Sau khi setup sẽ xuất hiện giao diện login. Quý khách hãy đăng nhập tài khoản vừa tạo

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/014.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Sau khi đăng nhập, quý khách đã cài đặt thành công ownCloud trên ubuntu
  
<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/015.png?raw=true" alt="Demo Image" width="800"/>
</div>

--------

# II. Hướng dẫn add disk HDD vào Storage của ownCloud

Theo dõi bài viết (https://wiki.vndata.vn/cloud-vps/huong-dan-chung/vps-stor/) để **add thêm disk HDD vào VPS Storage** và **Mount Disk HDD bên trong OS Linux**

*** Bước 1: Kiểm tra quyền truy cập thư mục

Để phân quyền cho *web server* có quyền truy cập vào thư mục /mnt/*tên thư mục đã mount*, quý khách sử dụng 2 lệnh:

*sudo chown -R www-data:www-data /mnt/data*
*sudo chmod -R 755 /mnt/data*

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/016.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Sau khi cấp quyền, quý khách kiểm tra bằng lệnh *ls -ld /mnt/data*
  

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/017.png?raw=true" alt="Demo Image" width="800"/>
</div>

*** Bước 2: Cho phép sử dụng ổ đĩa local
- Quý khách mở file cấu hình *sudo nano /var/www/html/owncloud/config/config.php*
- Thêm dòng sau vào file cấu hình *'files_external_allow_create_new_local' => true,* để thêm Local vào danh sách **allowed external storage types**.

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/018.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Sau đó lưu file và khởi động lại Apache bằng lệnh: *sudo systemctl restart apache2*

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/019.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Sau đó quý khách truy cập vào trình duyệt ownCloud của quý khách và chọn *Setting* và làm theo hướng dẫn:

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/020.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Ở phần **External storage** chọn **Local*
- Sau đó nhập đường dẫn thư mục được mount vào **Configuration**

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/021.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Quý khách đã hoàn thành việc *add disk HDD vào Storage của ownCloud*

- Để kiểm tra quý khách thực hiển theo các bước sau:
  
- Quý khách quay lại giao diện chính của ownCloud và chọn file *Local*
<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/022.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Quý khách chọn *upload* để upload file vào **Local**

 <div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/023.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Sau khi upload xong quý khách vào console của VPS dùng lệnh *ls -l /mnt/*thư mục được mount** để kiểm tra

 <div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/024.png?raw=true" alt="Demo Image" width="800"/>
</div>

  
  
