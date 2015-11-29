##LeetCode解题报告
####292. Nim Game

#####题目内容：
***
You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.

Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.

For example, if there are 4 stones in the heap, then you will never win the game: no matter 1, 2, or 3 stones you remove, the last stone will always be removed by your friend.
***
#####解题思路：
&#160;&#160;&#160;&#160;先考虑n比较小的时候，怎样才能取胜。

1. n = [1, 2, 3]时，直接取走全部石子即可获胜，`先手胜`。

2. n = 4时，无论取走几个石子，对手都会取走剩余的石子。换句话说，无论先手取走多少石子，都会令对手处于情况1，`对手胜`。

3. n = [5, 6, 7]时，可以分别取走1，2，3个石子，使对手处于情况2，`先手胜`。

4. n = 8时，无论取走多少石子，都会令对手处于情况3，`对手胜`。

&#160;&#160;&#160;&#160;&#160;&#160;...... 

&#160;&#160;&#160;&#160;由此可见，当一个人剩余石子数为4的整数倍时，无论他取走几个石子，另一个人都可以通过策略取相应数量的石子，使对手的剩余石子数始终为4的整数倍，从而获得最终的胜利。
	

#####核心代码：
	bool canWinNim(int n)
    {
        return (n % 4);
    }

#####拓展：
1. 假设一共有n个石子，两个人轮流取，每次至少取1个，至多取m个。如果 n = (m + 1) * k + a (k为任意自然数，a < m + 1)，先手可以先取走a个石子，每当对手取走x个石子时，先手再取走m + 1 - x个石子，使对手的剩余石子数始终为（m + 1）的整数倍，就能获胜。
2. 有两堆各若干个物品，两个人轮流从某一堆或同时从两堆中取同样多的物品，规定每次至少取一个，多者不限，最后取光者得胜。则面对非奇异局势，先拿者必胜；反之，则后拿者取胜。奇异局势为：ak = [k * (1 + √5) / 2]，bk = ak + k (k = 0, 1, 2...)。
3. 有三堆各若干个物品，两个人轮流从某一堆取任意多的物品，规定每次至少取一个，多者不限，最后取光者得胜。则面对非奇异局势，先拿者必胜；反之，则后拿者取胜。奇异局势为异或和等于0。
4. 任给N堆石子，两人轮流从任一堆中任取(每次只能取自一堆)，取最后一颗石子的人获胜。则奇异局势为N个数异或和等于0。


#####总结：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;解决本题时，我先枚举了n比较小的情况，从而发现了只有n=4k时先手才会输的规律。很多时候做这种偏数学的题目，如果没有什么思路，都可以先用找规律的方法找到规律，然后再用数学方法证明，往往效率很高。

#####参考资料：
1. <http://www.cnblogs.com/celia01/archive/2011/11/15/2250171.html>