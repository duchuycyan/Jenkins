# Cấu hình Notification cho Jenkins
## **1) Cấu hình Email Notification**
- **Email** là một khía cạnh quan trọng trong mọi tổ chức do tính dễ sử dụng và tính sẵn sàng cao của nó.- **Jenkins email notification** là một plugin dựa trên **Java** để tự động hóa cảnh báo thông qua email. Nó sẽ hữu ích cho quá trình **CI**.
> ### **Các bước cấu hình**
- **B1 :** Trên Dashboard, truy cập **Manage Jenkins** :

    <img src=https://i.imgur.com/vga54Og.png>

- **B2 :** Chọn **Manage Plugins** :

    <img src=https://i.imgur.com/zRBM9fG.png>

- **B3 :** Tìm kiếm và cài đặt đủ 2 plugin : **Email Extension Plugin** và **Email Extension Template Plugin** :

    <img src=https://i.imgur.com/fnyP43W.png>

- **B4 :** Để cấu hình SMTP server, quay lại **Manage Jenkins** -> **Configure System** :

    <img src=https://i.imgur.com/XjhFvQR.png>

- **B5 :** Kéo xuống mục **Jenkins Location**, nhập thông tin ***System Admin e-mail address***. Đây sẽ là tên user hiển thị khi gửi mail. Có thể để theo định dạng "`DisplayName <email_id@example.com>`" :

    <img src=https://i.imgur.com/nwQPmXf.png>
- **B6 :** Kéo xuống mục **Email Notification**, chọn ***Use SMTP Authentication*** sau đó nhập các thông tin sau :
    - User name: email_id@gmail.com (Email sender)
    - Password: *******             (Password Sender)
    - Use SSL: Checked
    - SMTP Port: `465`
    - Test e-mail recipient: email_id@gmail.com  (Test receiver)
    - Chọn ***Test Configuration*** để test cấu hình

    <img src=https://i.imgur.com/aCnih6g.png>

- **B7 :** Kiểm tra email test đã nhận được để verify cấu hình đã đúng :

    <img src=https://i.imgur.com/jvqPuDo.png>

    <img src=https://i.imgur.com/RrUfifa.png>

- **B8 :** Quay lại cấu hình email, bỏ chọn ***Test configuration by sending test e-mail*** -> ***Apply*** -> ***Save*** để lưu cấu hình :

    <img src=https://i.imgur.com/F2shTys.png>

- **B9 :** Trong **Project** cần build, chọn **Configure** :

    <img src=https://i.imgur.com/E7sA4Ry.png>

- **B10 :** Tại section **Build**, chọn ***Add post-build action*** -> ***Email Notification*** :

    <img src=https://i.imgur.com/M2Lc08L.png>

- **B11 :** Tại mục **Recipients**, nhập email người nhận (nếu nhiều email, phân tách nhau bằng dấu `space`). Email sẽ được gửi khi build fail, `unstable` hoặc bản build `stable` đầu tiên sau bản build fail. Ở đây có 2 lựa chọn :
    - ***Send e-mail for every unstable build*** : gửi email đển tất cả mọi người trong **Recipients**.
    - ***Send separate e-mails to individuals who broke the build*** : gửi email đển tất cả mọi người trong **Recipients**, đồng thời email tới người đã commit code cuối cùng khiến bản build bị fail
    - Chọn ***Apply*** -> ***Save*** để lưu lại cấu hình :

    <img src=https://i.imgur.com/DvqqfW2.png>

- **B12 :** Tiến hành build project để kiểm tra email trả về.
- **B13 :** Nếu quá trình build bị lỗi, sẽ nhận được email thông báo :

    <img src=https://i.imgur.com/qZbvQeJ.png>

    - Sau khi được fix, quá trình build OK trở lại, cũng sẽ nhận được email thông báo :

        <img src=https://i.imgur.com/G9F0OBV.png>
## **2) Cấu hình Slack Notification**