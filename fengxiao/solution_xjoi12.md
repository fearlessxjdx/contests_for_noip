# Solution
```
/******************
    xjoi链接： http://www.hzxjhs.com:83/contest/749
******************/
```
# #A 数列
```
/******************
     主要算法： 模拟
     Data limit:
     100%数据满足
    1<=T<=20
    1<=N<=50000
    1<=K<=1000000
    序列的每个数<=1000000000
    30%数据满足
    1<=T<=10
    1<=N,K<=1000
******************/
```
### 题意
给你个数列，n，k  
求出数列中所有的 和能被k整除的字串 的数量
### 题解
利用同余定理（有这玩意吗。。）  
可知如果两个数%P后的值相同那他们相减后能被P整除  
根据这个原理维护cnt数组表示%k余i的数的个数
sum数组表示前缀和（貌似没什么必要，可以边做边维护）
那么对于某一余i的位置只要加上cnt[i]就可以了，具体细节见代码（说不清楚）。。。
### 核心代码
```
/******************
 while(T--)
    {
        scanf("%I64d %I64d",&K,&n); ans=0; memset(cnt,0,sizeof(cnt));
        cnt[0]=1;
        for(int i=1;i<=n;i++)
        {
            scanf("%d",&a[i]);
            sum[i]=(sum[i-1]+a[i])%K;
            ans+=cnt[sum[i]];
            cnt[sum[i]]++;
        }
        printf("%d\n",ans);
    }
******************/
```
### 错题记录

***
# #B 钓鱼
```
/******************
    主要算法： DP
     Data limit:
     100%的数据满足
    1<=T,time<=10
    1<=Ax,Ay,Q,x,y,D,L<=10
    1<=N<=14
    30%的数据满足
    1<=N<=5
******************/
```
### 题意（未知数以代码中为准）
给定一个区间0—X，里面有n条鱼，每条鱼的信息有x（起始位置），y（垃圾），D（速度），l（长度**长度为1占两格。。**），t（鱼出现在初始位置的时间）  
初始位置在0的鱼只能向右游，初始位置在X的鱼只能向左移动。  
一个人初始位置在x，每秒有两个选择1：原地捕鱼。（能捕到在当前时间在他正下方的鱼，摸到个点也算，并且可能捕到多条鱼）2：向左边或右边移动小于等于q的距离  
时间从0开始，问在T时间（该时间末尾，然而题目有歧义）时他最多能捕到多少鱼。

### 题解
一看数据那么小，第一反应搜索，然而状态的记录太过麻烦，分析后复杂度较高，于是放弃  
然后便能想到状压DP：f[i][j][k]表示在i时间（末尾），在j号位置，能否捕掉k（二进制的状态，1表示这条鱼被捕了）鱼。  
然后便能发现要预处理出g[i][j]表示i时间j位置能捕到哪些鱼。**半条鱼在区间也是算的。。**  
然后就大功告成了。
### 核心代码
```
/******************
for(i=0;i<n;i++)
    {
        g[a[i].t][a[i].x]+=(1<<i);
        int pos=a[i].x;
        for(j=1;j;j++)
        {
            pos+=a[i].v*a[i].di;
            flag=0;
                for(k=0;k<=a[i].l;k++)
                {
                    if(pos-k*a[i].di>=0 && pos-k*a[i].di<=X)
                        {flag=1; g[a[i].t+j][pos-k*a[i].di]+=(1<<i);}
                }
            if(!flag) break;
        }
    }
    f[0][x][0]=1;
    for(i=1;i<=T+1;i++)
    {
        for(j=0;j<=X;j++)
            for(k=0;k<(1<<14);k++)
                for(l=-q;l<=q;l++)
                    if(j+l>=0 && j+l<=X)
                        f[i][j][k]=f[i][j][k] || f[i-1][j+l][k];
        for(j=0;j<=X;j++)
            if(g[i][j])
                for(k=0;k<(1<<14);k++)
                    f[i][j][k|g[i][j]]=f[i][j][k|g[i][j]] || f[i-1][j][k];
    }
******************/
```
### 错题记录
刚开始没想到鱼还能剩半条。。
***
# #C 雪
```
/******************
      主要算法：数论
     Data limit:
     100%的数据满足：
    0<a<pi
    0<A<1000,A为实数
    0<B<pi
    1<=N<=1000000
    30%的数据满足：
    1<=N<=100,且a=pi/2.
******************/
```
### 题意
给你一堆中线在y轴上的等腰三角形，以及一条已知入射角的光，求出这坨三角形能被照亮的面积（长度？）
### 题解
画个图列个方程可以解得光经过上一个等腰三角形的侧点后映照下面一个等腰三角形时上面的阴影长度，然后对每两个三角形做一次，再讨论一些情况就可以了  
并且此题采用弧度制表示角度，需要注意  
注意背光面也是可能照到的  
注意光线可能略过一个三角形直接到下面的下面那个三角形，这是就需要一些处理，详见代码。
### 核心代码
```
/******************
先%张正非dalao。。。
    for(i=1;i<=n;i++)
    {
        scanf("%lf %lf",&p[i].a,&p[i].b);
        p[i].a/=2; p[i].b/=2;
        p[i].l=p[i].a/sin(p[i].b);
        p[i].h=p[i].a/tan(p[i].b);
    }
    ans+=p[1].l,tmp=p[1].a;
    for(i=2;i<=n;i++)//count right
    {
        double x=tmp*tan(a)/(tan(a)+tan(pi/2-p[i].b))/sin(p[i].b);
        if(x>=p[i].l) tmp-=p[i].h/tan(a);
        else ans+=p[i].l-x,tmp=p[i].a;
    }
    if((pi/2-p[1].b)<a) ans+=p[1].l,tmp=p[1].a;
    else tmp=p[1].h/(tan(a));
    for(i=2;i<=n;i++)//count left
    {
        if((pi/2-p[i].b)>a) {tmp+=p[i].h/tan(a); continue;}
        double x=(tmp*tan(pi/2-a)/(tan(p[i].b)-tan(pi/2-a))+tmp)/sin(p[i].b);
        if(x>=p[i].l) tmp+=p[i].h/tan(a);
        else ans+=p[i].l-x,tmp=p[i].a;
    }
******************/
```
### 错题记录
由于思路是zzfdalao的思路我没有错（？？？）
***
# #D 键盘
```
/******************
      主要算法：大暴力
     Data limit:
     100%数据满足：
      0<=a,b,c,d,e<=100
      1<=N<=1000000
      30%数据满足：
      1<=N<=100
******************/
```
### 题意
背景：给你键盘图并告诉你哪些键盘归哪种手指控制  
给出每种手指按一次的疲劳值与一行字符  
让你调整键盘布局使总疲劳值最小  
约定：键盘只包括图中第2行'`'到'\',第三行'Q'到']',第四行'A'到''',第五行'Z'到'/'，第六行的空格键。  
     如果需要键盘配合的输出键，只需计算不加shift的代价，比如！以 1计算  
     所有字母均大写
### 题解
用cnt统计每种字符出现的次数，然后贪心把代价最小的配给敲击次数最多的，这样做就OK了，注意字符串处理
### 核心代码
```
/******************
sort(a+1,a+6);
    for(i=1;i<=ls;i++) cnt[getchar()]++;
    sort(cnt+1,cnt+300+1,cmp);
    int k=1;
    for(i=1,k=1;i<=256&&cnt[i];i++,--a[k].S==0?++k:0) ans+=a[k].F*cnt[i];
******************/
```
### 错题记录
被字符串坑了..

***
