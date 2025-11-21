## Turtlebot4_navigation_pick and place ##

Proyek ini dibuat untuk memenuhi Ujian Tengah Semester, dengan tujuan mengimplementasikan sistem navigasi otonom pada Turtlebot4.
Turtlebot4 bergerak menuju lokasi pick dan mengambil barang sambil membunyikan buzzer satu kali, kemudian melanjutkan perjalanan ke lokasi place di Lobby Brail dan mengantar barang sambil membunyikan buzzer dua kali sebagai penanda.
Proyek navigasi ini dibangun menggunakan ROS 2 dan memanfaatkan stack Nav2 untuk melakukan lokalisasi, pemetaan, perencanaan jalur, eksekusi navigasi otonom.

----------------------------------------------------------------------------------------------------

# *Step Pengengerjaan proyek*
----
# 1. Buat Folder Workspace
```bash
mkdir kelompok4a_uts/src
cd kelompok4a_uts/src
```
# 2. Membuat Package dan Dependencies 
```bash
source /opt/ros/jazzy/setup.bash
ros2 pkg create --build-type ament_cmake --node-name navkel4a navkel4a --dependencies rclcpp nav2_msgs rclcpp_action tf2
```
# 3. Lalu Colcon Build
```bash
colcon build
```
Pada perintah ini melakukan kompilasi seluruh package dalam workspace, lalu menghasilkan folder install/ yang berisi executable (node), konfigurasi, dan library. Setelah menyelesaikan proses build, environment pada workspace dapat diaktifkan dengan menggunakan:
```bash
source install/setup.bash
```

# *Menghubungkan dari laptop ke Turtlebot4*
----
Koneksi menggunakan kabel LAN dapat mengatur ke IP pada komputer secara manual: (IP Address: 192.168.185.6; Netmask: 255.255.255.0; Gateway / Robot IP: 192.168.185.3).

Perintah di terminal dan jalankan SHH:
```bash
ssh ubuntu@192.168.185.3
```
Perintah ini laptop akan terhubung langsung ke turtlebot4 melalui jaringan kabel LAN. 

# *Mapping*
---
# Perinrah menjalankan SLAM 
```bash
ros2 launch turtlebot4_navigation slam.launch.py
```
# Perintah menjalankan RViz
Karena tahap ini menggunakan Ubuntu versi 24, maka jalankan versi yang jazzy dengan perintah seperti berikut: 
```bash
ros2 launch turtlebot4_viz view_navigation.launch.py
```

# *Menjalankan Nav2 (Navigasi)*
--
# 1. Navigation Node 
```bash
ros2 launch nav_kel4a run_navigation.launch.py
```
Pada Launch file ini berisi konfigurasi navigasi yang dibuat dalam package nav_kel4a, dengan mencakup parameter navigasi seperti planner, controller, dan behavior tree.
# 2. Menjalankan Localization
```bash
ros2 launch turtlebot4_navigation localization.launch.py map:=kelompok4A_uts/src/nav_kel4a/maps/kel4a.yaml
```
Perintah ini menjanlankan AMCL untuk menentukan posisi robot pada peta yang telah dibuat saat mapping. ROS2 ini akan memuat file map.yaml tersebut dan mengaktifkan bagian Nav2.

# 3. Membuka RViz 
```bash
ros2 launch turtlebot4_viz view_navigation.launch.py
```

# *Menjalankan Program 
--
# Menjalankan Node program C++ yang mengirim goal
```bash
ros2 run nav_kel4a nav_kel4a 
```
Perintah ini tahapan terakhir. Node program C++ yang telah dibuat akan:
 - Mengirim robot bergerak menuju ke lokasi Pick
 - Mengaktifkan fungsi buzzer sekali
 - Mengirim lagi robot menuju ke lokasi Place
 - Mengaktifkan fungsi buzzer dua kali
