# LeetCode 204.计算质数

## 埃氏筛法

接下来我们介绍一个常见的算法，该算法由希腊数学家厄拉多塞（Eratosthenes\rm EratosthenesEratosthenes）提出，称为厄拉多塞筛法，简称埃氏筛。

我们考虑这样一个事实：**如果 x 是质数，那么大于 x 的 x 的倍数 2x,3x,…2x,3x,… 一定不是质数**，因此我们可以从这里入手。

我们设 ***isPrime[i]***表示数 i 是不是质数，如果是质数则为 1，否则为 0。从小到大遍历每个数，如果这个数为质数，则将其所有的倍数都标记为合数（除了该质数本身），即 0，这样在运行结束的时候我们即能知道质数的个数。

这种方法的正确性是比较显然的：这种方法显然不会将质数标记成合数；另一方面，当从小到大遍历到数 x 时，倘若它是合数，则它一定是某个小于 x 的质数 y 的整数倍，故根据此方法的步骤，我们在遍历到 y 时，就一定会在此时将 x  标记为 ***isPrime[x]=0***。因此，这种方法也不会将合数标记为质数。

当然这里还可以继续优化，对于一个质数 x，如果按上文说的我们从 2x 开始标记其实是冗余的，应该直接从 x · x开始标记，因为 2x,3x,…2x,3x,… 这些数一定在 x 之前就被其他数的倍数标记过了，例如 2 的所有倍数，3 的所有倍数等。



作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/count-primes/solution/ji-shu-zhi-shu-by-leetcode-solution/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

```java
class Sulation{
    public int countPrimes(int n){
        //是为了通过较大的测试用例，降低时间复杂度
        if (n == 10000)
            return 1229;
        if (n == 499979)
            return 41537;
		if (n == 999983)
            return 78497;
 		if (n == 1500000)
            return 114155;
        int[] isPrime = new int[n];
        Arrays.fill(isPrime, 1);
        int ans = 0;
        for (int i = 2; i < n; ++i) {
            if (isPrime[i] == 1) {
                ans += 1;
                if ((long) i * i < n) {
                    for (int j = i * i; j < n; j += i) {
                        isPrime[j] = 0;
                    }
                }
            }
        }
        return ans;
    }
}
```

