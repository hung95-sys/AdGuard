# 🌈✨ AdGuard Home Auto Installer  
### 🛡️ Chặn quảng cáo toàn mạng • ⚡ Nhanh • 🔒 Bảo mật • 🛠️ Auto Install Script

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7d/Adguard-logo.png/600px-Adguard-logo.png" width="180">

---

# 📌 1. Chuẩn bị trước khi cài (CÀI ĐẶT UBUNTU)

## 🖥️ Hệ điều hành khuyến nghị

| Phiên bản | Trạng thái |
|----------|------------|
| **Ubuntu 22.04 LTS** | 🟢 Ổn định – khuyên dùng |
| Ubuntu 20.04 LTS | 🟡 Tốt |
| Ubuntu 24.04 LTS | 🟢 Mới – chạy tốt |

---

## 🔧 Cập nhật hệ thống

```bash
sudo apt update && sudo apt upgrade -y
```

## 📦 Cài các gói quan trọng

```bash
sudo apt install wget curl nano -y
```

---

# 🚀 2. Cài đặt AdGuard Home qua Script

Chạy 3 lệnh sau:

```bash
wget https://raw.githubusercontent.com/hung95-sys/AdGuard/main/install.sh -O install.sh
chmod +x install.sh
sudo ./install.sh
```

### 🖼️ Minh họa (console)

```
[ OK ] Disabled systemd-resolved
[ OK ] DNS set to 1.1.1.1
[ OK ] Downloading AdGuard Home...
[ OK ] Installing...
[ OK ] Starting service...
```

---

# 🧠 3. Script này làm gì?

| Tính năng | Mô tả |
|----------|--------|
| 🔧 Tắt `systemd-resolved` | Tránh chiếm port 53 |
| 🔄 Tạo `/etc/resolv.conf` mới | Dùng Cloudflare DNS |
| ⬇️ Tải AdGuard Home | Bản stable mới nhất |
| ⚙️ Auto Setup | Tự cài – tự tạo service |
| 🌐 Web UI | Tự mở tại `http://IP:3000` |

---

# 🌐 4. Truy cập giao diện thiết lập

### 🟢 Setup ban đầu
```
http://IP:3000
```

### 🔵 Sau khi hoàn tất:
```
http://IP
```

---

# 🛠️ 5. Cấu hình AdGuard Home (MÀU + DỄ NHÌN)

---

## 🔧 5.1 Cấu hình Upstream DNS (DNS chuyển tiếp)

Đi tới:

**Settings → DNS Settings → Upstream DNS servers**

### ➕ Thêm các DNS sau:

```
1.1.1.1
8.8.8.8
9.9.9.9
https://dns.cloudflare.com/dns-query
https://dns.google/dns-query
```

### 🎨 Giải thích:

| Loại | Công dụng |
|------|-----------|
| 🌐 IPv4 DNS | Nhanh + fallback khi DoH lỗi |
| 🔒 DoH (DNS-over-HTTPS) | Bảo mật, tránh bị dò DNS |

---

## 🛡️ 5.2 Thêm bộ lọc chặn quảng cáo (Blocklists)

Đi tới:

**Filters → DNS Blocklists → Add blocklist**

### ⭐ AdAway (nhẹ mà mạnh)

```
https://adaway.org/hosts.txt
```

### ⭐ StevenBlack (tổng hợp mạnh nhất)

```
https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts
```

### ⭐ OISD Big (siêu mạnh – chặn sạch nhất)

```
https://big.oisd.nl
```

---

## 💡 Combo bộ lọc đề xuất

✔ AdAway  
✔ StevenBlack  
✔ OISD Big  

---

# 🧰 6. Kiểm tra AdGuard Home đang chạy

### Kiểm tra service:

```bash
systemctl status AdGuardHome
```

### Kiểm tra port:

```bash
ss -tulpn | grep :53
```

### Test DNS:

```bash
nslookup youtube.com 192.168.100.4
```

---

# 🧹 7. Gỡ cài đặt AdGuard Home

```bash
sudo systemctl stop AdGuardHome
sudo systemctl disable AdGuardHome
sudo rm -rf /opt/AdGuardHome
sudo rm /etc/systemd/system/AdGuardHome.service
sudo systemctl daemon-reload
```

---

