# Quản lý user trong Jenkins
## **1) Giới thiệu**
- Nhìn chung, trong một tổ chức lớn, có nhiều team riêng biệt, phân tách nhau và quản lý và run các job trong **Jenkins**. Cần quản lý lượng người dùng này và phân quyền cho hợp lý.
- Mặc định, **Jenkins** chỉ đi kèm các tùy chọn tạo user rất cơ bản. Có thể tạo rất nhiều user nhưng chỉ có thể gán các role và đặc quyền chung cho chúng. Điều này sẽ không thích hợp cho một tổ chức lớn.
- Plugin **Role-based Authorization Strategy** cho phép gán các role và các quyền khác nhau cho các user khác nhau. Trước tiên, cần tìm và cài đặt plugin này :

    <img src=https://i.imgur.com/2wEQDVB.png>

- Sau khi cài đặt plugin, cần cấu hình **Global Security** sử dụng plugin này :
    - Truy cập **Manage Jenkins** -> **Configure Global Security** :

        <img src=https://i.imgur.com/7uLTz6X.png>

    - Tại section **Authorization**, chọn ***Role-Based Strategy*** -> ***Apply*** -> ***Save***

        <img src=https://i.imgur.com/G1XUUSO.png>

## **2) Tạo và phân quyền user**
### **2.1) Tạo user**
- Để tạo mới user, truy cập **Manage Jenkins**, chọn **Manage Users** :

    <img src=https://i.imgur.com/PrKarNK.png>

- Chọn **Create User** :

    <img src=https://i.imgur.com/17eEzVD.png>

- Nhập các thông tin cơ bản của user rồi chọn ***Create User*** :

    <img src=https://i.imgur.com/0xP033d.png>

- User được tạo thành công :

    <img src=https://i.imgur.com/wvk9FX1.png>

### **2.2) Gán role cho user**
- Truy cập **Manage Jenkins** -> **Manage and Assign Roles** :

    <img src=https://i.imgur.com/NkVohjj.png>

- Chọn **Manage Roles** để tạo các role :

    <img src=https://i.imgur.com/cCdJIz7.png>

- Add thêm một role là `developer` :

    <img src=https://i.imgur.com/LAOIIqY.png>

- Tích chọn các quyền muốn gán cho role `developer` -> ***Apply*** -> ***Save*** để lưu lại :

    <img src=https://i.imgur.com/YO9bvG3.png>

- Chọn **Assign Roles** để gán role cho user :

    <img src=https://i.imgur.com/GQq7oH6.png>

- Add thêm user đã tạo lúc trước để gán role :

    <img src=https://i.imgur.com/v4qdPjG.png>

- Tích chọn role, sau đó chọn ***Apply*** -> ***Save*** để lưu lại :

    <img src=https://i.imgur.com/Sso5n8A.png>

### **2.3) Tạo Project Roles**
- Sử dụng để gán quyền cho user được truy cập project chỉ định.
- Truy cập **Manage Jenkins** -> **Manage and Assign Roles** -> **Manage Roles**. Add thêm role vào **Item roles** và phân quyền thêm cho nó. **Pattern** ở đây sẽ để tên project hoặc regex :

    <img src=https://i.imgur.com/YdkcPkG.png>

- Truy cập **Manage Jenkins** -> **Manage and Assign Roles** -> **Assign Roles**. Add thêm user vào role trong **Item roles** :

    <img src=https://i.imgur.com/JDytjXC.png>

- Đăng nhập bằng user vừa phân quyền, ta sẽ thấy user đã được cấp quyền view project chỉ định :

    <img src=https://i.imgur.com/vL3UCjK.png>