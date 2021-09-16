# Các thao tác vận hành Jenkins
## **1) Các thao tác với Jenkins Service**
- Trong terminal của node **manage**, có thể thực hiện một số thao tác sau :
    - Khởi động dịch vụ `jenkins` :
        ```
        # systemctl start jenkins
        ```
    - Dừng dịch vụ `jenkins` :
        ```
        # systemctl stop jenkins
        ```
    - Khởi động lại dịch vụ :
        ```
        # systemctl restart jenkins
        ```
    - Cho phép dịch vụ khởi động cùng hệ thống :
        ```
        # systemctl enable jenkins
        ```
- **Jenkins Server** cũng cung cấp một số API sau để thực hiện các thao tác stop/start dịch vụ :
    - `http://<JENKIN URL>/jenkins/exit` - dừng dịch vụ `jenkins`
    - `http://<JENKIN URL>/jenkins/restart` - khởi động lại dịch vụ
    - `http://<JENKIN URL>/jenkins/reload` - reload cấu hình `jenkins`
## **2) Các lưu ý khi cấu hình**
- Luôn cấu hình các build job đi kèm với automated testing khi chạy Testing Job.
- Sử dụng public key authentication khi thiết lập các node agent
- Sử dụng **label** : tạo ra nhiều khoảng agent bên trong 1 cluster, một cách để quản lý sự đa dạng của các node. Việc sử dụng đúng **label** sẽ giúp các team xác định tính duy nhất của 1 node và sử dụng nó đúng mục đích.
- Parallel execution : thực hiện các job song song là cách tốt hơn để xem kết quả và nhận về phản hồi nhanh chóng. Mọi **pipeline** đều có thể được thực hiện song song.
## **3) Các lưu ý khi maintainance**
- Mọi job cần chứa script liên quan đến việc cleanup sau khi hoàn thành.
- **Jenkins** cũng cần có các job maintain để tránh xảy ra việc full disk.
- Nên xóa các bản build cũ trước khi build mới.
- Các team cần archive lại các job không sử dụng trước khi xóa.
- Để tận dụng lợi thế của **Distributed Build** trong các hệ thống lớn, đảm bảo hoàn toàn các job chạy trên các **slave**, không chạy trên **master**.