# 2021-04-05
结构中的结构

1、结构数组
#include<stdio.h>

struct time {
	int hour;
	int minutes;
	int seconds;
}; 

struct time timeUpdate(struct time now);

int main(int argc,char const *argv[])
{
	struct time testTimes[5] = {
		{11,59,59}, {12,0,0}, {1,29,59}, {23,59,59}, {19,12,27}
	};
	int i;
	
	for (i=0 ; i<5 ; i++)
	{
		printf("Time is %.2d:%.2d:%.2d",
		testTimes[i].hour,testTimes[i].minutes,testTimes[i].seconds);
		
		testTimes[i] = timeUpdate(testTimes[i]);
		
		printf("... one second later it's %.2d:%.2d:%.2d\n",
		testTimes[i].hour,testTimes[i].minutes,testTimes[i].seconds);		
	}
	
	return 0;
}

struct time timeUpdate(struct time now)
{
	now.seconds++;
	if (now.seconds == 60)
	{
		now.seconds = 0;
		now.minutes++;
		
		if (now.minutes == 60)
		{
			now.minutes = 0;
			now.hour++;
			
			if (now.hour == 24)
			{
				now.hour = 0;
			}
		}
	}
	return now;
}

2、结构数组中的元素还是结构
#include<stdio.h>

struct point {
	int x;
	int y;
};

struct rectangle {
	struct point p1;
	struct point p2;
};

void printRect(struct rectangle r)
{
	printf("<%d, %d> to <%d, %d>\n",r.p1.x,r.p1.y,r.p2.x,r.p2.y);
}

int main(int argc,char const *argv[])
{
	int i;
	struct rectangle rects[] = {
		{{1,2}, {3,4}},
		{{5,6}, {7,8}},
	}; // 2rectangles
	for (i=0 ; i<2 ; i++)
	{
		printRect(rects[i]);
	 } 
	return 0;
}
