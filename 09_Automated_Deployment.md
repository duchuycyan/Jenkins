# Automated Deployment
- Quá trình **Automated Deployment** sẽ tự động build một pipeline mỗi khi code source code được commit lên repo.
## **Các bước thực hiện**
### **Cấu hình Jenkins Webhook trên GitHub**
- **B1 :** Tại repo muốn thực hiện CI/CD, chọn **Settings** :

    <img src=https://i.imgur.com/AqhNmx1.png>

- **B2 :** Chọn **Webhooks** -> ***Add webhook*** :

    <img src=https://i.imgur.com/1VTe6hx.png>

- **B3 :** Trong mục **Payload URL**, nhập vào URL của **Jenkins** (public), theo sau URL là `/github-webhook/`. Trong mục **Content type**, chọn `application/json` :

    <img src=https://i.imgur.com/gwEhdFA.png>

- **B4 :** Tại mục **Which events would you like to trigger this webhook?**, chọn ***Let me select individual events.*** Sau đó chọn các event cụ thể muốn trigger tới webhook : ***Pull requests*** và ***Pushes*** -> ***Add Webhook*** :

    <img src=https://i.imgur.com/KGRqj5j.png>

- **B5 :** Webhook được add thành công :

    <img src=https://i.imgur.com/v81m62D.png>

### **Cấu hình trên Jenkins**
- **B1 :** Chỉnh sửa pipeline đã tạo từ trước trên **Jenkins**: tại section **Build Triggers**, chọn ***GitHub hook trigger for GITScm polling*** -> ***Apply*** -> ***Save*** :

    <img src=https://i.imgur.com/sNpeeGE.png>

- **B2 :** Thực hiện sửa và commit code.

    <p align=center><img src=https://i.imgur.com/mJuGux0.png width=70%></p>

- **B3 :** Quay lại dashboard của **Jenkins** để thấy quá trình build pipeline tự động diễn ra :

    <img src=https://i.imgur.com/IDWDJoI.png>

- **B4 :** Sau khi quá trình build thành công, kiểm tra application trên trình duyệt để thấy code mới đã được deploy :

    <img src=https://i.imgur.com/iaM6FjB.png>