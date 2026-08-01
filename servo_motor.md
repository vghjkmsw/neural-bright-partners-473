# Arduino：舵机控制



## 说明

使用 Arduino 控制 SG90 舵机从 0° 到 180° 来回摆动。该项目学习 `Servo` 库的使用、PWM 信号控制角度、以及 `for` 循环的递增递减写法。



## 硬件需求

- Arduino UNO ×1

- SG90 舵机 ×1

- 跳线若干



## 电路连接

| 舵机线色 | 连接 |

|---------|------|

| 棕色 (GND) | Arduino GND |

| 红色 (VCC) | Arduino 5V |

| 橙色 (信号) | D9 |



## 代码

```cpp

#include <Servo.h>           // 引入舵机库



Servo myServo;               // 创建舵机对象

int angle = 0;               // 当前角度



void setup() {

  myServo.attach(9);         // 舵机信号线接 D9

  Serial.begin(9600);

}



void loop() {

  // 从 0° 慢慢转到 180°

  for (angle = 0; angle <= 180; angle++) {

    myServo.write(angle);    // 设定舵机角度

    Serial.print("角度: ");

    Serial.println(angle);

    delay(15);               // 给舵机转动的时间

  }



  delay(500);  // 到终点停半秒



  // 从 180° 慢慢转回 0°

  for (angle = 180; angle >= 0; angle--) {

    myServo.write(angle);

    Serial.print("角度: ");

    Serial.println(angle);

    delay(15);

  }



  delay(500);

}

```



## 教学重点

- `#include <Servo.h>` 引用外部库

- `Servo.attach(pin)` 绑定舵机到指定引脚

- `Servo.write(degree)` 设置 0~180° 角度

- `delay()` 在舵机控制中的重要性：如果不给延时，舵机来不及转动

- `for` 循环的灵活运用（递增 `++` 和递减 `--`）



## 常见错误

- 舵机卡顿抖动：USB 供电不足，建议外接电源

- 角度不对：确认 `write()` 参数在 0~180 之间

- 忘记 `delay()`：舵机需要 15~20ms 反应时间

- 多个舵机时供电不足：5V 引脚最多带 2 个小型舵机

