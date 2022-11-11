## inav betaflight stm32f411ceu6 (HSE_MHZ 25 (плата WeAct) )

Прошивки, target, прочее внутри [inav](./inav) и [betaflight](./betaflight)

Оригинальная прошивка тут: https://github.com/iNavFlight/inav 

## [Видео на YouTube](https://www.youtube.com/watch?v=FQCMZjob1gc)

Заметки по схеме  
* RX1/TX1: UART1  
* RX2/TX2: UART2  
* SS_RX/SS_TX: SoftSerial  
* SS_RX может использоваться как вход PPM  
* LED(WS2811): адресная светодиодная лента  
* SDA/SCL: i2c для компаса(hmc5883,QMC5883...), барометра(BMP280, BMP180...), акселерометр/гироскоп(mpu6050), ... 	  
* s1-s6:  коптер(моторы s1,s2,s3,s4 | сервы s5,s6), самолёт(моторы s1,s2 | сервы s3,s4,s5,s6)  
* VBAT: сенсор напряжения, для измерения выше 3.3 вольта нужен делитель напряжения  
* buzzer(+): выход на активную пищалку  
* USER1/USER2: pinio (переключение выхода на 0в или 3.3в)  

USER1/2, buzzer(+) не силовые выходы, и большую нагрузку не стоит подключать.  
SBUS можно подключить на любой RX, но нужен инвертор сигнала sbus (можно купить или сделать на транзисторе)

На готовой прошивке Betaflight 4.3 и выше не работают mpu6050 и bmp085/180, для поддержки следует установить более старую прошивку или собрать свою.  
На Betaflight 4.2.10 и выше могут быть проблемы с флешкой.  
Конфиги betaflight сделаны под прошивку STM32F411(target STM32_UNIFIED) для платы с чипом stm32f411ceu6.
Загружать в конфигураторе через cli.

Inav 5 не поддерживает PPM и есть проблемы с mpu6050(высокая загрузка процессора)  
В Inav 2.6.1 не работает флешка и user(pinio)  

![pinout](./%D1%81%D1%85%D0%B5%D0%BC%D0%B0.png)  
![pinout](./%D1%81%D1%85%D0%B5%D0%BC%D0%B02.png)
![pinout](./%D1%81%D1%85%D0%B5%D0%BC%D0%B03.png)
