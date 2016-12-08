## Best Divisor

Kristen loves playing with and comparing numbers. She thinks that if she takes two different positive numbers, the one whose digits sum to a larger number is better than the other. If the sum of digits is equal for both numbers, then she thinks the smaller number is better. For example, Kristen thinks that 13 is better than 31 and that 12 is better than 11.

Given an integer, n, can you find the divisor of n that Kristin will consider to be the best?

### Solution

```java
import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

public class Solution {

    public static int getSumOfDigit(int n) {
        int sum = 0;
        while(n > 0) {
            sum += n % 10;
            n = n / 10;
        }

        return sum;
    }

    public static int getBestDivisor(int n) {
        int maxSum = 1, bestNumber = 1;

        for(int i = 2; i <= n; i ++) {
            if(n % i == 0) {
                int digitSum = getSumOfDigit(i);

                if (digitSum > maxSum) {
                    maxSum = digitSum;
                    bestNumber = i;
                }
            }
        }

        return bestNumber;
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int n = in.nextInt();
        in.close();
        System.out.println(getBestDivisor(n));
    }
}

```
