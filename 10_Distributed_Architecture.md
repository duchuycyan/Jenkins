# Cấu hình mô hình Distributed Build - Master & Slave
## **1) Giới thiệu**
- Nếu đang trong các dự án lớn với các ứng dụng nặng và được build thường xuyên thì việc chạy các build job này trên chỉ một node trung tâm sẽ không phải lựa chọn tốt nhất. Trong trường hợp này, có thể cấu hình các **Jenkins machine** khác thành các **Slave** để chia tải giúp cho **Master Jenkins machine**.
- Đôi khi cũng có trường hợp cần một số môi trường khác nhau để test bản build, việc sử dụng **Slave** để đại diện cho mỗi môi trường sẽ là một ý kiến hay.
- Kiến trúc **Master-Slave** của **Jenkins** được sử dụng cho các môi trường **distributed build**, nơi mà workload của việc build project được phân tán trên các **agent node** hoặc **Slave**. Cũng có thể tạo ra các môi trường khác nhau cho mỗi bản build.

    <p align=center><img src=https://i.imgur.com/Sf2Q5UL.png width=70%></p>

- Vì mỗi **slave** chạy một chương trình riêng biệt, gọi là **slave agent**, nên không yêu cầu cài đặt **Jenkins** full trên **slave**. Có nhiều cách để khởi động **slave agent**, tuy nhiên **Jenkins master** cần thiết lập một liên kết 2 chiều (TCP/IP,...) để có thể hoạt động hoàn chỉnh.
- Có thể kết nối **Master** và **Slave** theo 2 cách :
    - Sử dụng giao thức **SSH** : sử dụng giao thức SSH để kết nối tới các **agent**. Kết nối được bắt đầu từ **Jenkins Master** và qua port `22` giữa **master** và **slave**.
    - Sử dụng phương thức **JNLP** : sử dụng giao thức Java **JNLP** (**Java Network Launch Protocol**). Trong phương pháp này, một Java agent được khởi tạo từ **agent** với các thông tin từ **master**. Node **master** cần allow các kết nối trên port **JNLP** được chỉ định. Thông thường, đây là port `50000`.
- Có 2 loại **Jenkins Agent** :
    - **Agent Nodes :** đây là các server (Windows/Linux) sẽ được cấu hình làm các ***static agent***. Các agent này sẽ luôn hoạt động và luôn kết nối với **Jenkin master**. Các tổ chức thường sử dụng các custom script để shutdown và restart agent khi không được sử dụng, thường chạy vào đêm hoặc cuối tuần.
    - **Agent Clouds :** **Jenkin Cloud agent** sẽ được cấu hình làm các ***dynamic agents***. Có nghĩa, bất cứ khi nào trigger một **job**, một agent sẽ được deploy như một VM/container theo yêu cầu và bị xóa khi **job** completed. Phương thức này tiết kiệm chi phí cơ sở hạ tầng khi có một hệ sinh thái **Jenkins** lớn và các bản build được thực hiện liên tục.

        <p align=center><img src=https://i.imgur.com/UvGwCiK.png width=70%></p>
## **2) Cấu hình Jenkins Slave**
### **2.1) Các bước chuẩn bị**
- Để cấu hình **Jenkins agent**, cần đảm bảo một số thứ sau trước khi thêm **agent** vào **master** :
    - **Java** cần được cài đặt trên agent server.
    - **Git** cần được cài đặt vì một số build job yêu cầu **Git**.
    - Một Linux user account có thể thực hiện các task trên agent server (nên sử dụng một user có quyền sudo nếu các task yêu cầu đặc quyền)
> #### **Cài đặt Java**
- Cài đặt **OpenJDK 11** trên RedHat/CentOS :
    ```
    # yum install -y java-11-openjdk-devel epel-release
    ```
- Cài đặt **OpenJDK 11** trên Ubuntu :
    ```
    $ sudo apt install default-jdk
    ```
> ####  **Cài đặt Git**
- Cài đặt **Git** trên RedHat/CentOS :
    ```
    # yum install git -y
    ```
- Cài đặt **Git** trên Ubuntu :
    ```
    $ sudo apt install git -y
    ```
> #### **Tạo user Jenkins**
- Tạo user `jenkins` và password kèm theo :
    ```
    # adduser jenkins --shell /bin/bash
    # passwd jenkins
    ```
- Login bằng user `jenkins` :
    ```
    # su jenkins
    ```
- Tạo thư mục `jenkins_slave` trong thư mục `/home/jenkins` :
    ```
    $ mkdir /home/jenkins/jenkins_slave
    ```
- Sinh cặp Key SSH :
    ```
    $ ssh-keygen -t rsa -C "The access key for Jenkins slaves"
    ```
> #### **Cấu hình Jenkins Master Credentials (trên node master)**
- Generate SSH keys và copy private key:
    ```
    # su - jenkins
    $ ssh-keygen
    $ cat /var/lib/jenkins/.ssh/id_rsa
    ```
- Trên màn hình dashboard, chọn **Manage Jenkins** -> **Manage Credentials** :

    <img src=https://i.imgur.com/fdyUBQT.png>

- Chọn credential **Jenkins** :

    <img src=https://i.imgur.com/uv1dOLE.png>

- Chọn **Global confidentials (unrestricted)** -> ***Add credentials*** :

    <img src=https://i.imgur.com/j3GVsv3.png>

- Nhập các thông tin về private key -> ***OK*** :

    <img src=https://i.imgur.com/MXM7WaI.png>

- Credential đã được tạo xong :

    <img src=https://i.imgur.com/h3wIjA8.png>

> #### **Copy SSH key sang slave**
- Thực hiện copy SSH key từ node master sang node slave :
    ```
    $ ssh-copy-id jenkins@<IP-SLAVE>
    ```
### **2.2) Cấu hình Jenkins Slave sử dụng SSH Keys**
- **B1 :** Trong màn hình dashboard của **Jenkins**, chọn **Manage Jenkins** -> **Manage Nodes and Clouds** :

    <img src=https://i.imgur.com/mE0RWQR.png>

- **B2 :** Chọn **New Node** để thêm node mới :

    <img src=https://i.imgur.com/LTwwmFb.png>

- **B3 :** Nhập tên node, chọn ***Permanent Agent*** -> ***OK*** :

    <img src=https://i.imgur.com/jFfARmt.png>

- **B4 :** Nhập các thông tin cho node **slave** :
    - **Name** : tên node
    - **Description** : mô tả
    - **Number of executors** : số luồng thực hiện cùng lúc
    - **Remote root directory** : thư mục chứa dữ liệu của Slave (đã tạo ở trên)
    - **Labels** : nhập label cho node để tiện phân loại khi build
    - **Usage** : nên chọn ***Only build jobs with label expressions matching this node***
    - **Launch method** : chọn ***Lauch agents via SSH***
    - **Host** : IP host slave
    - **Credentials** : chọn credential đã tạo trước đó
    - **Host Key Verification Strategy** : chọn ***Non verifying Verification Strategy***
    - Chọn ***Apply*** -> ***Save*** để hoàn tất

    <img src=https://i.imgur.com/4kM5BEj.png>

- **B5 :** Sau khi thêm thành công, node agent sẽ tự động được sync thông tin :

    <img src=https://i.imgur.com/I0cjM74.png>

- **B6 :** Khi cấu hình tạo project, chọn thêm phần ***Restrict where this project can be run*** để gán label của các node muốn build project

    <img src=https://i.imgur.com/Knjk4EE.png>

- Job được build thành công trên node mới :

    <img src=https://i.imgur.com/7iHF3xt.png>