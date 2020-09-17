# CAN_demo
    stm32 CAN bus Tx/Rx Example。
    stm32的CAN总线简单例程，裸机例程。
    需要两块板子，一个发送，一个接收，CAN总线模式为普通模式。

## 发送板

    发送板每5ms发送一帧数据，数据帧，标准帧，ID为0x320, 数据长度3字节。

## 接收板

    接收板使用中断模式接收数据，未开CAN过滤器，接收左右CAN消息。

    接收到数据时，进入中断回调函数。
    在回调函数中，首先LED0熄灭，用全局变量CAN_RxMessage_time储存当前uwTick；
    当接收到标准帧，ID为0x320，数据长度为3字节的数据时，LED1点亮，用全局变量led_time储存当前uwTick。

    在主循环中，用三个临时变量，储存当前的uwTick、CAN_RxMessage_time、led_time。
    计算CAN总线接收时间间隔，若大于1s，即在1s内未收到任何CAN消息，LED0点亮。
    计算LED1点亮时间间隔，若大于1s，即在1s内未收到对应CAN消息，LED1熄灭。
