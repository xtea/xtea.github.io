---
layout: post
title:  "Leetcode The Maze solution in Java "
description: Leetcode maze solution in Java
date:   2019-09-05 17:40:00 +0800
category: coding
tags: [coding, leetcode, leetcode490]
---

**Leetcode 490, The Maze** 

今天刷了这个题，被饶了很久，原因把 visted 和 wall 这2种情况混淆了。特此留念！

```java
 class Solution {
    
    int[][] directions = { 
        {1, 0}, {-1, 0}, {0, 1}, {0, -1}
    };

    public boolean hasPath(int[][] maze, int[] start, int[] destination) {
        boolean[][] visited = new boolean[maze.length][maze[0].length];
        return helper(maze, start, destination, visited);
    }

    public boolean helper(int[][] maze, int[] start, int[] destination, boolean[][] visited) {
        int x = start[0];
        int y = start[1];
        if (!canMove(x, y, maze)) {
            return false;
        }
        visited[x][y] = true;
        for (int i = 0; i < directions.length; i++) {
            int nx = x;
            int ny = y;
            // move until next is wall.
            while (canMove(nx + directions[i][0], ny + directions[i][1], maze)) {
                nx += directions[i][0];
                ny += directions[i][1];
            }
            // check if visited.
            if (visited[nx][ny]) {
                continue;
            }
            // check if find destination
            if (nx == destination[0] && ny == destination[1]) {
                return true;
            }
            // recursion with new start.
            if (helper(maze, new int[]{nx, ny}, destination, visited)) {
                return true;
            }
        }
        return false;
    }

    public boolean canMove(int x, int y, int[][] maze) {
        int r = maze.length;
        int c = maze[0].length;
        if (x < 0 || x >= r || y < 0 || y >= c) {
            return false;
        }
        if (maze[x][y] == 1) {
            return false;
        }
        return true;
    }
}
```