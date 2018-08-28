# 372-super-pow

## Question {#question}

[https://leetcode.com/problems/super-pow/description/](https://leetcode.com/problems/super-pow/description/)

Your task is to calculate ab mod 1337 where a is a positive integer and b is an extremely large positive integer given in the form of an array.

**Example:**

```text
a = 2
b = [3]

Result: 8
```

```text
a = 2
b = [1,0]

Result: 1024
```

## Thought Process {#thought-process}

1. Modular Exponentiation
   1. It's useful in the field of public-key cryptography, [https://en.wikipedia.org/wiki/Modular\_exponentiation](https://en.wikipedia.org/wiki/Modular_exponentiation)
   2. c mod m = \(a ⋅ b\) mod m = \[\(a mod m\) ⋅ \(b mod m\)\] mod m
   3. Starting from the front, we do the powMod the base with the corresponding digit
   4. Then, we need to remember to powMod the previous result with 10
   5. Time complexity O\(n\)
   6. Space complexity O\(1\)
2. Euler's Theorem/Fermat's Little Theorem
   1. Euler's theorem, \[\[[https://en.wikipedia.org/wiki/Euler's\_theorem\]\(https://en.wikipedia.org/wiki/Euler's\_theorem\]\(https://en.wikipedia.org/wiki/Euler's\_theorem\]\(https://en.wikipedia.org/wiki/Euler's\_theorem\)\](https://en.wikipedia.org/wiki/Euler's_theorem]%28https://en.wikipedia.org/wiki/Euler's_theorem]%28https://en.wikipedia.org/wiki/Euler's_theorem]%28https://en.wikipedia.org/wiki/Euler's_theorem%29\)\)
   2. Fermat's little theorem, \[\[[https://en.wikipedia.org/wiki/Fermat's\_little\_theorem\]\(https://en.wikipedia.org/wiki/Fermat's\_little\_theorem\]\(https://en.wikipedia.org/wiki/Fermat's\_little\_theorem\]\(https://en.wikipedia.org/wiki/Fermat's\_little\_theorem\)\](https://en.wikipedia.org/wiki/Fermat's_little_theorem]%28https://en.wikipedia.org/wiki/Fermat's_little_theorem]%28https://en.wikipedia.org/wiki/Fermat's_little_theorem]%28https://en.wikipedia.org/wiki/Fermat's_little_theorem%29\)\)
   3. Euler's totient function, \[\[[https://en.wikipedia.org/wiki/Euler's\_totient\_function\]\(https://en.wikipedia.org/wiki/Euler's\_totient\_function\]\(https://en.wikipedia.org/wiki/Euler's\_totient\_function\]\(https://en.wikipedia.org/wiki/Euler's\_totient\_function\)\](https://en.wikipedia.org/wiki/Euler's_totient_function]%28https://en.wikipedia.org/wiki/Euler's_totient_function]%28https://en.wikipedia.org/wiki/Euler's_totient_function]%28https://en.wikipedia.org/wiki/Euler's_totient_function%29\)\)
   4. Examples, [http://mathonline.wikidot.com/examples-using-euler-s-theorem](http://mathonline.wikidot.com/examples-using-euler-s-theorem)
   5. Three cases for reducing the power
      1. a is multiple of 1337, result is 0
      2. a is coprime of 1337, then a ^ b % 1337 = a ^ \(b % phi\(1337\)\) % 1337
      3. a has divisor of 7 or 191, 
   6. phi\(1337\) = phi\(7 \* 191\) = 6 \* 190 = 1140
   7. a ^ b mod 1337 = a ^ x mod 7, where x = b mod 1140
   8. 

## Solution {#thought-process}

```java
class Solution {
    public int superPow(int a, int[] b) {
        int k = 1337;
        a %= k;
        int result = 1;
        for (int i = 0; i < b.length; i++) {
            result = powMod(result, 10, k) * powMod(a, b[i], k) % k;
        }
        return result;
    }

    private int powMod(int a, int b, int k) {
        int result = 1;
        while (b != 0) {
            if (b % 2 != 0) result = result * a % k;
            a = a * a % k;
            b /= 2;
        }
        return result;
    }
}
```

```java
class Solution {
    public int superPow(int a, int[] b) {
        if (a % 1337 == 0) return 0;
        int k = 1337, phi = 1140;
        a %= k;
        int p = 0;
        for (int i : b) p = (p * 10 + i) % phi;
        if (p == 0) p += 1140;
        return powMod(a, p, k);
    }

    private int powMod(int a, int b, int k) {
        int result = 1;
        while (b != 0) {
            if (b % 2 != 0) result = result * a % k;
            a = a * a % k;
            b /= 2;
        }
        return result;
    }
}
```

## Additional {#additional}

