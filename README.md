## Turtlebot4_navigation_pick and place ##

Proyek ini dibuat untuk memenuhi Ujian Tengah Semester, dengan tujuan mengimplementasikan sistem navigasi otonom pada Turtlebot4.
Turtlebot4 bergerak menuju lokasi pick dan mengambil barang sambil membunyikan buzzer satu kali, kemudian melanjutkan perjalanan ke lokasi place di Lobby Brail dan mengantar barang sambil membunyikan buzzer dua kali sebagai penanda.
Proyek navigasi ini dibangun menggunakan ROS 2 dan memanfaatkan stack Nav2 untuk melakukan lokalisasi, pemetaan, perencanaan jalur, eksekusi navigasi otonom.

----------------------------------------------------------------------------------------------------

# *Step Pengengerjaan proyek*
----
1. Buat Folder Workspace
```bash
mkdir kelompok4a_uts/src
cd kelompok4a_uts/src
```
2. Membuat Package dan Dependencies 
```bash
source /opt/ros/jazzy/setup.bash
ros2 pkg create --build-type ament_cmake --node-name navkel4a navkel4a --dependencies rclcpp nav2_msgs rclcpp_action tf2
```
3. Lalu Colcon Build
```bash
colcon build
```
Pada perintah ini melakukan kompilasi seluruh package dalam workspace, lalu menghasilkan folder install/ yang berisi executable (node), konfigurasi, dan library. Setelah menyelesaikan proses build, environment pada workspace dapat diaktifkan dengan menggunakan:
```bash
source install/setup.bash
```

# *Menghubungkan dari laptop ke Turtlebot4*

