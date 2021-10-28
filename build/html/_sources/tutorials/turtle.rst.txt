海龟画图 
======================================================

待更新！！！==========================================


画太阳花
++++++++++++++++++++++++++++++++++++++++++++++++++++++
::

    import time
    from openaie import turtle 

    turtle = turtle() 

    turtle.penup()
    turtle.goto(-100, -8)
    turtle.pendown()
    turtle.pencolor(255,255,0)
    for i in range(50): 
        turtle.forward(20s0)
        turtle.left(170) 
        time.sleep_ms(100)    


画五角星
++++++++++++++++++++++++++++++++++++++++++++++++++++++
正五边形的内角为(n-2)*180/n = (5-2)*180/5 = 108°，五角星角的夹角为36°
 
::

    import math, time 
    from openaie import turtle

    turtle = turtle() 

    len = 160    
    turtle.clear()
    turtle.penup()
    turtle.goto(40, 50)
    turtle.pendown()
    #turtle.write("五角星")
    turtle.penup()
    turtle.goto(0, 0)
    turtle.pencolor(255,255,0)
    turtle.goto(-(len*math.cos(math.radians(36))-len/2), -len*math.sin(math.radians(72))/2)
    turtle.pendown()
    turtle.left(36)
    for i in range(5): 
        turtle.forward(len)
        turtle.left(144)
        time.sleep_ms(500)  


画正多边形
++++++++++++++++++++++++++++++++++++++++++++++++++++++        

::

    # 正多边形  https://www.cnblogs.com/youthlion/archive/2012/02/23/2365381.html
    # https://blog.csdn.net/qq_18617299/article/details/93909169
    import time
    from openaie import turtle 

    turtle = turtle() 

    NUM = 6  # 边
    L = 50   # 边长
    turn_angle = (NUM-2)*180/NUM # 内角
    turtle.clear()
    turtle.pensize(5)
    turtle.pencolor(255,0,0)
    for i in range(NUM): 
        turtle.forward(L)
        turtle.left(180-turn_angle) 
        time.sleep_ms(500)    

        
画树 树的颜色根据启蒙板的姿态变化而改变 
++++++++++++++++++++++++++++++++++++++++++++++++++++++ 

::

    import time
    from openaie import turtle, imu 

    turtle = turtle() 
     
    '''
     数值映射
     @param in_min, in_max 输入区间
     @param out_min, out_max 输出区间
    '''
    def math_map(input, in_min, in_max, out_min, out_max):
        output = (input-in_min)*(out_max-out_min)/(in_max-in_min) + out_min # 距离缩放 + 偏差
        return output

    def draw_colorful_tree(branch_len):    
        x = imu.read_accel('x')
        y = imu.read_accel('y')
        z = imu.read_accel('z')
        r = int(math_map(x, -9.8, 9.8, 0, 255))
        g = int(math_map(y, -9.8, 9.8, 0, 255))
        b = int(math_map(z, -9.8, 9.8, 0, 255))
        turtle.pencolor(r, g, b)
        if branch_len>5:
            turtle.forward(branch_len)
            turtle.right(20)
            draw_colorful_tree(branch_len-15)
            turtle.left(40)
            draw_colorful_tree(branch_len-10)
            turtle.right(20)
            turtle.backward(branch_len)
            
    turtle.clear()
    while True:
        turtle.reset()
        turtle.left(90)
        turtle.penup()
        turtle.pensize(3)
        turtle.backward(120)
        turtle.pendown()
        draw_colorful_tree(70)     
    

    
绘制科赫雪花 按键切换科赫雪花阶数
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    import time
    from openaie import turtle 

    turtle = turtle() 

    def draw_koch(size, n):
        if n==0:
            turtle.forward(size)
        else:
            for angle in [0, 60, -120, 60]:
                turtle.left(angle)
                draw_koch(size/3, n-1)

    def koch_curve(n):
        turtle.clear()
        #turtle.invisible() # 画图过程不显示，提高显示速度
        turtle.penup()
        turtle.goto(-100, 60)
        turtle.pencolor(255,255,255)
        turtle.pendown()
        level = n # 科赫雪花阶数
        draw_koch(200, level)
        turtle.right(120)
        draw_koch(200, level)
        turtle.right(120)
        draw_koch(200, level)
        turtle.visible() # 更新显示 

    turtle.clear()    
    num = 1
    koch_curve(3)

