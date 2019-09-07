---
layout: post
title:  "[LeetCode] 505. The Maze II 迷宫II "
description: [LeetCode] 505. The Maze II 迷宫II Java 实现
date:   2019-09-07 12:40:00 +0800
category: coding
tags: [coding, leetcode, leetcode505]
---

**Leetcode 505, The MazeII** 

这个题可以用DFS、BFS或者使用Dijkstra算法，以下是我使用Dijkstra实现。



```java
 public class Maze2 {


    class Point implements Comparator<Point> {
        int x, y;
        int distance;

        public Point() {
        }

        public Point(int x, int y, int distance) {
            this.x = x;
            this.y = y;
            this.distance = distance;
        }

        @Override
        public int compare(Point o1, Point o2) {
            return o1.distance - o2.distance;
        }
    }


    public int shortestDistance(int[][] maze, int[] start, int[] destination) {
        if (maze == null || maze.length == 0) {
            return -1;
        }
        int m = maze.length;
        int n = maze[0].length;
        // distanceTo from start to current point.
        int[][] distance = initDistance(m, n, start);
        PriorityQueue<Point> priorityQueue = new PriorityQueue<>(new Point());
        // put start to heap.
        priorityQueue.offer(new Point(start[0], start[1], 0));
        // start bfs.
        while (priorityQueue.size() > 0) {
            Point point = priorityQueue.poll();
            List<Point> nextPoints = findNextPoints(point, maze);
            for (Point np : nextPoints) {
                if (np.distance < distance[np.x][np.y]) {
                    distance[np.x][np.y] = np.distance;
                    // put to heap and mark visited.
                    priorityQueue.offer(np);
                }
            }
        }
        // shortest distanceTo from start to destination
        int ans = distance[destination[0]][destination[1]];
        return ans == Integer.MAX_VALUE ? -1 : ans;
    }

    private int[][] initDistance(int m, int n, int[] start) {
        int[][] ans = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                ans[i][j] = Integer.MAX_VALUE;
            }
        }
        ans[start[0]][start[1]] = 0;
        return ans;
    }

    private List<Point> findNextPoints(Point point, int[][] maze) {
        int[][] directions = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
        List<Point> ans = new ArrayList<>();
        // go four directions.
        for (int i = 0; i < directions.length; i++) {
            int nx = point.x;
            int ny = point.y;
            int step = 0;
            // move until next is wall.
            while (canMove(nx + directions[i][0], ny + directions[i][1], maze)) {
                nx += directions[i][0];
                ny += directions[i][1];
                step++;
            }
            Point np = new Point(nx, ny, point.distance + step);
            ans.add(np);
        }
        return ans;
    }

    public boolean canMove(int x, int y, int[][] maze) {
        int r = maze.length;
        int c = maze[0].length;
        if (x < 0 || x >= r || y < 0 || y >= c) {
            return false;
        }
        return maze[x][y] == 0;
    }
}
```