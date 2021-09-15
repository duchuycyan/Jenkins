# Cài đặt Jenkins trên Linux
## **1) Cài đặt trên CentOS 7**
### **Cài đặt Jenkins**
- **B1 :** Cài đặt **OpenJDK 11** :
    ```
    # yum install -y java-11-openjdk-devel epel-release
    ```
- **B2 :** Cài đặt **Jenkins repo** :
    ```
    # wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
    # rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
    # yum upgrade -y
    ```
- **B3 :** Cài đặt **Jenkins** :
    ```
    # yum install jenkins -y
    ```
- **B4 :** Khởi động dịch vụ và cho phép dịch vụ khởi động cùng hệ thống :
    ```
    # systemctl start jenkins
    # systemctl enable jenkins
    ```
- **B5 :** Mặc định **Jenkins** sẽ chạy ở port `8080`. Cho phép port `8080` qua `firewalld` :
    ```
    # firewall-cmd --zone=public --permanent --add-port=8080/tcp
    # firewall-cmd --reload
    ```
- **B6 :** Kiểm tra trạng thái dịch vụ :

    <img src=https://i.imgur.com/g9C1z4d.png>

### **Cấu hình ban đầu cho Jenkins**
- **B1 :** Lấy init password trong file `/var/lib/jenkins/secrets/initialAdminPassword` :
    ```
    # cat /var/lib/jenkins/secrets/initialAdminPassword
    ```
    - Output :
        ```
        887b4c3b56024aafa2ac65925421674e
        ```
- **B2 :** Trên trình duyệt, truy cập trang quản lý của **Jenkins** `http://<ip-server>:8080`. Nhập init password đã lấy ở trên rồi chọn ***Continue*** :

    <img src=https://i.imgur.com/SACqVLt.png>

- **B3 :** Tại cửa sổ **Instance Configuration**, chọn ***Save and Finish*** :

    <img src=https://i.imgur.com/VTk6Mz2.png>

- **B4 :** Sau khi cài đặt xong các plugin, tại cửa sổ **Create First Admin User**, **Jenkins** yêu cầu tạo một user khác để bảo mật cho user `admin` ban đầu. Điền các thông tin cho user rồi chọn ***Save and Continue*** :

    <img src=https://i.imgur.com/tuhB5t4.png>

- **B5 :** Tại cửa sổ **Instance Configuration**, chọn ***Save and Finish*** :

    <img src=https://i.imgur.com/YcmIBzF.png>

- **B6 :** Chọn ***Start using Jenkins*** :

    <img src=https://i.imgur.com/uSpRvnJ.png>

- **B7 :** Quá trình setup cơ bản đã xong. Let's enjoys!

    <img src=https://i.imgur.com/ut7cYwZ.png>

## **2) Cài đặt Jenkins trên Ubuntu 20.04**
