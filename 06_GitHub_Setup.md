# Tích hợp Jenkins với GitHub
## **1) Giới thiệu**
- **Jenkins** là một CI server, và nó hoạt động bằng cách kiểm tra source code trong repository và build code. **Jenkins** hỗ trợ tốt cho các hệ thống quản lú source code như **GitHub**, **Gitlab**,...
- **GitHub** hiện đang nhanh chóng trở thành một hệ thống quản lý source code phổ biến. Nó là một repository dựa trên web, đóng vai trò quan trọng đối với DevOps. **Github** cung cấp một nền tảng chung cho nhiều developer làm việc trên cùng một code project để truy xuất code liên tục, tạo điều kiện tốt cho **CI**. **Jenkins** làm việc với **Git** thông qua plugin `Git`.
- Để thiết lập **GitHub**, cần đảm bảo server cài đặt **Jenkins** có kết nối internet.
- Khi bạn tạo một **Project build job** thì **Jenkins Git plugin** sẽ cung cấp cho bạn option lựa chọn `Git` trong phần quản lý **SCM**. Bạn sẽ phải khai báo URL về **Git Repository** của bạn. Kế đến khi `build` job chạy thì **Jenkins Git plugin** sẽ thực hiện hoạt động cơ bản đó là truy vấn `git pull` giúp clone remote repository và lưu toàn bộ dữ liệu Repository đó ở thư mục **Jenkins workspace** tương ứng của từng Project.
- Kế đến bắt đầu từ thư mục **Workspace** đó bạn sẽ tiến hành các hoạt động như biên dịch, unit test, đóng gói,…. hoặc các hoạt động khác mà bạn mong muốn trong quá trình Jenkins `build` job.

    <img src=https://i.imgur.com/SROzvyr.png>
## **2) Các bước tích hợp**
### **Cấu hình Git trên Jenkins server**
- **B1 :** Cài đặt **Git** trên Jenkins server.
    ```
    # yum install git -y
    ```
- **B2 :** Thêm SSH public key của server vào **GitHub** của bạn.

    <img src=https://i.imgur.com/FBYgcEW.png>

- **B3 :** Cấu hình thông tin user `git` trên server :
    ```
    # git config --global user.name "QuocCuong97"
    # git config --global user.email "cuongnq24101997@gmail.com"
    ```
### **Cấu hình Jenkins**
- **B4 :** Trên dashboard của **Jenkins**, chọn **Manage Jenkins** :

    <img src=https://i.imgur.com/rtqIuFO.png>

- **B3 :** Chọn **Manage Plugins** :

    <img src=https://i.imgur.com/CnM3Bdo.png>

- **B4 :** Chọn tab **Installed** để verify là `Git plugin` đã được cài đặt. `Git plugin` nằm trong gói suggested plugin ta đã cài đặt khi setup bước đầu **Jenkins** :

    <img src=https://i.imgur.com/inclwnQ.png>

- **B5 :** Quay lại màn hình dashboard, chọn **New Item** để khởi tạo project mới :

    <img src=https://i.imgur.com/4kKcXq8.png>

- **B6 :** Nhập tên của project, chọn **Freestyle project** rồi chọn ***OK*** :

    <img src=https://i.imgur.com/IO4FT7d.png>

- **B7 :** Tại tab **General**, nhập các thông tin cơ bản như mô tả project,... :

    <img src=https://i.imgur.com/VbzyXYR.png>

- **B8 :** Tại tab **Source Code Management**, nhập 1 số cơ bản như thông tin repo, thông tin branch,... rồi chọn ***Apply*** -> ***Save***:

    <img src=https://i.imgur.com/xYYsgmu.png>

    - Vậy là bước đầu ta đã tích hợp được **GitHub** vào **Jenkins** :

        <img src=https://i.imgur.com/fEAH6vq.png>