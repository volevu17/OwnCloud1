# I. CÀI ĐẶT VÀ CẤU HÌNH OWNCLOUD TRÊN VPS SOTRAGE

*Kính chào Quý khách,*

Sau đây là hướng dẫn cài đặt và cấu hình ownCloud trên máy chủ ảo Cloud VPS. Quý khách vui lòng thực hiện theo từng bước như sau để đảm bảo quá trình cài đặt diễn ra thuận lợi.


### 1. ownCloud là gì?

ownCloud là ứng dụng web lưu trữ tệp, đồng bộ tệp và cộng tác nội dung nguồn mở cho phép người dùng lưu trữ và chia sẻ nội dung cá nhân trên máy chủ riêng. Khả năng tương thích đa nền tảng của ownCloud cho phép bạn truy cập tệp ở bất kỳ đâu và vì ứng dụng này chạy trên máy chủ riêng của bạn nên không cần sử dụng dịch vụ lưu trữ đám mây của bên thứ ba.

Tương tự như các dịch vụ lưu trữ đám mây như Dropbox, Google Drive, One Drive cùng nhiều dịch vụ khác, ownCloud cho phép bạn lưu trữ tệp và chia sẻ chúng với bất kỳ ai trên Internet.

### 2. Các bước cài đặt ownCloud trên Ubuntu VPS
  
  ### 2.1. Cài đặt môi trường 
  
ownCloud yêu cầu cơ sở dữ liệu MySQL và cài đặt PHP. 
### Bước 1: Cài đặt MySQL trên Ubuntu

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/001.png?raw=true" alt="Demo Image" width="800"/>
</div>

### Bước 2: Tạo cơ sở dữ liệu MySQL

Để tạo cơ sở dữ liệu, hãy đăng nhập vào bảng điều khiển MySQL, bằng lệnh *mysql -u root -p*

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/002.png?raw=true" alt="Demo Image" width="800"/>
</div>


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

Quý cần cài đặt PHP cùng với tất cả các module cần thiết mà ownCloud yêu cầu, ở hướng dẫn này là cài đặt **PHP 7.4**. 

Quý khách có thể sử dụng câu lệnh 

```bash
sudo apt install php7.4 php7.4-cli php7.4-common php7.4-curl php7.4-gd php7.4-mysql php7.4-xml php7.4-zip php7.4-mbstring php7.4-bcmath php7.4-intl php7.4-imagick php7.4-apcu php7.4-redis php7.4-soap libapache2-mod-php7.4 -y
```


<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/004.png?raw=true" alt="Demo Image" width="800"/>
</div>

### 2.2. Cài đặt ownCloud
   ### Bước 4: Cào đặt ownCloud

Quý khách phải vào trang chủ của ownCloud (https://owncloud.com/) sau đó đưa trỏ chuột vào **Download Server** và copy đường dẫn tải về phiên bản mới nhất.

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/005.png?raw=true" alt="Demo Image" width="800"/>
</div>

Trên máy chủ Ubuntu, sử dụng `wget` để tải ownCloud về máy:

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/006.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Sau khi tải về, di chuyển tệp quý khách đã tải xuống tới */var/www/html*

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/007.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Truy cập
```bash
  cd /var/www/html/
```
Và dùng lệnh *ls* để xác nhận sự tồn tại của tập tin đã di chuyển.

**Cài đặt công cụ giải nén và giải nén ownCloud**

- Cài đặt *unzip* để hỗ trợ giải nén tệp

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/008.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Quý khách chạy lệnh sau để giải nén tệp.

```bash
sudo unzip <tên tệp vừa tải xuống>
```

- Tiếp theo, quý khách Cấp quyền cho Apache truy cập thư mục ownCloud bằng lệnh:
```bash
  sudo chown -R www-data:www-data owncloud/
```
<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/009.png?raw=true" alt="Demo Image" width="800"/>
</div>

**Cấu hình Virtual Host cho ownCloud**

Chỉnh sửa file cấu hình mặc định của Apache bằng lệnh:
```bash
sudo nano /etc/apache2/sites-available/000-default.conf
```

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

### Bước 5: Truy cập giao diện cài đặt ownCloud
- Tiếp theo, quý khách hãy mở trình duyệt web trên máy tính cá nhân và nhập tên miền đã cấu hình hoặc địa chỉ IP công khai của máy chủ vào thanh địa chỉ trình duyệt (URL).

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/012.png?raw=true" alt="Demo Image" width="800"/>
</div>

Giao diện thiết lập ban đầu của ownCloud sẽ xuất hiện. Tại đây, quý khách vui lòng thực hiện các bước sau:
- **Tạo tài khoản quản trị viên (admin)** bằng cách nhập tên đăng nhập và mật khẩu mong muốn.
- Trong phần Thiết lập cơ sở dữ liệu, điền các thông tin như sau:
   - **Database user:** Tên người dùng cơ sở dữ liệu đã tạo ở bước trước.
   - **Database password:** Mật khẩu tương ứng với người dùng cơ sở dữ liệu.
   - **Database name:** Tên cơ sở dữ liệu đã được tạo.
- Sau khi hoàn tất, Quý khách nhấn vào nút Finish setup để hoàn tất quá trình cài đặt.

### Bước 6: Đăng nhập và hoàn tất cấu hình 

- Sau khi cài đặt hoàn tất, giao diện đăng nhập sẽ xuất hiện. Quý khách hãy đăng nhập bằng tài khoản quản trị viên vừa tạo ở bước trước.


<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/013.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Khi đăng nhập thành công, điều này đồng nghĩa với việc quý khách đã hoàn tất quá trình cài đặt ownCloud trên máy chủ Ubuntu.
--------

# II. Hướng dẫn thêm ổ đĩa HDD vào Storage của ownCloud

Vui lòng tham khảo bài viết sau để (https://wiki.vndata.vn/cloud-vps/huong-dan-chung/vps-stor/) để **add thêm disk HDD vào VPS Storage** và **Mount Disk HDD bên trong OS Linux**

 ### Bước 1: Kiểm tra quyền truy cập thư mục

Để đảm bảo web server (Apache) có thể truy cập được thư mục mount, quý khách hãy chạy các lệnh sau:

```bash
sudo chown -R www-data:www-data /mnt/data
```
```bash
sudo chmod -R 755 /mnt/data
```
<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/014.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Sau đó kiểm tra quyền truy cập thư mục bằng lệnh:
```bash
  ls -ld /mnt/data
  ```

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/015.png?raw=true" alt="Demo Image" width="800"/>
</div>

### Bước 2: Cho phép sử dụng ổ đĩa local
- Quý khách mở file cấu hình của ownCloud bằng lệnh
```bash
sudo nano /var/www/html/owncloud/config/config.php
```
- Thêm dòng sau vào file cấu hình
```bash
  'files_external_allow_create_new_local' => true,
```
Để thêm Local vào danh sách **allowed external storage types**.

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/016.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Sau đó lưu file và khởi động lại Apache bằng lệnh:

```bash
sudo systemctl restart apache2
```

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/017.png?raw=true" alt="Demo Image" width="800"/>
</div>

### Bước 3: Cấu hình ổ đĩa trong ownCloud

- Quý khách truy cập vào trình duyệt ownCloud của quý khách và chọn *Settings* và làm theo hướng dẫn:

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/018.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Trong phần **External storage** chọn **Local**
- Nhập đường dẫn đến thư mục đã mount ở phần **Configuration**

<div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/019.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Quý khách đã hoàn thành việc *add disk HDD vào Storage của ownCloud*

### Bước 4: Kiểm tra và sử dụng ổ đĩa
  
- Quý khách quay lại giao diện chính của ownCloud, chọn thư mục **Local**

- Quý khách click **Upload** để tải tệp lên thư mục **Local**

 <div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/020.png?raw=true" alt="Demo Image" width="800"/>
</div>

- Sau khi upload xong quý khách truy cập VPS qua terminal và chạy lệnh sau để xác minh tệp vừa upload:
```bash
  ls -l /mnt/data
```
 <div align="center">
  <img src="https://github.com/volevu17/OwnCloud1/blob/main/021.png?raw=true" alt="Demo Image" width="800"/>
</div>

  
  
