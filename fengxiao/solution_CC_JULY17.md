# Solution
```
/******************
    Code chef链接：https://www.codechef.com/JULY17?order=desc&sortBy=successful_submissions
题目按CF顺序排序
******************/
```
# #A Whats in the Name
```
/******************
     主要算法：模拟+字符串处理
     Data limit: 
     1 ≤ T ≤ 100
     2 ≤ 名字长度 ≤ 10
******************/
```
### 题意
给你每行一个名字，要求将它格式化    
规则： 除了最后一个单词，都输出 (首字母大写)+'.'+' ' 最后一个输出 (大写的首字母)+（小写的别的字母）+\n
### 题解
随便模拟一下。。
### 核心代码
```
/******************
for(i=1;i<=n;i++)
	{
		while(ch!='\n')
		{
			ch=getchar(); cnt=0;
			while(ch!=' ' && ch!='\n')
			{
				if(cnt==0) name[++cnt]=upper(ch);
				else name[++cnt]=lower(ch);
				ch=getchar();
			}
			if(ch!='\n') printf("%c. ",name[1]);
			else break;
		}
		for(j=1;j<=cnt;j++) printf("%c",name[j]); puts("");
		ch=0;
	}
******************/
```
### 错题记录
没错过
***
# #B Chef and Sign Sequences
```
/******************
    主要算法： 字符串+脑洞
     Data limit:1 ≤ T, |s| ≤ 1e6
******************/
```
### 题意
给你一串由><=组成的串，再运算符两遍填数字（正整数），使运算符成立。  
让你求填的数字的最大值的最小值。

### 题解
可以直接无视=，然后就转换成求连续相同字串的组成数量的最大值+1
### 核心代码
```
/******************
cin>>s; ls=strlen(s);
		int i=0,cnt=0,top=1,b=1;
		while(i<ls)
		{
			char t=s[i]; cnt=0;
			for(i=i;i<ls;i++)
				if(s[i]==t) cnt++;
				else if(s[i]=='=');
				else break;
			if(t == '<') top=max(top,b+cnt),b+=cnt;
			if(t == '>') top=max(top,cnt+1),b=1;
		}
		cout<<top<<endl;
******************/
```
### 错题记录

***
# #C Calculator
```
/******************
      主要算法：微数学
     Data limit:
     1 ≤ T ≤ 10,000
      1 ≤ N, B ≤ 1,000,000,000
******************/
```
### 题意
有两个屏幕，初始数字都是0，有n个能量，两种操作  
1.在1号屏幕的数字+1，代价：1能量  
2.在2号屏幕的数字+=1号屏幕的 代价：b能量  
### 题解
贪心策略：先在1号屏幕一个个+，到一定值后一直+二号屏幕（那么简单不用证明吧。。）  
根据这个策略得到二次函数：ans=(1/b)*x*(n-x), (1<=x<=n)  
然后求个最大值就可以了  
细节处理：让x能被b整除，要不然剩下的能量就浪费了，但注意要两边都算一下取max
### 核心代码
```
/******************
cin>>n>>b;
		int ans=(n/2/b*b)*(n-(n/2/b*b))/b;
		if(n/2/b*b!=n/2)
		ans=max((n/2/b*b+b)*(n-(n/2/b*b+b))/b,ans);
		cout<<ans<<endl;
******************/
```
### 错题记录

***
# #D 
```
/******************
      主要算法：
     Data limit:
******************/
```
### 题意

### 题解

### 核心代码
```
/******************

******************/
```
### 错题记录


***
# #E 
```
/******************
      主要算法：
     Data limit:
******************/
```
### 题意


### 题解

### 核心代码
```
/******************

******************/
```
###错题记录

***
