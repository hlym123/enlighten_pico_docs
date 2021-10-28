电机风扇 
====================================================== 

应用编程接口说明
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

	'''
	 类：电机风扇
	 参数:
		port: 端口号 -- 1~8 
	'''
	class motor_fan(port)
	
	'''
	 方法：转速设置 
	 参数:
		val: 0~100
	'''
	motor_fan.set(val)

案例
++++++++++++++++++++++++++++++++++++++++++++++++++++++

**1. 调速风扇**
::
            
    import time 
    from openaie import *
        
    p = potentiometer(3) # 电位器连接 端口3   
    m = motor_fan(6)     # 电机风扇模块连接 端口6  

    while True:
        val = p.read()
        print("speed: %d%%"%val)
        m.set(val)
        time.sleep_ms(50)
