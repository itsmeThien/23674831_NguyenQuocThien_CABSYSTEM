---
config:
  layout: elk
---
flowchart TB
    Customer["Khách hàng"]
    Driver["Tài xế"]
    Operator["Nhân viên vận hành"]

    CAB["CAB System<br/>Nền tảng đặt xe"]

    Booking["Đặt xe"]
    Dispatch["Tìm và phân công tài xế"]
    Trip["Thực hiện và theo dõi chuyến"]
    Fare["Tính cước"]
    Payment["Thanh toán"]
    Notification["Thông báo"]
    Rating["Đánh giá"]

    Admin["Quản trị vận hành"]
    Report["Báo cáo và phân tích"]

    PaymentGateway["Cổng thanh toán bên ngoài"]
    MapService["Dịch vụ bản đồ và định vị"]
    NotificationProvider["Nhà cung cấp thông báo"]

    Customer --> Booking
    Customer --> Trip
    Customer --> Payment
    Customer --> Rating

    Driver --> Dispatch
    Driver --> Trip
    Driver --> Notification

    Operator --> Admin
    Operator --> Report

    Booking --> Dispatch
    Dispatch --> Trip
    Trip --> Fare
    Fare --> Payment
    Trip --> Notification
    Payment --> Notification
    Trip --> Rating

    Dispatch --> MapService
    Payment --> PaymentGateway
    Notification --> NotificationProvider

    Booking --> CAB
    Dispatch --> CAB
    Trip --> CAB
    Payment --> CAB
    Admin --> CAB

    classDef actor fill:#eef2ff,stroke:#818cf8
    classDef core fill:#f0fdf4,stroke:#4ade80
    classDef admin fill:#fff7ed,stroke:#fb923c
    classDef external fill:#ecfeff,stroke:#22d3ee
    classDef platform fill:#f5f3ff,stroke:#a78bfa

    class Customer,Driver,Operator actor
    class Booking,Dispatch,Trip,Fare,Payment,Notification,Rating core
    class Admin,Report admin
    class PaymentGateway,MapService,NotificationProvider external
    class CAB platform
