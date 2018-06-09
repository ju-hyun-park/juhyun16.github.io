---
layout: post
title: Tin Cutter solution
subtitle: icpc.me Problem 6350.
category: [PS, ]
tags: [좌표압축, ]
---

사실 [이 문제](https://www.acmicpc.net/problem/6350)를 처음 접한 건 오래전이다.(심지어 올해가 아니다...)  
어려워서 못풀었었고, 구글링으로 [solution](https://github.com/morris821028/UVa/blob/master/volume003/308%20-%20Tin%20Cutter.cpp)을 구했으나 코드가 잘 이해되지 않았다.  
지금에야 끈기있게 코드를 분석해보았고 풀이가 이해되었다...

조금만 생각해보면 단순한 2차원 배열([][])로는 문제를 풀 수 없음을 알게된다. 내가 필요로 하는건 `Line` 이다. 

들어가기에 앞서 좌표계는 다음과 같이 사용하겠다.  
![pic3]({{site.url}}/img/pic3.png)

## 1. Unit Line

![pic1]({{site.url}}/img/pic1.png)

그럼 어떻게 주어진 입력 (y1, x1, y2, x2)을 line으로 modeling할 수 있을까? 길이 1 선분(unit line)을 생각해보자.  
(1, 4) ~ (1, 5) 분명 길이 1 가로선이다. 만약 2차원 배열에 저장을 한다면 `[1][4] = [1][5] = 1; //  marked` 이런 코드를 생각해볼 수 있을텐데 서두에 언급했듯이 2차원은 아니다.  
그래서 하나의 차원을 더 두는데 마지막에는 현재 위치에서 `동, 서, 남, 북` 으로 이동 가능함을 나타낸다.  

(1, 4) ~ (1, 5)는 `[1][4][UP] = [1-1][4][DOWN] = 1;` 이렇게 표현한다.  
(2, 2) ~ (3, 2) 이건 세로 직선이다. 이건 3차원으로 어떻게 표현될까? `[2][2][LEFT] = [2][2-1][RIGHT] = 1;` 이다.

위 그림의 빨간색 선분이 unit line 이다. 네모 한 칸이 길이 1 선분으로 모델링 되었음을 확인하라!

임의의 길이의 선분은 아래의 코드로 그려질 수 있다.

{% highlight c++ linenos %}
void drawLine(const int y1, const int x1, const int y2, const int x2){
	if(y1==y2){		//		가로선이면...
		for(int i=x1; i<x2; ++i){
			grid[UP][y1][i]=grid[DOWN][y1-1][i]=1;
		}
		return;
	}

	//		세로선이면...
	for(int i=y1; i<y2; ++i){
		grid[LEFT][i][x1]=grid[RIGHT][i][x1-1]=1;
	}
}
{% endhighlight %}

## 2. flood fill

모든 직사각형 hole을 구분짓는다. 가장 먼저 외벽을 숫자 1로 맵핑시켜두고 온전한 직사각형을 찾아서 내부를 2, 3, 4, ... 의 숫자들로 채워나간다.

flood fill 알고리즘으로 구현할 수 있다.

{% highlight c++ linenos %}
void dfs(int y, int x, const int cnt, const int sizeY, const int sizeX){
	if(y<0 || y>sizeY || x<0 || x>sizeX)	return;
	if(cover[y][x]!=0)	return;
	cover[y][x]=cnt;
	for(int i=0; i<4; ++i){
		if(grid[i][y][x]==1)	continue;
		int nextY=y+d_y[i];
		int nextX=x+d_x[i];
		dfs(nextY, nextX, cnt, sizeY, sizeX);
	}
}

int cnt=0;
dfs(0, 0, ++cnt, sizeY, sizeX);
for(int y=0; y<=sizeY; ++y){
	for(int x=0; x<=sizeX; ++x){
		if(cover[y][x]==0){
			dfs(y, x, ++cnt, sizeY, sizeX);
		}
	}
}
{% endhighlight %}

![pic2]({{site.url}}/img/pic2.png)
위와 같이 전처리해두어야 한다. 편의상 cover[y][x]에 값을 저장해두었다고 생각.

## 3. count 하기.

위의 example 처럼 직사각형이 그려졌다면 정답은 1이다. 어떻게 빨간색과 남색 직사각형 둘을 합쳐서 하나라고 count 할 수 있을까?  
일단 현재 위치를 (y, x)라고 하고 동,서,남,북 중 한 곳으로 이동하는 다음 위치는 (nextY, nextX)라고 가정하자.

1. 만약 현재 위치와 다음 위치의 cover 값이 같아면 => 같은 직사각형 내부를 검사하고 있으므로 count를 감소시켜선 안된다.
2. 만약 현재 위치와 다음 위치의 cover 값이 다르다면 => 서로 다른 직사각형이라는 뜻이므로 count를 하나 줄여줘야 한다.
	- (y, x) = (2, 2) && (nextY, nextX) = (3, 2) 일 때 count 1 감소시켰다고 가정해보자.
	- (y, x) = (2, 3) && (nextY, nextX) = (3, 3) 일 때는 count 1 감소시키면 안된다.
	- 우리는 경계선을 기준으로 한쪽 직사각형과 나머지 정사각형을 좀 더 체계적으로 관리할 필요가 있겠다.
	
`DisjointSet` 자료구조를 써서 직사각형을 집합으로 생각하고 집합을 관리하자.

{% highlight c++ linenos %}
int answer=cnt;
S.init(cnt);
for(int y=0; y<=sizeY; ++y){
	for(int x=0; x<=sizeX; ++x){
		for(int direc=0; direc<4; ++direc){
			int nextY=y+d_y[direc];
			int nextX=x+d_x[direc];
			if(nextY<0 || nextY>sizeY || nextX<0 || nextX>sizeX)	continue;
			//		현재좌표와 다음좌표가 변을 공유하는지 검사한다.
			//		만약 변을 공유한다면... 서로가 다른 집합에 속하는지 검사하여
			//		0 또는 1일 빼주어야 한다.
			if(cover[y][x]>1 && cover[nextY][nextX]>1)	answer-=S.merge(cover[y][x], cover[nextY][nextX]);
		}
	}
}
{% endhighlight %}

**12번째 줄 코드**가 이해하기 힘들었는데 현재위치와 다음위치에 대해 cover 값이 둘다 크다는 말이 경계선을 기준으로 서로 다른 두 직사각형이 맞닿아 있다는 것이다.

만약 현재위치 or 다음위치가 1값을 가지면 이는 직사각형이 외벽과 맞닿아 있다는 뜻이된다.

## 4. 정리
좌표압축, DFS, 서로소집합 등 많은 것이 한데 섞인 좋은 문제였다... 열공해야겠다. 갈길이 머네.
