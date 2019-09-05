---
layout: post
title:  "Leetcode Integer to English Words solution in Java"
description: Integer to English Words solution in Java leetcode273
date:   2019-09-04 17:40:00 +0800
category: coding
tags: [coding, leetcode, leetcode273]
---

**Leetcode 273, Integer to English Words** 

总体的思路：分治， 每三个数字当成一组处理，这样方便增加单位。

有很多细节需要考虑，比如0的时候，另外：11 - 19 这个范围需要特殊处理。



*PS: 说实话，如果面试遇到这类问题并且之前没有做过，那就等着跪吧。*


```java
 class Solution {

        private String[] oneMap = {"One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine"};
        private String[] n10Map = {"Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"};
        private String[] n20Map = {"Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"};

        public String numberToWords(int num) {
            if (num == 0) {
                return "Zero";
            }
            List<String> ans = new ArrayList();
            String[] units = {"Thousand", "Million", "Billion"};
            int unitIndex = -1;
            while (num > 0) {
                if (num % 1000 != 0) {
                    String nums = toWords(num % 1000);
                    if (unitIndex >= 0) {
                        ans.add(units[unitIndex]);
                    }
                    ans.add(nums);
                }
                num /= 1000;
                unitIndex++;
            }
            return toResultString(ans);
        }


        public String toWords(int num) {
            String snum = String.valueOf(num);
            if (snum.length() == 1) {
                return oneNumber(num);
            } else if (snum.length() == 2) {
                return twoNumber(num);
            } else {
                int kOfNum = snum.charAt(0) - '0';
                String ans = oneNumber(kOfNum);
                if (ans.length() > 0) {
                    ans += " Hundred";
                }
                String tw = twoNumber(Integer.parseInt(snum.substring(1)));
                return tw.length() == 0 ? ans : ans + " " + tw;
            }
        }

        public String oneNumber(int n) {
            if (n == 0) {
                return "";
            }
            return oneMap[n - 1];
        }

        public String twoNumber(int n) {
            if (n == 0) {
                return "";
            }
            if (n < 10) {
                return oneNumber(n);
            }
            if (n < 20) {
                return n10Map[n - 10];
            }
            String ans = n20Map[n / 10 - 2];
            String last = oneNumber(n % 10);
            if (last.length() > 0) {
                return ans + " " + last;
            }
            return ans;
        }

        private String toResultString(List<String> ans) {
            StringBuffer sb = new StringBuffer();
            for (int i = ans.size() - 1; i >= 0; i--) {
                sb.append(ans.get(i) + " ");
            }
            return sb.toString().trim();
        }
    }
```

