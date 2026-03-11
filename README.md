# Testing-System

Kiểm định an toàn thông tin hệ thống Web Application trên môi trường mô phỏng doanh nghiệp.  

---

## Môi trường

- **Mục tiêu:** Công ty ABC giả định — 2 máy chủ (Linux + Windows Web Server)
- **Công cụ tấn công:** Kali Linux (192.168.202.129)
- **Web App lỗ hổng:** DVWA trên Windows Server 2016 + XAMPP

## Công cụ

| Reconnaissance | Exploitation | Web Testing |
|---|---|---|
| Nmap + vulners | Metasploit Framework | Burp Suite |
| Nessus, OpenVAS | msfconsole | CyberChef |
| Nikto | curl, netcat | Developer Tools (F12) |

---

## Phạm vi kiểm thử

### Linux Server — CVE Exploited

| Port | Dịch vụ | CVE | Kết quả |
|---|---|---|---|
| 21/tcp | vsftpd 2.3.4 | CVE-2011-2523 (CVSS 10.0) |  Root shell |
| 6667/tcp | UnrealIRCd | CVE-2010-2075 |  Reverse shell |
| 22/tcp | OpenSSH 4.7p1 | CVE-2023-38408 |  Brute-force thành công (`msfadmin:msfadmin`) |

### Windows Web Server — OWASP Top 10

| Lỗ hổng | Mức độ | Kết quả |
|---|---|---|
| Brute Force | Medium |  Dò được password qua Content-Length diff |
| Command Injection | High |  Đọc file, liệt kê hệ thống |
| CSRF | Medium |  Chiếm tài khoản qua cookie stolen |
| File Inclusion (LFI) | Medium |  Đọc file ẩn ngoài danh sách |
| File Upload | High |  Upload Web Shell (`image.php.jpg`) |
| SQL Injection | High |  Dump toàn bộ bảng users + version DB |
| XSS (Reflected) | High |  Đánh cắp session cookie |
| JavaScript Attack | Medium |  Reverse token MD5(ROT13) bằng CyberChef |
| Authorisation Bypass | High |  Truy cập API admin qua URL trực tiếp |
| Cryptography | High |  AES-128-ECB block swap → leo thang đặc quyền |

---

## Kết quả

- Khai thác thành công **3/3 CVE** trên Linux, đạt quyền **root**
- Khai thác thành công **10/10 lỗ hổng OWASP Top 10** trên DVWA
- Phân loại rủi ro theo CVSS và đề xuất biện pháp khắc phục từng lỗ hổng

---



> ⚠️ Toàn bộ kiểm thử thực hiện trong môi trường sandbox được cấp phép, phục vụ mục đích học thuật.
