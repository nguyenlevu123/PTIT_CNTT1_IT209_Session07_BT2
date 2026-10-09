# Bài 2: Quản trị Tường lửa UFW cho Cụm Dịch vụ Multi-port

## 1. Các lệnh cấu hình UFW

Khai báo các chính sách mặc định:
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

Cho phép các cổng dịch vụ quy định:
```bash
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 8082/tcp
```

Kích hoạt UFW:
```bash
sudo ufw enable
```

## 2. Kết quả kiểm tra

Đầu ra của lệnh `sudo ufw status verbose`:

```text
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere
80/tcp                     ALLOW IN    Anywhere
8082/tcp                   ALLOW IN    Anywhere
22/tcp (v6)                ALLOW IN    Anywhere (v6)
80/tcp (v6)                ALLOW IN    Anywhere (v6)
8082/tcp (v6)              ALLOW IN    Anywhere (v6)
```

**Nhận xét:**
- Trạng thái tường lửa hiển thị **Status: active**.
- Các cổng `22/tcp` (SSH), `80/tcp` (Web HTTP) và `8082/tcp` (Spring Boot) đều có trạng thái **ALLOW IN** từ **Anywhere**.
- Cổng `3306` (MySQL) không có trong danh sách cho phép, nên sẽ bị chặn kết nối từ bên ngoài do chính sách mặc định là `deny incoming`.
