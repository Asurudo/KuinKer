# 背包

```c++
struct Pack
{
	int dp[maxn];
	//别忘记初始化V 
	int V;
	//0-1 背包，代价为 cost, 获得的价值为 weight
	void ZeroOnePack(int cost,int weight)
	{
		for(int i=V; i >= cost; i--)
			dp[i]=max(dp[i],dp[i-cost]+weight);
	}
	//完全背包，代价为 cost, 获得的价值为 weight
	void CompletePack(int cost,int weight)
	{
		for(int i=cost; i<=V; i++)
			dp[i]=max(dp[i],dp[i-cost]+weight);
	}
	//多重背包
	void MultiplePack(int cost,int weight,int amount)
	{
		if(cost*amount>=V) CompletePack(cost,weight);
		else
		{
			int k=1;
			while(k<amount)
			{
				ZeroOnePack(k*cost,k*weight);
				amount -= k;
				k<<=1;
			}
			//这个不要忘记了，经常 掉了
			ZeroOnePack(amount*cost,amount*weight);
		}
	}
}P;
```

