计算机图形学
	图形的裁剪和几何变换
		4.1二维坐标系统
			设备坐标系，二维坐标系
		4.2 窗口-视图区的变换
			窗口是在世界坐标系里指定的一个矩形区域
			视区是用户在设备坐标系中定义的一个矩形区域
				二者转换，需要进行数学变换
				sx、sy 表示缩放比例：sx = sy = 1 ，a = b = 0
				NDC 变换到 DC
		4.3二维图形的裁剪
			直线裁剪算法
				编码算法
					先判定一条直线端是否全部位于窗口内或外
						*给地图划分区间，然后判定端点，进行逻辑运算*
					四位代码的含义
				中点算法
				梁-Barsky算法
			多边形裁剪算法
				逐次多边形裁剪算法
		4.4二维图形的几何变换
		4.5三维图形的几何变换
		4.6投影变换
		