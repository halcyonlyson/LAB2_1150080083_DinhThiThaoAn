# LAB 2 – MÃ HÓA ĐỐI XỨNG HIỆN ĐẠI

**Họ và tên:** Đinh Thị Thảo An  
**MSSV:** 1150080083  
**Học phần:** An toàn và Bảo mật thông tin

## 1. Giới thiệu

Bài thực hành xây dựng chương trình mã hóa và giải mã dữ liệu bằng các thuật toán DES, TripleDES, AES, RC4 và Twofish, kết hợp Java Swing, Python và SQL Server. Chương trình có menu chính để truy cập các chức năng, kết nối cơ sở dữ liệu và xem lịch sử thao tác.

**Lưu ý:** DES, TripleDES và RC4 là các thuật toán lỗi thời, được triển khai trong LAB để học tập. AES-CTR và AES-CBC trong ví dụ chưa có cơ chế xác thực bản mã; không sử dụng các ví dụ này trực tiếp để bảo vệ dữ liệu thực tế.

## 2. Công nghệ sử dụng

- Java JDK 17
- Apache NetBeans IDE 31
- Java Swing và Maven
- Microsoft SQL Server và SQL Server Management Studio (SSMS)
- Python 3.13 và Tkinter
- Microsoft JDBC Driver và BouncyCastle
- Thư viện Python `cryptography`

## 3. Nội dung thực hành

| Bài | Nội dung | Công nghệ |
|---|---|---|
| 2.1 | DES – mã hóa và giải mã ở chế độ CBC | Java Swing |
| 2.2 | TripleDES – mã hóa và giải mã ở chế độ CBC | Java Swing |
| 2.3 | AES-GCM – đăng ký, đăng nhập, Ticket và lịch sử | Java Swing, SQL Server |
| 2.4 | RC4 – mã hóa dòng, bản mã HEX | Java Swing |
| 2.5 | Twofish-CBC – sinh IV, mã hóa, lưu/mở tệp | Java Swing, BouncyCastle |
| 2.6 – Bài nâng cao 01 | AES-256-CTR – sinh Key và Nonce | Java Swing |
| 2.6 – Bài nâng cao 02 | AES-256-CBC – giao diện Tkinter, tự kiểm thử | Python |

Menu chính `frm_Menu` cung cấp các nút mở sáu form thuật toán Java, form kết nối SQL Server và form xem lịch sử. Bài AES-CBC bằng Python được chạy riêng.

## 4. Hướng dẫn chạy

### 4.1. Chạy chương trình Java trong NetBeans

1. Mở Apache NetBeans IDE 31.
2. Chọn **File → Open Project** và mở thư mục `LAB2_MaHoaHienDai` (chứa `pom.xml`).
3. Đợi Maven tải đầy đủ các dependency khai báo trong `pom.xml`.
4. Nhấp phải project → **Clean and Build** (`Shift + F11`); kiểm tra thông báo `BUILD SUCCESS`.
5. Nhấp phải project → **Run** (`F6`). Main Class là `week_02.frm_Menu`.
6. Tại Menu chính, chọn bài thực hành cần mở.

### 4.2. Kết nối SQL Server

1. Khởi động SQL Server, bảo đảm dịch vụ đang hoạt động và TCP/IP đã được cấu hình.
2. Dùng SSMS chạy các script thiết lập cơ sở dữ liệu trong thư mục `SQL/` theo đúng thứ tự của tài liệu LAB 2, nếu máy chưa có cơ sở dữ liệu.
3. Cơ sở dữ liệu dùng trong bài: `LAB2_MaHoaHienDai`; địa chỉ kết nối thực hành: `127.0.0.1`, cổng `14333`.
4. Mở `frm_Menu` → **Kết nối SQL Server**; nhập tài khoản và mật khẩu SQL đã cấu hình trên máy, rồi chọn **Test Connection**.
5. Sau khi kết nối thành công, có thể mở **Xem lịch sử** để đọc dữ liệu trong `dbo.crypto_history`.

**Bảo mật:** Không commit mật khẩu SQL Server, thông tin kết nối chứa bí mật, khóa mã hóa thử nghiệm hay tệp cấu hình nhạy cảm lên GitHub. Nếu dùng tài khoản/mật khẩu mẫu trong hướng dẫn, chỉ sử dụng trong môi trường thực hành cục bộ.

### 4.3. Chạy chương trình Python AES-CBC

Mở Terminal/Command Prompt tại thư mục `Python/`, sau đó chạy:

```powershell
py --version
py -m pip install cryptography
py aes_cbc_gui.py --self-test
py aes_cbc_gui.py
```

- `--self-test`: chạy các trường hợp tự kiểm thử; kết quả mong muốn có dòng `SELF-TEST OK`.
- Lệnh cuối: mở giao diện Tkinter, sử dụng **Generate Key**, **Generate IV**, **Encrypt**, **Decrypt**, **Save File**, **Open File**.
- Khi mở tệp bản mã đã lưu, nhập lại đúng Key ban đầu để giải mã. Tệp chỉ lưu IV và bản mã, không lưu Key.

## 5. Kết quả thực hành và kiểm thử

Các chức năng đã được thực hiện và kiểm thử trong quá trình làm LAB:

| Chức năng | Nội dung kiểm thử | Kết quả ghi nhận |
|---|---|---|
| DES | Mã hóa/giải mã với khóa 8 byte | PASS |
| TripleDES | Mã hóa/giải mã với khóa 24 byte | PASS |
| AES-GCM | Đăng ký, đăng nhập, cấp Ticket, mã hóa/giải mã và kiểm tra bản mã bị sửa | PASS |
| RC4 | Plaintext `Plaintext`, Key `Key` → HEX `BBF316E8D940AF0AD3` | PASS |
| Twofish | Generate IV, Encrypt/Decrypt, Save/Open File | PASS |
| AES-CTR | Generate Key/Nonce, Encrypt/Decrypt, văn bản dài, Save/Open File | PASS |
| AES-CBC Python | Self-test, Encrypt/Decrypt và kiểm tra văn bản dài | PASS |
| Menu chính | Mở các form qua tám nút chức năng | PASS |
| Kiểm thử tích hợp SQL Server | Chạy project bằng F6, kết nối SQL Server, thực hiện lại các bài Java và xem lịch sử | PASS |

### 5.1. Kiểm thử tích hợp từ Menu chính (Bước 13 – trang 48)

1. Chạy project bằng **Run (`F6`)** để mở `frm_Menu`.
2. Mở **Kết nối SQL Server** và kiểm tra kết nối thành công.
3. Từ Menu, thực hiện ít nhất một thao tác mã hóa cho từng thuật toán Java: DES, TripleDES, AES, RC4, Twofish và AES-CTR. Đối với AES-GCM, đăng nhập trước khi mã hóa.
4. Mở **Xem lịch sử** (`frm_LichSu`) → nhấn **Tải lại**.
5. Xác nhận bảng `dbo.crypto_history` hiển thị các thao tác tương ứng với sáu thuật toán; bài AES-CBC Python không ghi vào bảng lịch sử Java/SQL Server.

**Kết quả:** Theo kết quả thực hành đã xác nhận, các bước kiểm thử tích hợp hoàn thành; chức năng lịch sử hiển thị dữ liệu thao tác đã lưu trong SQL Server.

