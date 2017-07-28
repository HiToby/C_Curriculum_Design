#文件
[TOC]
--------
##文件类型指针
```c
	typedef struct  {
        int             level;          /* fill/empty level of buffer */
        unsigned        flags;          /* File status flags          */
        char            fd;             /* File descriptor            */
        unsigned char   hold;           /* Ungetc char if no buffer   */
        int             bsize;          /* Buffer size                */
        unsigned char   _FAR *buffer;   /* Data transfer buffer       */
        unsigned char   _FAR *curp;     /* Current active pointer     */
        unsigned        istemp;         /* Temporary file indicator   */
        short           token;          /* Used for validity checking */
}       FILE; 
```

##文件打开函数
```c
	// 函数原型
	FILE *fopen(const char *filename,const char *mode);
	// 调用一般形式
	FILE *fp;
	if ((fp = fopen("c:\\config.sys","r")) == NULL) 
	// 可以使用相对路径“ccbp.bat”
	// 文件使用方式见课本P249
```

##文件关闭函数
```c
	//一般调用形式
	fclose(fp);
	//正常关闭返回0值，有错误发生返回非0值。
```

##数据块读/写函数
```c
	// 函数原型
	size_t fread(void *ptr,size_t size,size_t n,FILE *stream);
	size_t fwrite(const void *ptr,size_t size,size_t n,FILE *stream);
```

##格式化读/写函数
```c
	// 函数原型
	int fscanf(FILE *fp,const char *format[,address]);
	int fprintf(FILE *fp,const char *format[,address]);
	// 一般调用形式
	fscanf(fp,"%d %s",&i,s);
	fprintf(fp,"%d %c",j,ch);
```

##读/写字符函数
```c
	ch = fgetc(fp);
	fputc('a',fp);
```

##读/写字符串函数
```c
	fgets(str,n,fp); //字符串数组名，n，文件指针
    fputs("abcd",fp); //字符量，文件指针
```

## fseek 移动文件内部位置指针
```c
	fseek(文件指针,位移量,起始点);
	// 起始点相关符号见课本P252
```

## 位置指针置首函数
```c
	rewind(文件指针);
```

##文件检测函数
```c
	// 文件结束检测函数（若文件结束，返回1，否则返回0）
	feof(fp);
	// 读写文件出错检测函数（若文件读写时出错，返回1，否则返回0）
	ferror(fp);
	// 文件出错标志和文件结束标志置0函数
	clearerr(fp);
```