# Jenkins Pipeline
## **1) Pipeline CI/CD là gì ?**
- Như ta biết thì hoạt động **CI/CD** tự động hóa các quá trình `build`, `test` (Unit Test, Intergration Test, Smoke Test, BDD, ATDD, Security Test, Performance Test…), `deploy`, `delivery`,… giúp mỗi khi source code có thay đổi thì ngay lập tức thay đổi đó được chạy qua các quá trình liệt kê ở trên, đảm bảo các quá trình chạy đúng, không có vấn đề gì xảy ra. Từ đó **CI/CD** giúp đảm bảo chất lượng sản phẩm, đẩy nhanh quá trình phát triển, giảm chi phí vận hành và phát triển.
- **Pipeline CI/CD** là tập hợp quy trình thứ tự của các tác vụ được khai báo cho hoạt động `build`, `test`, `deploy`,… sản phẩm. Với **CI/CD pipeline**, mỗi khi phát hiện sự thay đổi trong mã nguồn dự án phần mềm, mã nguồn sẽ được **CI/CD Server** như **Jenkins** tiến hành `build` và `test` tự động. Nếu nó vượt qua các phần kiểm soát chất lượng và tất cả các bài `test` vượt qua, nó sẽ tự động được `deploy`.

    <img src=https://i.imgur.com/iIuCVwu.png>
## **2) Jenkins Pipeline**
- **Jenkins Pipeline** là bộ công cụ plugin hỗ trợ giúp triển khai và tích hợp quy trình **CI/CD pipeline** vào Jenkins.
- Trong những năm qua, đã có nhiều bản phát hành **pipeline Jenkins** bao gồm: **Jenkins Build Flow**, plugin **Jenkins Build Pipeline**, **Jenkins Workflow**,... Các tính năng chính của các plugin này là :
    - Plugin sẽ sắp xếp thể hiện các job trong một bộ quy trình **CI/CD flow** dưới dạng một quy chuẩn **pipeline**.
    - Các **pipeline** này là tập hợp các job **Jenkins** được kích hoạt có điều kiện với nhau theo một trình tự diễn biến cụ thể.
- **VD :** giả sử team đang phát triển một ứng dụng nhỏ trên **Jenkins** và muốn `build`, `test` và `deploy` ứng dụng này. Để làm điều này, nếu làm cách truyền thống thì ta sẽ cần phân bổ 3 job để thực hiện mỗi quy trình. Vì vậy, `job1` sẽ dùng để `build`, `job2` sẽ thực hiện các bài kiểm tra (`testing`) và `job3` để triển khai ứng dụng (`deploy`). Ta có thể sử dụng plugin xây dựng một **pipeline Jenkins** để thực hiện quy trình gồm thứ tự 3 job này.
- Cách tiếp cận này có hiệu quả khi triển khai các ứng dụng nhỏ. Nhưng điều gì xảy ra khi có xây dựng một **pipeline** phức tập hơn với một số quy trình (`build`, `test`, `unit test`, `integration test`, `pre-deploy`, `deploy`, `monitor`) chạy cả `100` job khác nhau.
- Chi phí xây dựng và bảo trì cho một **pipeline** phức tạp như vậy là rất lớn và tăng theo số lượng quy trình. Nó cũng trở nên tẻ nhạt để xây dựng và quản lý một số lượng lớn các job như vậy. Để khắc phục vấn đề này, một tính năng mới có tên **Jenkins Pipeline Project** đã được giới thiệu.
- Tính năng chính của **Jenkins Pipeline Project** này là giúp bạn định nghĩa khai báo toàn bộ flow quy trình triển khai **CI/CD** thông qua code. Điều đó có nghĩa là tất cả các công việc tiêu chuẩn được xác định bởi **Jenkins** đều có thể được khai báo viết thủ công dưới dạng toàn bộ tập lệnh và chúng có thể được lưu trữ trong một hệ thống kiểm soát phiên bản (Source Version Control). Thay vì xây dựng một số job cho từng giai đoạn, giờ đây bạn có thể lập trình code toàn bộ quy trình công việc và đưa nó vào **Jenkinsfile**.

    <img src=https://i.imgur.com/CrIt5fU.png>

## **3) Lợi ích của Jenkins Pipeline**
- **Jenkins Pipeline** được thực hiện dưới dạng code nên cho phép người dùng có thể chỉnh sửa và thực thi quá trình **pipeline**
- Sử dụng ngôn ngữ **Groovy** : mang đến sự thân thiện, dễ dàng implement hơn là sử dụng Bash / Bat Script
- Hỗ trợ **Docker** : Tùy biến môi trường phát triển cho từng project riêng biệt.
- Cấu trúc **DSL** chặt chẽ : sử dụng cú pháp **DSL (Domain Specific Language)** thuận tiện , cùng với đó là các methods/functions general của **jenkins pipeline** mang đến sự implement tối giản hơn.
- Dễ dàng mở rộng với **Shared Libraries** : Tự do xây dựng library common để sử dụng trong khi runtime.
- Hỗ trợ `build` đa luồng, đa môi trường phân tán trong cùng 1 `build`.
## **4) Jenkinsfile**
- **Jenkinsfile** là một file text chứa cấu hình của toàn bộ quy trình workflow **jenkins pipeline** dưới dạng code. Lợi thế của file text này giúp cho các lập trình viên hoặc quản trị viên dễ dàng truy cập, thay đổi nội dung code tuỳ biến ở mọi thời điểm.
- **Jenkinsfile** có quy chuẩn viết bằng ngôn ngữ **Groovy DSL**. Bạn có thể tạo ra **Jenkinsfile** thông qua trình text editor cơ bản hoặc qua giao diện cấu hình trên Jenkins website. Đối với **Jenkinsfile** sẽ có hai hình thức kĩ thuật khai báo cú pháp **Jenkinsfile**:
    - **Declarative pipeline**
    - **Scripted pipeline**
### **4.1) Declarative pipeline**
- Sử dụng những syntax đơn giản hơn. Dựa trên các methods / functions dựng sẵn, chỉ cần  sử dụng và tuân thủ theo các rule và syntax được định nghĩa sẵn theo các steps và funtions như vậy để implement theo các **stages** (từng đoạn trong **pipeline**). Nhìn chung là sẽ giúp người dùng dễ sử dụng như dễ viết/đọc các nội dung **pipeline** mà bạn khai báo.
- Cú pháp cơ bản của **Declarative pipeline** :
    ```groovy
    pipeline {
        agent any 
        stages {
            stage('Build') { 
                steps {
                    // 
                }
            }
            stage('Test') { 
                steps {
                    // 
                }
            }
            stage('Deploy') { 
                steps {
                    // 
                }
            }
        }
    }
    ```
- Concept :
    - `pipeline` : là block do người dùng định nghĩa, chứa tất cả các quy trình như `build`, `test`, `deploy`,..., là một nhóm các **stage** trong **Jenkinsfile**. Tất cả các **stage** và **step** được định nghĩa trong block này.
    - `stage` : block này chứa một loạt các **step** trong một **pipeline**: `build`, `test`, `deploy`. Nói chung, một block **stage** sẽ giúp hình dung quá trình **Jenkins Pipeline**.
    - `step` : là tác vụ duy nhất thực hiện một quy trình cụ thể tại 1 thời điểm xác định. Một **pipeline** bao gồm một loạt các **step** định nghĩa trong **stage**.
### **4.2) Scripted pipeline**
- Sử dụng **Groovy script** là kỹ thuật nâng cao hơn khi cần sử dụng code để implement vài tasks nào đó hoặc logic phức tạp tùy thuộc bài toán. Thường kĩ thuật này dùng cho các bạn có tư duy lập trình do phải nghiên cứu học thêm ngôn ngữ **Groovy**.
    ```groovy
    // Script //
    node {
      stage('Build') {
      echo 'Building....'
      }
      stage('Test') {
      echo 'Building....'
      }
      stage('Deploy') {
      echo 'Deploying....'
      }
    }
    ```
> Tham khảo **Pipeline Syntax** : https://www.jenkins.io/doc/book/pipeline/syntax/
## **5) Thao tác với Pineline**
### **Project GitHub**
- **Project** : https://github.com/QuocCuong97/pricelist
- File `Jenkinsfile` tạo sẵn trong project :
    ```Jenkinsfile
    pipeline {
        agent any
        stages {
            stage('Clear Old Version') {
                steps {
                    echo "Removing old containerized environment..."
                    sh '/usr/local/bin/docker-compose down -v'
                }
            }
            stage('Deploy Source Code') {
                steps {
                    echo "Running source code in a fully containerized environment..."    
                    sh '/usr/local/bin/docker-compose up -d --build'
                }
            }
        }
    }
    ```
### **Các bước thực hiện**
- **B1 :** Tạo 1 project **Pipeline**. Trên màn hình Dashboard chọn **New Item** :

    <img src=https://i.imgur.com/ckcFko5.png>

- **B2 :** Nhập tên project, chọn loại ***Pipeline*** -> ***OK*** để khởi tạo project :

    <img src=https://i.imgur.com/IgiVwy7.png>

- **B3 :** Tại section **Pipeline**, nhập một số thông tin sau :
    - **Definition** : chọn ***Pipeline script from SCM***
    - **SCM** : chọn ***Git***
    - **Repository URL** : nhập URL của project **GitHub**
    - Chọn ***Apply*** -> ***Save*** để lưu lại cấu hình

    <img src=https://i.imgur.com/XR274Q2.png>

- **B4 :** Chọn **Build Now** để tiến hành build pipeline :

    <img src=https://i.imgur.com/Cs1sQZU.png>

- **B5 :** Quá trình build diễn ra :

    <img src=https://i.imgur.com/9YovrzQ.png>

- **B6 :** Sau khi quá trình build thành công, kiểm tra application trên trình duyệt client :

    <img src=https://i.imgur.com/B2lI93q.png>

- **B7 :** Thử chỉnh sửa source code, sau đó build lại lần 2 :

    <img src=https://i.imgur.com/xG9xDbn.png>

- **B8 :** Application đã được deploy source code mới nhất :

    <img src=https://i.imgur.com/k8Gjp3W.png>
