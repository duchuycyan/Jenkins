# Metrics trong Jenkins
## **1) Metrics**
- **Jenkins** cung cấp nhiều plugin để hiển thi các metrics cho các bản build được thực hiện trong một khoảng thời gian. Các metrics này sẽ rất hữu ích khi xem tổng quan về bản build và có thể hiểu được tần suất build pass/fail trong một khoảng thời gian.
- Cần cài đặt plugin **Build History Metrics** để hiển thị các build metrics :

    <img src=https://i.imgur.com/Rsvwhoz.png>

- Các metric build thu thập được :
    - **MTTF** (Metrics Time to Failure) - thời gian build fail
    - **MTTR** (Mean Time to Recovery) - thời gian phục hồi trung bình
    - **Standard Deviation of Build Times** - độ lệch chuẩn của thời gian build

    <img src=https://i.imgur.com/N7BesVb.png>