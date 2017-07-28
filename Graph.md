#图形
[TOC]
------
##初始化图形函数
```c
	// 函数原型
	void initgraph(int *graphdiver,int *graphmode, char *pathtodriver);
	
	enum graphics_drivers {     /* define graphics drivers */
    	DETECT,         /* requests autodetection */
    	CGA, MCGA, EGA, EGA64, EGAMONO, IBM8514,    /* 1 - 6 */
    	HERCMONO, ATT400, VGA, PC3270,          /* 7 - 10 */
    	CURRENT_DRIVER = -1
	};

	enum graphics_modes {       /* graphics modes for each driver */
    	VGALO      = 0,  /* 640x200 16 color 4 pages    */
    	VGAMED     = 1,  /* 640x350 16 color 2 pages    */
    	VGAHI      = 2,  /* 640x480 16 color 1 page     */
    	PC3270HI   = 0,  /* 720x350 1 page          */
    	IBM8514LO  = 0,  /* 640x480 256 colors      */
    	IBM8514HI  = 1   /*1024x768 256 colors      */
	};
	// 一般调用形式
	int gd = VGA, gm = VGAHI;
	initgraph(&gd, &gm, "C:\\bc31\\bgi");
	// 让图形系统在初始化时有程序自动侦测显示卡的最高显示模式
	int gd = DETECT,gm;
	initgraph(&gd,&gm,"");
```

##图形系统关闭函数
```c
	//函数原型
	void closegraph(void);
	// 将图形模式切换至文本模式函数
	void far restorecrtmode(void);
```

##设置画笔当前颜色及屏幕背景色
```c
	void setcolor(int color);   // 设置当前画笔颜色
	void setbcolor(int color);  // 设置屏幕背景色
	enum COLORS {
    	BLACK,          /* dark colors */
    	BLUE,
    	GREEN,
    	CYAN,
    	RED,
    	MAGENTA,
    	BROWN,
    	LIGHTGRAY,
    	DARKGRAY,           /* light colors */
    	LIGHTBLUE,
    	LIGHTGREEN,
    	LIGHTCYAN,
    	LIGHTRED,
    	LIGHTMAGENTA,
    	YELLOW,
    	WHITE
	};
```

## 画点及获取屏幕点的颜色
```c
	void putpixel(int x,int y,int color);//向指定坐标(x,y)处画一个给定颜色的点
	unsigned getpixel(int x,int y);      //获取(x,y)点的颜色
```

##设置线性及画直线
```c
	void setlinestyle(int linestyle,unsigned user_pattern,int thickness);
	
	enum line_styles {      /* Line styles for get/setlinestyle */
    	SOLID_LINE   = 0,
    	DOTTED_LINE  = 1,
    	CENTER_LINE  = 2,
    	DASHED_LINE  = 3,
    	USERBIT_LINE = 4,   /* User defined line style */
	};
	enum line_widths {      /* Line widths for get/setlinestyle */
    	NORM_WIDTH  = 1,
    	THICK_WIDTH = 3,
	};
	
	// 画直线相关函数
	void line(int x1,int y1,int x2,int y2);
	void lineto(int x,int y);
	void moveto(int x,int y);
```

##画圆，椭圆，矩形及多边形
```c
	void circle(int x,int y,int radius); //圆
	void ellipse(int x,int y,int stangle,int endangle,int xradius,int yradius); //椭圆
	void rectangle(int left,int top,int right,int bottom); //矩形
	void drawpoly(int numpoints,int *polypoingts); //多边形
	// 一般调用形式
	circle(100,80,30);
	ellipse(150,100,0,180,40,30)；
	rectangle(10,20,80,50)；
	int v[] = {50,10,100,10,120,60,30,20,50,10};
	drawpoly(5,v);
```

##填充图形函数
```c
	//设置填充模式和填充颜色函数
	void setfillpattern(char* upattern,int color);
	void setfillstyle(int pattern,int color);
	
	enum fill_patterns {        /* Fill patterns for get/setfillstyle */
    	EMPTY_FILL,     /* fills area in background color */
    	SOLID_FILL,     /* fills area in solid fill color */
    	LINE_FILL,      /* --- fill */
    	LTSLASH_FILL,       /* /// fill */
    	SLASH_FILL,     /* /// fill with thick lines */
    	BKSLASH_FILL,       /* \\\ fill with thick lines */
    	LTBKSLASH_FILL,     /* \\\ fill */
    	HATCH_FILL,     /* light hatch fill */
    	XHATCH_FILL,        /* heavy cross hatch fill */
    	INTERLEAVE_FILL,    /* interleaving line fill */
    	WIDE_DOT_FILL,      /* Widely spaced dot fill */
    	CLOSE_DOT_FILL,     /* Closely spaced dot fill */
    	USER_FILL       /* user defined fill */
	};
	
	//填充制定区域函数
	void floodfill(int x, int y, int border);
	
	// 一般调用形式
	setcolor(GREEN);
	circle(80,60,30);
	floodfill(80,63,RED);
	
	//填充矩形、多边形、椭圆、圆和扇形相关的函数
	void var(int left, int top, int right, int bottom);
	void fillpoly(int numpoints,int *poolypoints);
	void fillellipse(int x, int y, int xradius, int yradius);
	void pieslice(int x, int u, int stangle, int endagle, int radius)；
	void sector(int x, int y, int stangle, int endangle, int xradius, int yradius);
```

#图形方式下的文本常见操作函数
##视口操作函数
```c
	void far setviewpoint(int left, int top, int right, int bottom, int clip); // clip当绘制图形越过视口边界时是否对其进行裁剪。非0则裁剪。
	void far getviewport(struct viewporttype *viewport);
	void far clearviewport(void);
```

##图形方式下的文字输出
```c
	settextstyle(int font,int direction,int charsize);
	// 文本操作函数
	void outtext(char*textstring);
	void outtextxy(int x, int y, char *textstring);
	
	enum font_names {
    	DEFAULT_FONT    = 0,    /* 8x8 bit mapped font */
    	TRIPLEX_FONT    = 1,    /* "Stroked" fonts */
    	SMALL_FONT  = 2,
    	SANS_SERIF_FONT = 3,
    	GOTHIC_FONT = 4,
    	SCRIPT_FONT = 5,
    	SIMPLEX_FONT = 6,
    	TRIPLEX_SCR_FONT = 7,
    	COMPLEX_FONT = 8,
    	EUROPEAN_FONT = 9,
    	BOLD_FONT = 10
	};
	#define HORIZ_DIR   0   /* left to right */
	#define VERT_DIR    1   /* bottom to top */
```

##屏幕的保存和恢复
```c
	// 屏幕保存至指定内存中
	getimage(int left, int top, int right, int bottom, void *bitmap);
	// 计算保存图形所需要的储存空间
	imagesize(int left, int top, int right, int bottom);
	// 恢复函数getimage保存的函数,并将其显示带屏幕上去
	putimage(int left, int top, void *bitmap, int op);
	
	enum putimage_ops {     /* BitBlt operators for putimage */
    	COPY_PUT,       /* MOV */
    	XOR_PUT,        /* XOR */
    	OR_PUT,         /* OR  */
    	AND_PUT,        /* AND */
    	NOT_PUT         /* NOT */
	};
```