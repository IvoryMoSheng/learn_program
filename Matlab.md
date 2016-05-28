	function  自定义函数
	clear 清理定义的变量
	close all 关闭窗口
	cls 清理命令屏
	figure 命名图
	plot 画点
	grid on 画出网格

---
	//同时画两个图，并打开两个画图窗口，避免前一个图被覆盖
	t=   ;
	x1=		;
	x2=		;
	figure(1)
	plot(t,x1);
	figure(2)   //figure()默认为figure(2)
	plot(t,x2);

---
		  '-s' 表示方格
          '-p' 表示五角星
          '-d' 表示菱形
          '-h' 表示六角形
          '-+' 表示用加号
          '-o' 表示用圈
          '-*' 表示星号
