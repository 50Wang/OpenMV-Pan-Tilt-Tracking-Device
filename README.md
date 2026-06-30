# OpenMV-Pan-Tilt-Tracking-Device
基于stm32f103c8t6和OpenMV4 H7PLUS的跟踪云台。/A tracking pan-tilt based on STM32F103C8T6 and OpenMV4 H7PLUS.

# 硬件准备
stm32f103c8t6核心板、OpenMV4H7PLUS(OV5460) + 1.8寸LCD扩展板、二维舵机云台打印件(stl)、sg90舵机两个

# 注意事项
当运行 find_face.py/main.py 时，不使用stm32，openmv直接控制舵机
openmv      sg90
  P7 ------ PWM1
  P8 ------ PWM2
  GND ------ GND         
  VCC ------ VCC 
  
# 连线（运行 openmv.py 时）
stm32     openmv       stm32       sg90
PA10 ------ P4          PA0 ------ PWM1
PA9  ------ P5          PA1 ------ PWM2
GND  ------ GND         GND ------ GND
5V   ------ VCC         5V  ------ VCC

# 代码程序
OpenMV IDE
先把 pid.py 拷贝到 OpenMV 的根目录
find_face.py: 从识别到的多个人脸中挑出“最大的”一个，计算其中心点与画面中心的偏移量，通过 PID 算法驱动云台实时跟随人脸
main.py: 寻找画面中最大的指定色块（默认红色），计算坐标偏移，并利用 PID 控制舵机使摄像头对准色块
lcd.py: 基础 LCD 预览脚本，用于测试显示功能
openmv.py: 识别特定色块（绿色瓶盖），并将质心坐标通过串口发送给其他设备

keil
根据 openmv.py 实时接收到的质心坐标，使用PID控制两个舵机的角度，使质心一直保持在图像中心附近






