# Cài đặt Jenkins trên Windows
## **1) Cài đặt Standalone**
> **Lưu ý :** **Jenkins** hiện tại chỉ hỗ trợ **Java JDK 8** và **JDK 11** (khi cài đặt **Jenkins** trên **Docker**)
### **Cài đặt Java JDK 8**
- **B1 :** Download **Java JDK 16** tại [link](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html).
- **B2 :** Chạy file `jdk-8u301-windows-x64.exe` vừa download, chọn ***Next*** :

    <p align=center><img src="https://i.imgur.com/uzWo51r.png" width=50%></p>

- **B3 :** Tại cửa sổ **Select optional feature**, chọn ***Next*** :

    <p align=center><img src="https://i.imgur.com/tMhKzLO.png" width=50%></p>

- **B4 :** Tại cửa sổ **Destination Folder**, chọn ***Next*** để chọn đường dẫn mặc định :

    <p align=center><img src="https://i.imgur.com/XNFsBKJ.png" width=50%></p>

- **B5 :** Quá trình cài đặt diễn ra :

    <p align=center><img src="https://i.imgur.com/2ILztw9.png" width=50%></p>

- **B6 :** Chọn ***Close*** để hoàn tất quá trình cài đặt :

    <p align=center><img src="https://i.imgur.com/usGropr.png" width=50%></p>

- **B7 :** Truy cập ***Control Panel*** > ***System and Security*** > ***System*** > ***Advanced System Settings*** :

    <p align=center><img src="https://i.imgur.com/UBxLrJD.png" width=70%></p>

- **B8 :** Trong tab **Advanced**, chọn ***Environment Variables...*** :

    <p align=center><img src="https://i.imgur.com/jZH58p8.png" width=50%></p>

- **B9 :** Tại cửa sổ **Environment Variables**, thay đổi **Path** của Windows :

    <p align=center><img src="https://i.imgur.com/PcJhNau.png" width=50%></p>

- **B10 :** Chọn ***New*** để thêm đường dẫn cho **Java** :

    <p align=center><img src="https://i.imgur.com/HMTlLBw.png" width=50%></p>

- **B11 :** Thêm đường dẫn cài đặt **Java** `C:\Program Files\Java\jdk-16.0.2\bin`, sau đó chọn ***OK*** để hoàn tất :

    <p align=center><img src="https://i.imgur.com/Z5eUDN5.png" width=50%></p>

- **B12 :** Kiểm tra lại version **Java** đã cài đặt :
    ```
    > java -version
    ```
    ```
    java version "1.8.0_301"
    Java(TM) SE Runtime Environment (build 1.8.0_301-b09)
    Java HotSpot(TM) 64-Bit Server VM (build 25.301-b09, mixed mode)
    ```
### **Cài đặt Jenkins**
- **B1 :** Download Jenkins tại [link](https://www.jenkins.io/download/).
- **B2 :** Sau khi tải về file `jenkins.msi`, tiến hành run để cài đặt. Tại cửa sổ **Welcome**, chọn ***Next*** để tiếp tục :

    <p align=center><img src="https://i.imgur.com/jGN5rUs.png" width=50%></p>

- **B3 :** Tại cửa sổ **Destination Folder**, chọn ***Next*** để tiếp tục :
    
    <p align=center><img src="https://i.imgur.com/Gt1asn9.png" width=50%></p>

- **B4 :** Tại cửa sổ **Service Logon Credential**, chọn ***Run service as LocalSystem*** rồi chọn ***Next*** để tiếp tục :

    <p align=center><img src="https://i.imgur.com/iU5PMHz.png" width=50%></p>

- **B5 :** Tại cửa sổ **Port Selection**, chọn port cho **Jenkins**, sau đó chọn ***Test Port*** để kiểm tra port có sử dụng được không -> chọn ***Next*** để tiếp tục :

    <p align=center><img src="https://i.imgur.com/46Ge4os.png" width=50%></p>

- **B6 :** Tại cửa sổ **Select Java home directory**, chọn ***Nex*** :

    <p align=center><img src="https://i.imgur.com/bY5EX8x.png" width=50%></p>

- **B7 :** Tại cửa sổ **Custom Setup**, chọn ***Next*** :

    <p align=center><img src="https://i.imgur.com/jlBc2KK.png" width=50%></p>

- **B8 :** Chọn ***Install*** để tiến hành cài đặt :

    <p align=center><img src="https://i.imgur.com/XpqNiPv.png" width=50%></p>

- **B9 :** Chọn ***Finish*** để kết thúc cài đặt :

    <p align=center><img src="https://i.imgur.com/bGYqnzZ.png" width=50%></p>

- **B10 :** Trên trình duyệt, truy cập URL : `http://localhost:8080` để vào dashboard của **Jenkins**. Tại đây ta sẽ thấy **Jenkins** yêu cầu nhập mật khẩu để Unlock. Để đảm bảo người cài đặt nắm quyền Administrator, người dùng cần phải truy cập được vào file `C:\Windows\system32\config\systemprofile\AppData\Local\Jenkins\.jenkins\secrets\initialAdminPassword` để lấy password. Sau khi nhập password, chọn ***Continue*** để tiếp tục :

    <img src="https://i.imgur.com/udFdYWA.png">

- **B11 :** Tại cửa sổ **Customize Jenkins**, chọn ***Install suggested plugins*** :

    <img src=https://i.imgur.com/Kd8T0hq.png>

- **B12 :** Sau khi cài đặt xong các plugin, tại cửa sổ **Create First Admin User**, **Jenkins** yêu cầu tạo một user khác để bảo mật cho user `admin` ban đầu. Nếu muốn bỏ qua, chọn ***Skip and continue as admin*** :

    <img src=https://i.imgur.com/WS0PQbK.png>

- **B13 :** Tại cửa sổ **Instance Configuration**, chọn ***Save and Finish*** :

    <img src=https://i.imgur.com/lOGKUyc.png>

- **B14 :** Chọn ***Start using Jenkins*** :

    <img src=https://i.imgur.com/Ew0lwCi.png>

- **B15 :** Quá trình setup cơ bản đã xong. Let's enjoys!

    <img src=https://i.imgur.com/CoHpVLC.png>
## **2) Cài đặt Jenkins trên Apache Tomcat**
### **Cài đặt Java JDK 8**
### **Download Jenkins war file**
- Download `jenkins.war` tại [link](https://www.jenkins.io/download/) :

    <img src=https://i.imgur.com/5oEJtYX.png>

### **Cài đặt Apache Tomcat 9**
> Cần cài đặt **Tomcat 9** vì sau version 9 sẽ không hỗ trợ **Java JDK 8**
- **B1 :** Download file cài đặt **Apache Tomcat** tại [link](https://tomcat.apache.org/download-90.cgi).
- **B2 :** Chạy file `apache-tomcat-9.0.52.exe` vừa download, chọn ***Next*** :

    <p align=center><img src="https://i.imgur.com/LF7Apzi.png" width=50%></p>

- **B3 :** Tại cửa sổ **License Agreement**, chọn ***I Agree*** :

    <p align=center><img src="https://i.imgur.com/wTNI37U.png" width=50%></p>

- **B4 :** Tại cửa sổ **Choose Components**, chọn ***Next*** :

    <p align=center><img src="https://i.imgur.com/aFHCzbs.png" width=50%></p>

- **B5 :** Tại cửa sổ **Configuration**, có thể tạo Administrator User để quản lý Tomcat qua GUI, sau đó chọn ***Next*** :

    <p align=center><img src="https://i.imgur.com/m0jc73M.png" width=50%></p>

- **B6 :** Tại cửa sổ **Java Virtual Machine**, chọn ***Next*** :

    <p align=center><img src="https://i.imgur.com/Iv2lnB1.png" width=50%></p>

- **B7 :** Tại cửa sổ **Choose Install Location**, chọn ***Install*** để tiến hành cài đặt :

    <p align=center><img src="https://i.imgur.com/dSVus6r.png" width=50%></p>

- **B8 :** Quá trình cài đặt hoàn tất, chọn ***Finish*** để kết thúc :

    <p align=center><img src="https://i.imgur.com/x2jycW8.png" width=50%></p>

- **B9 :** Trên trình duyệt, truy cập `http://localhost:8080` để vào giao diện của Tomcat, chọn ***Manage apps*** :

    <img src=https://i.imgur.com/fhgRW6J.png>

- **B10 :** Hệ thống sẽ yêu cầu user password Administrator đã tạo từ trước. Sau khi đăng nhập vào giao diện quản lý app của **Tomcat**, tại tab **WAR file to deploy**, chọn ***Choose file*** để browse tới file `jenkins.war` đã download :

    <img src=https://i.imgur.com/mAGdOSU.png>

- **B11 :** Chọn ***Deploy*** để cài đặt app **Jenkins** :

    <img src=https://i.imgur.com/AcOOLor.png>

- **B12 :** Quá trình cài đặt sẽ mất `2-3p`. Sau khi cài đặt thành công, ta sẽ thấy app **Jenkins** xuất hiện ở trang quản lý :

    <img src=https://i.imgur.com/FGoVkV3.png>

- **B13 :** Trên trình duyệt, truy cập `http://localhost:8080/jenkins` để vào trình setup của **Jenkins** :

    <img src=https://i.imgur.com/UjOuinv.png>