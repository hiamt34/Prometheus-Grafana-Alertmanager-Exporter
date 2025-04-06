

**Hệ Thống Giám Sát Dịch Vụ API và Cơ Sở Dữ Liệu**

**Mô Tả**

Hệ thống giám sát này được thiết kế để giám sát dịch vụ API và cơ sở dữ liệu sử dụng Prometheus, Grafana, Alertmanager, Node Exporter, Blackbox Exporter, Mysql Exporter, Mongodb Exporter. Hệ thống này được triển khai thông qua Docker Compose và bao gồm các chức năng cơ bản như giám sát tài nguyên hệ thống, trạng thái API, cảnh báo khi API trả về mã lỗi HTTP thông báo về Discord (Tele Slack), và hiển thị dữ liệu giám sát trên giao diện Grafana.

**Cài Đặt**

Để cài đặt hệ thống, bạn cần thực hiện các bước sau:

1. Cài đặt Docker trên máy tính của bạn.
2. Chạy lệnh `git clone https://github.com/hiamt34/Prometheus-Grafana-Alertmanager-Exporter.git` để tải mã nguồn xuống.
3. Chạy lệnh `docker-compose up -d` để khởi động hệ thống.
4. Join Chanel Discord sau kể nhận mesages từ Prometheus khi có Req lỗi từ Blackbox Exporter vào server `https://discord.gg/DytH4tqU`
5. Truy cập Grafana `http://localhost:3000/` username:: `admin` password: `admin`. Bấm bào dashboards sẽ có sãn các Dashboard đã đc config phù hợp

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
├── configs
│    ├── alertmanager
│    │   └── alertmanager.yml              # File cấu hình receivers nhận notify
│    ├── blackbox
│    │   └── blackbox.yml                  # File cấu hình blackbox để kiểm tra và giám sát các dịch vụ
│    ├── grafana
│    │   └── provisioning
│    │       ├── dashboards
│    │       │   ├── dashboard.yml         # File cấu hình các dashboards
│    │       │   ├── mongo-exporter.json   # Dashboard Mongo Exporter
│    │       │   ├── mysql-exporter.json   # Dashboard MySQL Exporter
│    │       │   ├── node-exporter.json    # Dashboard Node Exporter
│    │       │   └── v3.json               # Dashboard Backbox Exporter
│    │       └── datasources
│    │           └── datasource.yml        # File cấu hình datasource (prometheus)
│    ├── mongo-entrypoint
│    │     └── init.js                     # File init MongoDB để Mongo Exporter có thế thu thập metrics
│    └── prometheus
│        ├── alert_rules.yml               # File cấu hình alert rule
│        └── prometheus.yml                # File cấu hình Job để thu thập metrics từ các Exporter định kỳ
├── docker-compose.yml
└── README.md

**Kết Quả**

Khi chạy hệ thống, bạn sẽ thấy các dashboard giám sát trên giao diện Grafana, bao gồm:

* Giám sát tài nguyên hệ thống (CPU, RAM, Disk).
* Giám sát trạng thái API taget.
* Giám sát tài nguyên MySQL
* Giám sát tài nguyên MongoDB
* Chanel Discord để nhận message cảnh báo khi có lỗi
