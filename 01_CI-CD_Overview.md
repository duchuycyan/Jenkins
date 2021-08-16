# Tổng quan về CI/CD
## **1) CI là gì?**
- **CI - *Continuous Integration*** là phương pháp phát triển phần mềm yêu cầu các thành viên của team tích hợp công việc của họ thường xuyên, mỗi ngày ít nhất một lần. Mỗi tích hợp được "`build`" tự động (bao gồm cả `test`) nhằm phát hiện lỗi nhanh nhất có thể. Cả team nhận thấy rằng cách tiếp cận này giảm thiểu vấn đề tích hợp và cho phép phát triển phần mềm nhanh hơn.

    <p align=center><img src=https://i.imgur.com/wTpkgu4.png></p>

- Một kịch bản **CI** bắt đầu bằng việc developer `commit` code lên repository (**GitHub** chẳng hạn). Bất kỳ thay đổi nào cũng sẽ trigger một vòng đời **CI**. Các bước trong một kịch bản **CI** thường như sau:
    - Đầu tiên, developer `commit` code lên repo.
    - **CI server** giám sát repo và kiểm tra xem liệu có thay đổi nào trên repo hay không (liên tục, chẳng hạn mỗi phút 1 lần)
    - Ngay khi `commit` xảy ra, **CI server** phát hiện repo có thay đổi, nên nó nhận code mới nhất từ repo và sau đó `build`, chạy `unit` và `integration test`.
    - **CI server** sẽ sinh ra các feedback và gửi đến các member của project.
    - **CI server** tiếp tục chờ thay đổi ở repo.
- Mỗi lần developer làm xong task, họ phải chạy một `private build` (tức là chạy phần mềm trên local trước), check cẩn thận và `commit` code lên repo khi đã thấy ổn. Bước này xảy ra thường xuyên và ở bất kỳ thời điểm nào trong ngày. Việc `build` tích hợp sẽ không xảy ra khi những thay đổi này chưa ảnh hưởng đến repo (kiểu như bạn `commit` mà chưa được `merge` vậy).
- Một trong những tuyên ngôn của **CI** là "***Build Software at Every Change***". Vấn đề sẽ được tìm ra sớm bằng cách `build` thường xuyên, và để **CI** hoạt động hiệu quả trong project, tốt nhất là developer phải `commit` code thường xuyên hơn. Đợi hơn một ngày để `commit` code lên repo có thể khiến việc tích hợp tốn thời gian và code mình dùng có thể không phải là code mới nhất.
- Lợi ích của việc sử dụng **CI** :
    - Giảm thiểu rủi ro nhờ việc phát hiện lỗi và fix sớm, tăng chất lượng phần mềm nhờ việc tự động `test` và `inspect` (đây cũng là một trong những lợi ích của CI, code được `inspect` tự động dựa theo config đã cài đặt, đảm bảo coding style, chẳng hạn một function chỉ được dài không quá 10 dòng code ...)
    - Giảm thiểu những quy trình thủ công lặp đi lặp lại (build css, js, migrate, test...), thay vì đó là build tự động, chạy test tự động.
    - Sinh ra phần mềm có thể deploy ở bất kì thời gian, địa điểm.
## **2) CD là gì?**
- Trong khi **Continuous Integration** là quy trình để `build` và `test` tự động, thì **Continuous Delivery** (tạm dịch là *chuyển giao liên tục*) lại nâng cao hơn một chút, bằng cách triển khai tất cả thay đổi về code (đã được `build` và `test`) đến môi trường **testing** hoặc **staging**. **Continuous Delivery** cho phép developer tự động hóa phần testing bên cạnh việc sử dụng `unit test`, kiểm tra phần mềm qua nhiều thước đo trước khi triển khai cho khách hàng (**production**). Những bài test này bao gồm UI testing, load testing, integration testing, API testing... Nó tự động hoàn toàn quy trình release phần mềm.

    <p align=center><img src=https://i.imgur.com/E0a6dwa.png></p>

- **Continuous Delivery** được thực hiện bằng cách sử dụng **Deployment Pipeline**.
- **Deployment Pipeline** chia quy trình chuyển giao phần mềm thành các giai đoạn. Mỗi giai đoạn có mục tiêu xác minh chất lượng của các tính năng mới từ một góc độ khác nhau để kiểm định chức năng và tránh lỗi ảnh hưởng đến người dùng. **Pipeline** sẽ cung cấp phản hồi cho nhóm trong việc cung cấp tính năng mới. Ở góc độ trừu tượng hơn, **deployment pipeline** là quy trình để chuyển phần mềm từ version control đến tay người dùng. Mỗi thay đổi đến phần mềm sẽ đi qua một quy trình phức tạp để được phát hành.
- Có một khái niệm nữa là **Continuous Deployment**, và hai khái niệm này thường hay bị nhầm lẫn với nhau. Nếu **Continuous Delivery** là triển khai code lên môi trường **staging**, và deploy thủ công lên môi trường **production**, thì **Continuous Deployment** (cũng viết tắt là **CD**) lại là kỹ thuật để triển khai code lên môi trường **production** một cách tự động, và cũng nên là mục tiêu của hầu hết công ty.

    <p align=center><img src=https://i.imgur.com/Xx6RtDe.png></p>

- Về cơ bản thì môi trường **staging** là môi trường giống với **production**, nên đã làm **Continous Delivery** được thì cũng làm **Continous Deployment** được. Tuy nhiên, thực tế lại không dễ dàng như vậy. Lý do thứ nhất là chúng ta có thể `deploy` tự động lên **staging**, nhưng liệu chúng ta có dám `deploy` tự động với **production**, cho dù là mọi cấu hình đều giống nhau thì thực tế **staging** và **production** server vẫn là hai server riêng biệt, và vì thế không thể đảm bảo mọi thứ chạy đúng trên **staging** sẽ chạy đúng trên **production**, thế nên `deploy` lên **production** thường phải làm thủ công để chắc chắn là các bước `build`, `test` được thực hiện chính xác. Lý do thứ hai đơn giản hơn, đó là rất khó để `test` tự động hoàn toàn, và bởi vậy khó mà tự động `deploy` được.
- Dù **Continous Deployment** có thể không phù hợp với mọi công ty, nhưng **Continuous Delivery** thì tuyệt đối là yêu cầu cho việc thực hiện triết lý **DevOps**. Chỉ khi code được chuyển giao liên tục, chúng ta mới có thể tự tin rằng những thay đổi từ code sẽ phục vụ cho khách hàng sau chỉ vài phút với một nút ấn.

    <p align=center><img src=https://i.imgur.com/plq2c3a.png></p>


