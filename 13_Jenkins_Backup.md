# Backup trong Jenkins
- Một việc khá quan trọng và cần thiết khi sử dụng **Jenkins** là backup data và cấu hình của nó, bao gồm  job config, các plugin, build logs, cấu hình plugin,...
- **Jenkins** cung cấp 2 phương pháp để backup :
    - Sử dụng plugin **ThinBackup**
    - Backup sử dụng **Disk Snapshots**
## **1) Backup sử dụng plugin Thin Backup**
- **ThinBackup** là một plugin phổ biến cho việc backup trong **Jenkins**. Nó sẽ backup dữ liệu dựa trên schedule và xử lý thời gian tồn tại của các bản backup.
- Các tính năng chính của plugin :
    - Full backup
    - Differential backup
    - File exclusions from Backup
    - Backup build results
    - Cleanup of differential backups
    - Archive old backups to ZIP format
> ### **Cài đặt plugin**
- **B1 :** Trên dashboard của **Jenkins** chọn **Manage Jenkins** -> **Manage Plugins** :

    <img src=https://i.imgur.com/ImdoeAf.png>

- **B2 :** Tìm và cài đặt plugin **ThinBackup** :

    <img src=https://i.imgur.com/l3Hp9lw.png>

> ### **Cấu hình ThinBackup**
- **B1 :** Trên dashboard của **Jenkins** chọn **Manage Jenkins** -> **ThinBackup** :

    <img src=https://i.imgur.com/mVutED1.png>

- **B2 :** Chọn **Settings** :

    <img src=https://i.imgur.com/6NAzuno.png>

- **B3 :** Nhập các cài đặt cơ bản cho việc backup :
    - **Backup directory** : thư mục sẽ chứa các bản backup
    - **Backup schedule for full backups** : thời gian thực hiện 1 bản full backup (cú pháp tương tự với cronjob)
    - **Backup schedule for diffirential backups** : thời gian thực hiện 1 bản diffirential backup (cú pháp tương tự với cronjob)
    - **Max number of backup sets** : số bản backup sẽ giữ lại
    - Lựa chọn các loại backup cần thực hiện
    - Chọn ***Save*** để lưu lại cấu hình :

    <img src=https://i.imgur.com/ku1GOUG.png>

- **B4 :** Có thể chủ động backup mà không cần chờ đến cronjob. Chọn **Backup Now** :

    <img src=https://i.imgur.com/PcXKhF9.png>

- **B5 :** Kiểm tra các bản backup đã tạo trong terminal :

    <img src=https://i.imgur.com/SnFMrw7.png>

- **B6 :** Để restore lại bản backup, chọn **Restore** :

    <img src=https://i.imgur.com/VzMabi5.png>

- **B7 :** Chọn bản backup muốn restore -> ***Restore*** :

    <img src=https://i.imgur.com/DAoUwq6.png>

## **2) Backup sử dụng Disk Snapshots**
- **Jenkins** hoạt động không sử dụng database. Tất cả các cấu hình đều được lưu trữ dưới dạng file trong thư mục `/var/lib/jenkins`.
- Tất cả các nền tảng private hoặc public cloud hiện đại hiện nay đều hỗ trợ tính năng **disk snapshot**.
- Những việc cần làm nếu môi trường hỗ trợ **disk snapshot** :
    - Đính kèm external disk vào Jenkins server
    - Mount disk vào một folder trên server, giả sử là `/jenkins_data`.
    - Nếu đã có dữ liệu trước đó, copy toàn bộ dữ liệu từ thư mục `/var/lib/jenkins` tới `/jenkins_data`.
    - Set symlink `/var/lib/jenkins` tới `/jenkins_data`.
    - Khởi động lại **Jenkins** để xem **Jenkins** có đang sử dụng disk mới hay không.
    - Sau đó, có thể tạo snapshot của external disk. Đây được coi là thực hiện 1 backup point.
- Nếu đang sử dụng **AWS**, có thể sử dụng tính năng **EBS snapshot automation** để backup tự động Jenkins data disk.
- Ngoài ra, nếu đang sử dụng **Kubernetes**, có thể backup persistent volume.
- Tuy nhiên, nên sử dụng kết hợp cả giải pháp **ThinBackup** và **disk snapshot**.