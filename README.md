# Read-AS5600-with-micropython-I2C
Read AS5600 magnetic rotary position sensor with micropython I2C

##Usage：
```
import time
from machine import Pin,I2C,SoftI2C

# i2c = I2C(scl=Pin(22), sda=Pin(21))#ESP32默认的SCL SDA引脚
i2c = I2C(1, scl=Pin(7), sda=Pin(6))#ESP32-S3可任意定义SCL SDA引脚

while 1:
    data1=i2c.readfrom_mem(0x36, 0x0C, 1, addrsize=8)#高4位
    data2=i2c.readfrom_mem(0x36, 0x0D, 1, addrsize=8)#低8位
    val1=int(hex(data1[0]),16)#16进制转为10进制
    val2=int(hex(data2[0]),16)#16进制转为10进制
    val=val1*256+val2#读出0-4095的值
    print(val/4095*360)#转成360度
    time.sleep(0.5)
```
