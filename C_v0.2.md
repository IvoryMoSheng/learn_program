	/*the first C programme */	
	/*helloword.c*/
	#includ<stdio.h>            //包含标准输入输出头文件
	main()						//主函数
	{
		printg("Hello,world.\n");	//打印输出信息
	}

---
	/*运行多个源文件，没有理解*/
	/*helloword.c*/
	#include "print.h"
	
	int main(void)
	{
		printHello();
		return 0;
	}
	/*print.c*/
	#include "print.h"
	
	void printHello()
	{
		printf("hello world!\n");
	}
	
	/*print.h*/
	#include "stdio.h"
	
	void printHello(void);

---
	/*求整数之积*/
	/* Input two numbers, output the product */
	#include <stdio.h>
	main()
	{
		int x,y,m;				/* 定义整型变量x，y，m */
		printf("Please input x and y\n");	/* 输出提示信息 */
		scanf("%d%d",&x,&y);			/* 读入两个乘数，赋给x，y变量 */
		m=x*y;					/* 计算两个乘数的积，赋给变量m */
		printf("%d * %d = %d\n",x,y,m);		/* 输出结果 */
	}

---
	/* 输入两个浮点数，输出它们中的大数 */
	#include <stdio.h>
	main()
	{
		float x,y,c;				/* 变量定义 */
		printf("Please input x and y:\n");	/* 提示用户输入数据 */
		scanf("%f%f",&x,&y);
		c=x>y?x:y;				/* 计算c=max(x,y) */
		printf("MAX of (%f,%f) is %f",x,y,c);	/* 输出c */
	}

---
	/* 字符的输出，没有理解*/
	#include <stdio.h>
	main()
	{
		char ch,nch;	/* */
		int count;	/* */
		int k;		/* */
	
		printf("Please input a string with a # in the end.\n");
		scanf("%c",&ch);	/* */
		while(ch != '#')	/* */
		{
			if(ch >= '0' && ch <= '9')
			{
				/* */
				count = ch-'0'+1;	/* */
				scanf("%c",&nch);	/* */
				for(k=0;k<count;k++)	/* */
					printf("%c",nch);
			}
			else
				printf("%c",ch);	/* */
			printf(" ");			/* */
			scanf("%c",&ch);		/* */
		}
		printf("#\n");				/* */
	}

---
	/* 输出不同类型所占的字节数*/
	#include <stdio.h>
	int a = 3;
	void main()
	{
	    /* sizeof()是保留字，它的作用是求某类型或某变量类型的字节数, */
	    /* 括号中可以是类型保留字或变量。*/
	    /*int型在不同的机器，不同的编译器中的字节数不一样,*/
	    /*一般来说在TC2.0编译器中字节数为2,在VC编译器中字节数为4 */
	    printf("The bytes of the variables are:\n");
	    printf("int:%d bytes\n",sizeof(int));
	    /* char型的字节数为1 */
		printf("int:%d bytes\n",sizeof(a));
		/*变量a的字节数为1*/
	    printf("char:%d byte\n",sizeof(char));
	    /* short型的字节数为2 */
	    printf("short:%d bytes\n",sizeof(short));
	    /* long型的字节数为4 */
	    printf("long:%d bytes\n",sizeof(long));
	    /* float型的字节数为4 */
	    printf("float:%d bytes\n",sizeof(float));
	    /* double型的字节数为8 */
	    printf("double:%d bytes\n",sizeof(double));
	    /* long double型的字节数为8或10或12 */
	    printf("long double:%d bytes\n",sizeof(long double));
	    getchar();
	
	}

---
	/*自增自减运算，没有理解*/
	#include <stdio.h>
	main()
	{
		int a=5,b,c,i=10;
		b=a++;
		c=++b;
	
		printf("a = %d, b = %d, c = %d\n",a,b,c);
		printf("i,i++,i++ = %d,%d,%d\n",i,i++,i++);
		printf("%d\n",++i);
		printf("%d\n",--i);
		printf("%d\n",i++);
		printf("%d\n",i--);
		printf("%d\n",-i++);
		printf("%d\n",-i--);
		getchar();
	}

---
	/*数列求和*/
	#include <stdio.h>
	main()
	{
		int i,j,n;
		long sum=0,temp=0;
	
		printf("Please input a number to n:\n");
		scanf("%d",&n);
		if(n<1)
		{
			printf("The n must no less than 1!\n");
			return;
		}
	
		for(i=1;i<=n;i++)
		{	
			temp=0;
			for(j=1;j<=i;j++)
				temp+=j;
			sum+=temp;
		}
		printf("The sum of the sequence(%d) is %d\n",n,sum);
		getchar();
		getchar();
	}

---
	/*乘法口诀表，没有理解*/
	#include <stdio.h>
	#include <conio.h>
	void main(void)
	{
		int i,j,x,y;
		clrscr();
		printf("\n\n  * * * ³Ë·¨¿Ú¾÷±í * * * \n\n");
		x=9;
		y=5;
		for(i=1;i<=9;i++)
		{
			gotoxy(x,y);
			printf("%2d ",i);
			x+=3;
		}
		x=7;
		y=6;
		for(i=1;i<=9;i++)
		{
			gotoxy(x,y);
			printf("%2d ",i);
			y++;
		}
		x=9;
		y= 6;
		for(i=1;i<=9;i++)
		{
			for(j=1;j<=9;j++)
			{
				gotoxy(x,y);
				printf("%2d ",i*j);
				y++;
			}
			y-=9;
			x+=3;
		}
		printf("\n\n");
	}

---
	/*猜数字游戏，没有理解*/
	#include <stdio.h>
	#include <conio.h>
	void main()
	{
		int Password=0,Number=0,price=58,i=0;
		clrscr();
		printf("\n====This is a Number Guess Game!====\n");
		while( Password != 1234 )
		{
			if( i >= 3 )
				return;
			i++;
			puts("Please input Password: ");
			scanf("%d",&Password);
		}
	
		i=0;
		while( Number!=price )
		{
			do{
				puts("Please input a number between 1 and 100: ");
				scanf("%d",&Number);
				printf("Your input number is %d\n",Number);
			}while( !(Number>=1 && Number<=100) );
			if( Number >= 90 )
			{
				printf("Too Bigger! Press any key to try again!\n");
			}
			else if( Number >= 70 && Number < 90 )
			{
				printf("Bigger!\n");
			}
			else if( Number >= 1 && Number <= 30 )
			{
				printf("Too Small! Press any key to try again!\n");
			}
			else if( Number > 30 && Number <= 50 )
			{
				printf("Small! Press any key to try again!\n");
			}
			else
			{
				if( Number == price )
				{
					printf("OK! You are right! Bye Bye!\n");
				}
				else if( Number < price )
				{
					printf("Sorry,Only a little smaller! Press any key to try again!\n");
	
				}
				else if( Number > price )
					printf(" Sorry, Only a little bigger! Press any key to try again!\n");
			}
			getch();
		}
	}
	
