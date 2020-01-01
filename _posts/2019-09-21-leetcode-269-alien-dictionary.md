---
layout: post
title: "[LeetCode] 269.Alien Dictionary 火星词典"
description: 269.Alien Dictionary 火星词典
date: 2019-09-21 18:58:00 +0800
category: coding
tags: [coding, leetcode, leetcode269]
---

**Leetcode 269, Alien Dictionary** 

使用BFS的拓扑排序.


```java
 class Solution {
    public String alienOrder(String[] words) {
        if (words == null || words.length == 0) {
            return "";
        }
        // init nodes.
        int[] indegree = new int[256];
        Arrays.fill(indegree, -1);
        Set<Character>[] edges = new Set[256];
        build(words, indegree, edges);
        // start bfs.
        Queue<Character> queue = new LinkedList();
        Set<Character> hset = new HashSet();
        for (char root : findRoots(indegree)) {
            queue.offer(root);
            hset.add(root);
        }
        String ans = "";
        if (queue.size() == 0) {
            return ans;
        }
        while (queue.size() > 0) {
            char node = queue.poll();
            ans += node;
            for (char next : edges[node]) {
                indegree[next]--;
                if (indegree[next] == 0) {
                    if (hset.contains(next)) {
                        continue;
                    }
                    queue.offer(next);
                    hset.add(next);
                }
            }
        }
        int charCount = 0;
        for (int i = 0; i < 256; i++) {
            if (edges[i] != null) {
                charCount++;
            }
        }
        if (ans.length() != charCount) {
            return "";
        }
        return ans;
    }

    public void build(String[] words, int[] indegree, Set<Character>[] edges) {
        // init
        for (String word : words) {
            for (char ch : word.toCharArray()) {
                if (edges[ch] == null) {
                    indegree[ch] = 0;
                    edges[ch] = new HashSet<Character>();
                }
            }
        }
        for (int i = 0; i < words.length; i++) {
            for (int j = i + 1; j < words.length; j++) {
                int index = findFirstNonEquals(words[i], words[j]);
                if (index == -1) {
                    continue;
                }
                char from = words[i].charAt(index);
                char to = words[j].charAt(index);
                // build edges.
                if (from != to && !edges[from].contains(to)) {
                    edges[from].add(to);
                    indegree[to]++;
                }
            }
        }
    }

    public int findFirstNonEquals(String a, String b) {
        int i = 0;
        while (i < a.length() && i < b.length()) {
            if (a.charAt(i) == b.charAt(i)) {
                i++;
            } else {
                return i;
            }
        }
        return -1;
    }

    public List<Character> findRoots(int[] indegree) {
        List<Character> roots = new ArrayList();
        for (int i = 0; i < 256; i++) {
            if (indegree[i] == 0) {
                roots.add((char) i);
            }
        }
        return roots;
    }
}
```


