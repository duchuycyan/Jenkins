# Các công cụ CI/CD phổ biến
## **1) Jenkins**
- Trang chủ : https://www.jenkins.io/

    <img src=https://i.imgur.com/EWzPs3S.png>
- **Jenkins** là công cụ **CI** mã nguồn mở được viết bằng **Java**. Nó có nguồn gốc như là một nhánh của **Hudson** khi mà **Oracle** mua **Sun Microsystems**. **Jenkins** là công cụ **CI platform** và nó cung cấp cấu hình thông qua cả giao diện GUI và các câu lệnh console.
- Theo thống kê thì **Jenkins**:
    - Chiếm `71%` thị trường với cộng đồng sử dụng cũng như sự hỗ trợ lớn
    - có khoảng hơn `1400` plugin nên dễ dàng mở rộng
- **Jenkins** sẽ phù hợp với dự án:
    - Code lưu ở 1 server riêng
    - Muốn toàn quyền kiểm soát **CI/CD**
    - Yêu cầu 1 máy chủ tại chỗ
    - Yêu cầu quy trình công việc có thể tuỳ biến cao.
    - Có thể chỉ định 1 hay nhóm người quản lí và duy trì Jenkin.
    - Tiết kiệm tiền.
- ***Đánh giá:*** **Jenkins** là một trong những giải pháp tốt nhất cho **CI**, mạnh mẽ và linh hoạt.
## **2) TeamCity**
- Trang chủ : https://www.jetbrains.com/teamcity/

    <img src=https://i.imgur.com/8avm4Ds.png>
- **TeamCity** là máy chủ **CI** thật, đến từ công ty **JetBrains**. **JetBrains** đã xây dựng bản quyền trên thị trường phát triển phần mềm trên toàn thế giới, và công cụ của họ giống như **WebStorm** và **ReSharper** được các lập trình viên sử dụng phổ biến trên toàn thế giới.
- Đặc điểm :
    - Cung cấp toàn bộ các tính năng trong phiên bản miễn phí
    - Giới hạn `20` cấu hình và `3` bản build máy chủ (`2018`) và `2020` bản miễn phí tăng lên `100` cấu hình nên muốn dùng thêm thì phải trả phí.
    - Hoạt động trên nhiều nền tảng khác nhau và có sự hỗ trợ cho rất nhiều các công cụ và framework.
    - Bảo mật và cung cấp plugin cực kỳ ổn định.
- Sẽ phù hợp với dự án:
    - **Teamcity** dùng server riêng nên nếu cần giải pháp làm việc mà không gặp rắc rối về bảo trì thì đây là lựa chọn tốt.
    - Có thể chỉ định 1 hay nhóm người quản lí hay phụ trách nó
    - Có thể hỗ trợ khách hàng nhanh chóng.
    - Có nhiều dự án với cấu hình tương tự nhau, mỗi dự án tiến triển khác nhau
- ***Đánh giá :*** Đây là giải pháp tổng thể tuyệt vời, nhưng do sự phức tạp và giá cả, nó dường như phù hợp hơn cho nhu cầu của doanh nghiệp. Với quy mô nhỏ thì **Teamcity** là lựa chọn hợp lí.
## **3) Gitlab CI/CD**
- Trang chủ : https://docs.gitlab.com/ee/ci/

    <img src=https://i.imgur.com/C34oicJ.png>

- **GitLab CI** là một phần của dự án mã nguồn mở **GitLab**, được đưa ra bởi công ty **GitLab inc**. **GitLab** được lưu trữ trên gitlab.com, một dịch vụ được lưu trữ miễn phí và cung cấp quản lý kho lưu trữ `git` chi tiết với các tính năng như kiểm soát truy cập, theo dõi các vấn đề, đánh giá mã code và nhiều hơn nữa.
- Đặc điểm:
    - Công cụ có sẵn và tích hợp trên **GitLab** mà mọi người dùng **GitLab** có thể sử dụng
    - Cho phép mở rộng dễ dàng vì hệ thống máy chủ nhiều.
    - Cho phép lưu trữ một số tính năng **GitLab** trên máy chủ và phân bố nhãn cho chúng.
- Sẽ phù hợp nếu:
    - Code lưu trên **GitLab**
    - Bỏ qua config lằng nhằng của các công cụ khác.
    - Không cần plugin.
    - Khi cần có thể tích hợp **Docker**, **K8s**.
    - Liên tục phát hành tính năng ổn định.
- ***Đánh giá :*** Công cụ hiện tại được tổ chức với danh sách các tính năng ấn tượng, cung cấp cả miễn phí và giải pháp mức doanh nghiệp.
## **4) GitHub Actions**
- Trang chủ : https://github.com/features/actions

    <img src=https://i.imgur.com/5kYDbWv.png>

- **GitHub Actions** ra đời tháng `11` năm `2019`, là tính năng CI có sẵn trên **GitHub**, vì vậy sẽ thuận tiện cho những người sử dụng **GitHub**. **GitHub Actions** không cần server riêng, không cần maintain server, cung cấp cả gói miễn phí và tính phí.
- **GitHub Actions** khá đơn giản, khi tiến trình `build`, `test` và `deploy` được viết trong một file có định dạng `.yaml` nằm trong thư mục `.github/workflows/` trong chính source code **GitHub**.
- **GitHub** miễn phí `2000` phút build mỗi tháng cho private/public repo, `500MB` storage để lưu trữ package.
## **5) CircleCI**
- Trang chủ : https://circleci.com/

    <img src=https://i.imgur.com/RaA9A7x.png>
- **CircleCI** là công cụ cloud-based giúp tự động hóa quá trình tích hợp và triển khai. **CircleCI** không cần server riêng, không cần maintain server, thậm chí cung cấp cả gói miễn phí ngay cả đối với tài khoản doanh nghiệp.
- **CircleCI** hiện được sử dụng bởi rất nhiều công ty lớn như Spotify, Facebook, RedBull, Harvest, Teespring,...
- Đặc điểm:
    - Có khả năng lưu trữ mạnh mẽ và quy trình làm việc tuỳ biến cao
    - Dễ dàng thiết lập và chạy.
    - Có thể cấu hình và gửi kết quả trực tiếp đến **Slack**….
    - CircleCI hiện chỉ hỗ trợ **GitHub** và **BitBucket** và danh sách các ngôn ngữ bao gồm Java, Ruby/Rails, Python, Node.js, PHP, Haskell và Skala.
    - Khung giá chính của **CircleCI** là "container".
    - Có 5 mức song song (`1x`, `4x`, `8x`, `12x`, `16x`). Vì vậy, bắt đầu với `16` container, bạn có thể đạt được tối đa song song `16x` trên một bản `build`. Hoặc bạn có thể chạy `4` bản builds trên `16` containers với `4x` song song.
- Sẽ phù hợp nếu:
    - Cần hỗ trợ sẵn và song song với việc develop.
    - Code lưu trữ trên **Github** hay **BitBucket**.
    - Làm việc trên Mac hay Linux.
    - Nhóm bao gồm nhiều nhà phát triển dùng chung 1 CI.
    - Ưu tiên tốc độ hơn các thứ khác.
    - Cần chung 1 quy trình và quy trình công việc tuỳ biến cao, tương thích nhiều test tool, không giới hạn repo, user…
- ***Đánh giá :*** Nếu chi phí không phải vấn đề và cần nhanh thì **CircleCI** là 1 lựa chọn không thể bỏ qua.
## **6) Travis CI**
- Trang chủ : https://www.travis-ci.com/

    <img src=https://i.imgur.com/VUyB8EL.png>
    
- **Travis CI** là công cụ CI đầu tiên được cung cấp dưới dạng service tool, giới thiệu 1 hướng tiếp cận mới build code trên cloud. **Travis CI** cho phép người dùng đăng ký tài khoản, link repository, build cũng như test các ứng dụng.
- Công cụ này có thể dễ dàng tích hợp với kho lưu trữ repository phổ biến như **Bitbucket** và **GitHub**.
- Đối với các dự án open-source, **Travis CI** miễn phí. Đối với các dự án thương mại, cần mua gói enterprise.
- Đặc điểm:
    - Travis CI là miễn phí cho tất cả các dự án mã nguồn mở được lưu trên trên GitHub và cho 100 bản build đầu tiên khác. Có một vài kế hoạch về việc lựa chọn giá, sự khác biệt chính là số lượng các bản build bạn có thể đồng thời chạy cùng 1 lúc.
    - Cho phép kiểm tra trên hệ điều hành Mac và linux cùng 1 lúc.
    - Thiết lập dễ dàng và nhanh chóng.
- Sẽ phù hợp nếu:
    - Code lưu trên github.
    - Cần hỗ trợ nhiều ngôn ngữ khác nhau (hơn 20 ngôn ngữ).
    - Không dùng window.
    - Cần 1 giải pháp linh hoạt.
    - Cần các máy chủ cơ sở dữ liệu được cài sẵn.
    - Không yêu cầu nhiều tích hợp từ bên thứ 3.
- ***Đánh giá :*** Là giải pháp tốt cho cả máy chủ và biến thể On-premises, được rất nhiều team yêu thích.
## **7) Tekton**
- Trang chủ : https://tekton.dev/

    <img src=https://i.imgur.com/qneStJA.png>

- **Tekton** là một giải pháp cloud-native dùng để build các pipeline. Nó bao gồm **Tekton pipeline**, cung cấp các building block và các thành phần hỗ trợ, chẳng hạn như **Tekton CLI** và **Tekton Catalog**, khiến cho **Tekton** trở thành một hệ sinh thái hoàn chỉnh.
- **Tekton** là một phần của **CD Foundation**, một dự án của **Linux Foundation**.
- **Tekton** sẽ được cài đặt và chạy như một extension trên **Kubernetes cluster** và bao gồm một **Kubernetes Custom Resources** để định nghĩa các building block có thể tạo và tái sử dụng cho pipeline.
- Một khi được cài đặt, **Tekton pipeline** sẽ có thể truy cập thông qua `kubectl` và thông qua API call, giống như **pod** và các resource khác.
- Hiện tại, **Tekton** được sử dụng như core của **Openshift Pipeline**.