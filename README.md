

**Hệ Thống Giám Sát Dịch Vụ API và Cơ Sở Dữ Liệu**

**Mô Tả**

Hệ thống giám sát này được thiết kế để giám sát dịch vụ API và cơ sở dữ liệu sử dụng Prometheus, Grafana, Alertmanager, Node Exporter, Blackbox Exporter, Mysql Exporter, Mongodb Exporter. Hệ thống này được triển khai thông qua Docker Compose và bao gồm các chức năng cơ bản như giám sát tài nguyên hệ thống, trạng thái API, cảnh báo khi API trả về mã lỗi HTTP thông báo về Discord (Tele Slack), và hiển thị dữ liệu giám sát trên giao diện Grafana.

**Cài Đặt**

Để cài đặt hệ thống, bạn cần thực hiện các bước sau:

1. Cài đặt Docker trên máy tính của bạn.
2. Chạy lệnh `git clone https://github.com/hiamt34/Prometheus-Grafana-Alertmanager-Exporter.git` để tải mã nguồn xuống.
3. Chạy lệnh `docker-compose up -d` để khởi động hệ thống.

**Các Thành Phần**

* **Prometheus**: Thu thập và lưu trữ dữ liệu giám sát.
* **Alertmanager**: Gửi cảnh báo khi có sự cố.
* **Grafana**: Hiển thị các dashboard giám sát.
* **Node Exporter**: Thu thập dữ liệu tài nguyên hệ thống (CPU, RAM, Disk).
* **Blackbox Exporter**: Kiểm tra trạng thái và mã phản hồi HTTP của API.
* **MySQL Exporter**: Kiểm tra trạng thái, connect, tải, uptime... của MySQL.
* **Mongo Exporter**: Kiểm tra trạng thái, connect, uptime... của Mongodb.
* **Server Health Check**: Để giả lập 1 server khi Blackbox kiểm tra trạng thái của api health-check thì nó sẽ trả ra status code bất kỳ.
* **Discord**: Nơi nhận cảnh báo của Prometheus khi API gặp lỗi, Node bị down.... (có thể thay bằng Tele hoặc Slack)

**Cấu Hình**
.
├── configs                              # Thư mục chứa các file cấu hình
│   ├── grafana                          # Thư mục chứa các file cấu hình Grafana
│   │   ├── provisioning                
│   │   │   ├── dashboards
│   │   │   │   ├── mysql-exporter.json
│   │   │   │   ├── node-exporter.json
│   │   │   │   └── v3.json
│   │   └── grafana.ini
│   ├── prometheus                        # File cấu hình
│   │   └── prometheus.yml
│   └── blackbox
│       └── blackbox.yml
├── docker-compose.yml
└── README.md

**Kết Quả Mong Đợi**

Khi chạy hệ thống, bạn sẽ thấy các dashboard giám sát trên giao diện Grafana, bao gồm:

* Giám sát tài nguyên hệ thống (CPU, RAM, Disk).
* Trạng thái API (success rate, response time).
* Cảnh báo trực quan khi API gặp lỗi.

**Lưu Ý**

* Hệ thống này được thiết kế để chạy trên môi trường Docker.
* Bạn cần cài đặt Docker và Docker Compose trên máy tính của bạn để chạy hệ thống.
* Bạn cần cấu hình lại file `config.yml` để gửi cảnh báo qua Slack hoặc Telegram.