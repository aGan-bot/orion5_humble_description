# orion5_humble_description

ROS 2 Humble icin Orion5 robot tanim paketi.

Bu paket, robotun URDF modelini, mesh dosyalarini ve hizli goruntuleme launch dosyasini icerir.
Ana model dosyasi: `urdf/orion5.urdf`.

## Icerik

- `urdf/orion5.urdf`: 6 eksenli robot modeli, `tool0` frame'i ve `ros2_control` bloklari
- `meshes/stl/*.stl`: gorsel/collision meshleri
- `launch/view_orion5.launch.py`: RViz + robot_state_publisher + joint_state_publisher_gui

## Ozellikler

- Zincir yapisi: `world -> base_link -> ... -> link_6 -> tool0`
- Eksen isimleri: `joint_1` ... `joint_6`
- Komut arayuzu: `effort`
- Durum arayuzleri: `position`, `velocity`, `effort`
- `ros2_control` hardware plugin referansi:
  `mujoco_pendulum::MujocoSystem`

## Gereksinimler

Asagidaki ROS 2 paketlerinin yuklu olmasi gerekir:

- `robot_state_publisher`
- `joint_state_publisher_gui`
- `rviz2`

Ornek kurulum:

```bash
sudo apt update
sudo apt install -y \
  ros-humble-robot-state-publisher \
  ros-humble-joint-state-publisher-gui \
  ros-humble-rviz2
```

## Calistirma (Robotu Goruntule)

Workspace kokunden:

```bash
colcon build --symlink-install --packages-select orion5_humble_description
source install/setup.bash
ros2 launch orion5_humble_description view_orion5.launch.py
```

## Notlar

- Bu paket robot tanim ve gorsellestirme odaklidir.
- MuJoCo simulasyon ve denetim akisi icin `mujoco_pendulum` paketini kullan.
- URDF uzerinde kinematik/dinamik guncelleme yapildiginda, MuJoCo XML tarafinin da eslenmesi gerekir.

## Gelistirme Ipuclari

- URDF dogrulama icin:

```bash
check_urdf src/orion5_humble_description/urdf/orion5.urdf
```

- Frame kontrolu icin:

```bash
ros2 run tf2_tools view_frames
```

Bu README proje ilerledikce guncellenmelidir.
