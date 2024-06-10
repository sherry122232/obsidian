warehouse

![[Pasted image 20240425142320.png]]


hack's team: 2771
```java
    public int maxNonDecreasingLength(int[] A, int[] B) {
        int res = 1, dp1 = 1, dp2 = 1, n = A.length, t11, t12, t21, t22;
        for (int i = 1; i < n; ++i) {
            t11 =  A[i - 1] <= A[i] ? dp1 + 1 : 1;
            t12 = A[i - 1] <= B[i] ? dp1 + 1 : 1;
            t21 = B[i - 1] <= A[i] ? dp2 + 1 : 1;
            t22 = B[i - 1] <= B[i] ? dp2 + 1 : 1;
            dp1 = Math.max(t11, t21);
            dp2 = Math.max(t12, t22);
            res = Math.max(res, Math.max(dp1, dp2));
        }
        return res;
    }
```

moves:

```
Solution {
    public int minKnightMoves(int x, int y) {
        int[][] dirs = new int[][] { { -1, -2 }, { -1, 2 }, { 1, -2 }, { 1, 2 }, { -2, -1 }, { -2, 1 }, { 2, -1 },
                { 2, 1 } };
        x = Math.abs(x);
        y = Math.abs(y);
        HashSet<String> visited = new HashSet<>();
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[] { 0, 0 });
        visited.add("0,0");

        int step = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            while (size-- > 0) {
                int[] cur = queue.poll();
                if (cur[0] == x && cur[1] == y) {
                    return step;
                }

                for (int[] dir : dirs) {
                    int i = cur[0] + dir[0];
                    int j = cur[1] + dir[1];
                    // (0, 0) -> (2, -1) -> (1, 1)
                    // +2的意思是多给两个格子的空间以便于骑士跳出去再跳回来的操作
                    if (!visited.contains(i + "," + j) && i >= -1 && j >= -1 && i <= x + 2 && j <= y + 2) {
                        queue.offer(new int[] { i, j });
                        visited.add(i + "," + j);
                    }
                }
```
process execution:

![[Pasted image 20240425143934.png]]


max path in tree，类似利口 幺尔斯，看看bfs / dfs思路的解
![[Pasted image 20240425143212.png]]
![[Pasted image 20240425143200.png]]

## first lady
first lady of software 算法
n_processes to run in n_intervals, 相邻interval的process不能相同
n_processes * (n_processes - 1) * (n_processes - 1) ...
广告
取modulos %(10^9+7)