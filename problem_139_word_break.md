# Problem 139: Word Break


> https://leetcode.com/problems/word-break/

-------------------------------------------
##思路
这道题的思路类似于Palindrome Partitioning II。不过有不同的一点是，他加入了maxLength这个trick，只比到最大的长度就可以了。

-------------------------------------------
```java
public class Solution {
    public boolean wordBreak(String s, Set<String> wordDict) {
        if (s == null || s.length() == 0) {
            return true;
        }
        
        int maxLength = getMaxLength(wordDict);
        boolean[] canSegment = new boolean[s.length() + 1];
        canSegment[0] = true;
        for (int i = 1; i <= s.length(); i++) {
            canSegment[i] = false;
            for (int lastWord = 1; lastWord <= maxLength && lastWord <= i; lastWord++) {
                if (!canSegment[i - lastWord]) {
                    continue;
                }
                String word = s.substring(i - lastWord, i);
                if (wordDict.contains(word)) {
                    canSegment[i] = true;
                    break;
                }
            }
        }
        
        return canSegment[s.length()];
    }
    
    private int getMaxLength(Set<String> wordDict) {
        int maxLength = 0;
        for (String word : wordDict) {
            maxLength = Math.max(word.length(), maxLength);
        }
        return maxLength;
    }
    
}
```
------------------------------
##易错点

1. 数组长度
数组长度为```s.length() + 1```，也就是说从单词的开头到单词的屁股后面都要cut一下
2. 简化trick
```java
int lastWord = 1; lastWord <= maxLength && lastWord <= i; lastWord++
```
中间的这两个条件，相辅相成。lastWord不需要比最大的length大，因为再大了字典里就没有这个词了。
3. 跳过条件
```java
if (!canSegment[i - lastWord]) {
     continue;
}
```
![](wordBreak_1.jpg)































