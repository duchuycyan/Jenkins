# Tổng quan về Jenkins
## **1) Giới thiệu** <img src=https://i.imgur.com/nojq5a3.png align=right width=20%>
- Trang chủ : https://www.jenkins.io/
- **Jenkins** là một công cụ tự động hóa open-source được viết bằng **Java** cho phép triển khai tích hợp liên tục (***Continuos Integration***).
- **Jenkins** hỗ trợ `build` và `test` các project, liên tục giúp các developer tích hợp các thay đổi vào project dễ dàng hơn, giúp người dùng có bản build hoàn chỉnh sớm hơn.
- **Jenkins** cung cấp khả năng kết nối một lượng lớn các công nghệ kiểm thử và triển khai phổ biến hiện nay.
- Với sự giúp đỡ của **Jenkins**, các tổ chức có thể tăng tốc quá trình phát triển phần mềm thông qua tự động hóa. **Jenkins** bổ sung các quy trình về vòng đời (life-cycle) phát triển của sản phẩm, bao gồm `build`, `document`, `test`, `package`, `stage`, `static deploy` và hơn thế nữa.
- **Jenkins** triển khai được **CI** là nhờ sự hỗ trợ của các plugin. Các plugin được sử dụng để cho phép tích hợp các giai đoạn **Devops** khác nhau. Nếu muốn tích hợp một công cụ cụ thể, phải cài đặt plugin cho công cụ đó. **VD :** Maven 2, Git, HTML Publisher, Amazon EC2,...
- **Jenkins** cung cấp nhiều tính năng hấp dẫn cho các developers:
    - ***Dễ dàng cài đặt*** : **Jenkins** là một nền tảng độc lập dựa trên **Java**, sẵn sàng chạy trên các hệ điều hành Windows, MacOS, Unix-like
    - ***Dễ dàng cấu hình*** : Có thể dễ dàng cấu hình các chức năng **Jenkins** qua giao diện web của nó
    - ***Các plugins dồi dào*** : Có hàng trăm plugin có sẵn trong update center, mỗi plugin có thể cung cấp hoặc hỗ trợ cho một tính năng nào đó, tích hợp với mọi công cụ trong chuỗi công cụ CI và CD.
    - ***Extensible*** : **Jenkins** có thể được mở rộng bằng kiến trúc plugin của nó, cung cấp khả năng gần như vô tận cho những gì nó có thể làm.
    - ***Dễ dàng phân phối*** : **Jenkins** có thể dễ dàng phân phối công việc trên nhiều node để build, test và deploy nhanh hơn trên nhiều nền tảng.
    - ***Mã nguồn mở*** : **Jenkins** là một công cụ mã nguồn mở, nên dĩ nhiên nó miễn phí cộng với một cộng đồng hỗ trợ hùng hậu.
- Nhược điểm của **Jenkins** :
    - Giao diện đã outdate và không thích hợp với xu hướng UX/UI hiện tại
    - Không dễ maintain vì nó chạy trên server nên sẽ yêu cầu các kỹ năng quản trị server để duy trì hoạt động của nó.
    
## **2) Lịch sử phát triển của Jenkins**
- **Kohsuke Kawaguchi**, một Java developer làm việc tại **Sun Microsystems**, đã cảm thấy mệt mỏi với việc build code và sửa code lặp đi lặp lại. Năm `2004`, anh tạo ra một máy chủ tự động hóa tên là **Hudson** để tự động hóa các tác vụ `build` và `test`.
- Năm `2011`, **Oracle** sở hữu **Sun Microsystems** đã có tranh chấp với cộng đồng mã nguồn mở **Hudson**, vì vậy họ đã fork **Hudson** về và đổi tên thành **Jenkins**.
- Cả **Hudson** và **Jenkins** vẫn tiếp tục hoạt động độc lập. Nhưng trong một thời gian ngắn, **Jenkin** đã có được rất nhiều contributors và projects trong khi**Hudson** chỉ duy trì với `32` projects. Sau đó theo thời gian, **Jenkins** trở nên nổi tiếng hơn, và **Hudson** cũng không còn được duy trì nữa.
## **3) Workflow của Jenkins**
- Dưới đây là quy trình làm việc của **Jenkins** :
    - Các developer `commit` code thay đổi lên repository.
    - **Jenkins CI Server** đều đặn kiểm tra repository và phát hiện bất kỳ code mới nào được thêm vào.
    - **Build Server** build code thành một file thực thi. Trong trường hợp build thất bại sẽ phản hồi đến team dev.
    - **Jenkins** `deploy` ứng dụng đã được `build` lên server test. Nếu test thất bại sẽ phản hồi tới team dev.
    - Nếu code không có lỗi, ứng dụng đã được test sẽ được `deploy` lên **production**.

        <img src=https://i.imgur.com/3B5WLN4.png>
- Các file có thể chứa nhiều sự thay đổi code và các thay đổi này có thể rất lớn, yêu cầu nhiều lần `build`. Khi đó một server sẽ khó có thể đáp ứng được.Trong trường hợp này ta có thể xây dựng **Jenkins** thành một hệ phân tán để có thể giải quyết bài toán này.
## **4) Kiến trúc triển khai Jenkins**
- **Jenkins** tuân theo kiến trúc **Master-Slave** để quản lý `build` phân tán. Trong kiến trúc này, **master** và **slave** giao tiếp với nhau thông qua giao thức TCP/IP.
- Kiến trúc **Jenkins** bao gồm 2 thành phần :
    - **Jenkins Master / Server**
    - **Jenkins Slave / Node / Build Server**

    <p align=center><img src=https://i.imgur.com/DBiaVvk.png width=50%></p>

### **4.1) Jenkins Master**
- Server chính của **Jenkins** sẽ là **Jenkins Master**. Nó là một web dashboard được cung cấp từ 1 file `.war`, mặc định chạy trên cổng `8080`. Với sự trợ giúp của dashboard, ta có thể cấu hình các jobs/projects tuy nhiên quá trình build thì sẽ diễn ra trong các **Nodes/Slaves**. Mặc định, một **node** được cấu hình và chạy trên **Jenkins server**. Có thể add thêm nhiều node sử dụng địa chỉ IP, username và password hoặc sử dụng SSH,...
- Các công việc chính của **master** :
    - Scheduling build jobs
    - Gửi các bản build đến các **slave** để thực thi
    - Giám sát các **slave**
    - Ghi lại và báo cáo kết quả `build`
    - Một **master** cũng có thể thực hiện các build jobs trực tiếp trên chính nó.
### **4.2) Jenkins Slave**
- **Jenkins Slave** được sử dụng để thực hiện các build jobs được gửi đến từ **master**. Có thể cấu hình mỗi project luôn chạy trên 1 **slave** cụ thể, hoặc cho **Jenkins** tự chọn các **slave** khả dụng
- Các **slave** có thể chạy bất cứ nền tảng Windows/Linux hay MacOS.