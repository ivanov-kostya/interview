## Reverse String

Пример:

public String reverse(String input) {
// Ваш код
}

reverse("Hello") => "olleH"

Ожидается, что кандидат покажет знание работы с массивами символов и манипуляциями строк в Java.

### Решение

package com.ki.tasks;

import java.util.Arrays;

public class ReverseStr {
public static void main(String[] args) {
String input = "Hello";
String reverseStr = reverse(input);
System.out.println(reverseStr);

        String reverse2Str = reverse2(input);
        System.out.println(reverse2Str);
    }

    public static String reverse(String input) {
        StringBuilder sb = new StringBuilder(input);

        return sb.reverse().toString();
    }

    public static String reverse2(String input) {
        char[] chars = input.toCharArray();
        System.out.println(Arrays.toString(chars));

        int left = 0;
        int right = chars.length - 1;

        while (left < right) {
            char temp = chars[left];
            chars[left] = chars[right];
            chars[right] = temp;
            left++;
            right--;
        }

        return new String(chars);
    }
}

---------

## Reverse Integer

Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-231, 231 - 1], then return 0.
Assume the environment does not allow you to store 64-bit integers (signed or unsigned).

Если задано знаковое 32-битное целое число x, верните x с перевернутыми цифрами. Если при переворачивании x значение выходит за пределы диапазона знаковых 32-битных целых чисел [-231, 231 - 1], то верните 0.
Предположим, что среда не позволяет хранить 64-битные целые числа (подписанные или беззнаковые).

### Решение

package com.ki.tasks;


public class ReserseInt {
public static void main(String[] args) {
int x1 = 123;
int x2 = -123;
int x3 = 120;

        System.out.println(reverse(x1)); // 321
        System.out.println(reverse(x2)); // -321
        System.out.println(reverse(x3)); // 21
    }

    public static int reverse(int x) {
        int reversed = 0;
        while (x != 0) {
            int digit = x % 10;  // Извлекаем последнюю цифру
            x /= 10;  // Убираем последнюю цифру

            // Проверяем переполнение при реверсе
            if (reversed > Integer.MAX_VALUE / 10 || (reversed == Integer.MAX_VALUE / 10 && digit > 7)) {
                return 0;  // Переполнение для положительного числа
            }
            if (reversed < Integer.MIN_VALUE / 10 || (reversed == Integer.MIN_VALUE / 10 && digit < -8)) {
                return 0;  // Переполнение для отрицательного числа
            }

            // Обновляем реверсированное число
            reversed = reversed * 10 + digit;
        }
        return reversed;
    }
}


-----

## First Unique Character in a String

Given a string s, find the first non-repeating character in it and return its index. If it does not exist, return -1.

Задав строку s, найдите в ней первый неповторяющийся символ и верните его индекс. Если он не существует, верните -1.

Example 1:

Input: s = "leetcode"

Output: 0

Explanation:

The character 'l' at index 0 is the first character that does not occur at any other index.

Example 2:

Input: s = "loveleetcode"

Output: 2

Example 3:

Input: s = "aabb"

Output: -1

Constraints:

1 <= s.length <= 105
s consists of only lowercase English letters.

### Решение

public class FirstUniqueCharacterString {
    public static void main(String[] args) {
        String str1 = "digital";
        String str2 = "iikletk";
        String str3 = "aabb";

        System.out.println(getFirstUniqueChar(str1));
        System.out.println(getFirstUniqueChar(str2));
        System.out.println(getFirstUniqueChar(str3));
    }

    public static int getFirstUniqueChar(String str) {
        Map<String, Integer> charWithCount = new HashMap<>();
        char[] charArray = str.toCharArray();
        for (char ch : charArray) {
            charWithCount.put(ch, charWithCount.getOrDefault(ch, 0) + 1);
        }

        for (int i = 0; i < charArray.length; i++) {
            if (charWithCount.get(charArray[i] == 1) {
                return i;
            }
        }

        return -1;
    }
}

----------

## Given two strings s and t, return true if t is an anagram of s, and false otherwise.

## Если даны две строки s и t, верните true, если t является анаграммой s, и false в противном случае.


Example 1:

Input: s = "anagram", t = "nagaram"

Output: true

Example 2:

Input: s = "rat", t = "car"

Output: false



Constraints:

1 <= s.length, t.length <= 5 * 104
s and t consist of lowercase English letters.


Follow up: What if the inputs contain Unicode characters? How would you adapt your solution to such a case?

package com.ki.tasks;

import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

public class Anagram {
    public static void main(String[] args) {
        String str1 = "anagram";
        String str2 = "2nagaram";

        System.out.println(str1 + " is anagram for " + str2 + ": " + isAnagram2(str1, str2));
    }

    public static boolean isAnagram(String str1, String str2) {
        if (str1.length() == str2.length()) {
            char[] char1 = str1.toCharArray();
            char[] char2 = str2.toCharArray();
            Map<Character, Integer> char1WithCount = new HashMap<>();
            for (char c : char1) {
                char1WithCount.put(c, char1WithCount.getOrDefault(c, 0) + 1);
            }

            for (char c : char2) {
                if (!char1WithCount.containsKey(c) || char1WithCount.get(c) == 0) {
                    return false;
                }

                char1WithCount.put(c, char1WithCount.get(c) - 1);
            }
            return true;
        }
        return false;
    }

    public static boolean isAnagram2(String str1, String str2) {
        if (str1.length() != str2.length()) {
            return false;
        }

        char[] char1 = str1.toCharArray();
        char[] char2 = str2.toCharArray();

        Arrays.sort(char1);
        Arrays.sort(char2);

        return Arrays.equals(char1, char2);
    }
}

-------
## A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

Если задана строка s, верните true, если она является палиндромом, или false в противном случае.

Example 1:

Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
Example 2:

Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
Example 3:

Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.


Constraints:

1 <= s.length <= 2 * 105
s consists only of printable ASCII characters.

### Решение

package com.ki.tasks;

public class Palindrom {
    public static void main(String[] args) {
        String s = "A man, a plan, a canal: Panama";
        System.out.println("Palindrom1 " + isPalindrom(s));
        System.out.println("Palindrom2 " + isPalindrom2(s));
    }

    private static boolean isPalindrom(String s) {
        StringBuilder cleaned = new StringBuilder();
        char[] chars = s.toCharArray();
        for (char c : chars) {
            if (Character.isLetterOrDigit(c)) {
                cleaned.append(Character.toLowerCase(c));
            }
        }
        System.out.println(cleaned.toString());

        int left = 0;
        int right = cleaned.length() - 1;

        while (left < right) {
            if (cleaned.charAt(left) != cleaned.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }

        return true;
    }

    private static boolean isPalindrom2(String s) {
        String cleaned = s.toLowerCase().replaceAll("[^a-z0-9]", "");
        System.out.println(cleaned);
        String strReverse = new StringBuilder(cleaned).reverse().toString();

        return cleaned.equals(strReverse);
    }
}

-------

## Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

## Если даны две строки needle и haystack, верните индекс первого вхождения needle в haystack, или -1, если needle не является частью haystack.


Example 1:

Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.
Example 2:

Input: haystack = "leetcode", needle = "leeto"
Output: -1
Explanation: "leeto" did not occur in "leetcode", so we return -1.


Constraints:

1 <= haystack.length, needle.length <= 104
haystack and needle consist of only lowercase English characters.

### Решение

package com.ki.tasks;

public class HaystackNeedle {
public static void main(String[] args) {
System.out.println(haystackNeedle("frtsadgfssad", "sad"));
System.out.println(haystackNeedle("frtsadgfssad", "sad0"));
System.out.println(subStr("frtsadgfssad", "sad"));
System.out.println(subStr("frtsadgfssad", "sad0"));
}

    private static int haystackNeedle(String haystack, String needle) {
        return haystack.indexOf(needle);
    }

    private static int subStr(String haystack, String needle) {
        int haystackLen = haystack.length();
        int needleLen = needle.length();
        if (haystackLen < needleLen) {
            return -1;
        }

        for (int i = 0; i < haystackLen - needleLen; i++) {
            if (haystack.substring(i, i + needleLen).equals(needle)) {
                return i;
            }
        }

        return -1;
    }
}

-------

Implement the myAtoi(string s) function, which converts a string to a 32-bit signed integer.

The algorithm for myAtoi(string s) is as follows:

Whitespace: Ignore any leading whitespace (" ").
Signedness: Determine the sign by checking if the next character is '-' or '+', assuming positivity is neither present.
Conversion: Read the integer by skipping leading zeros until a non-digit character is encountered or the end of the string is reached. If no digits were read, then the result is 0.
Rounding: If the integer is out of the 32-bit signed integer range [-231, 231 - 1], then round the integer to remain in the range. Specifically, integers less than -231 should be rounded to -231, and integers greater than 231 - 1 should be rounded to 231 - 1.
Return the integer as the final result.

Реализуйте функцию myAtoi(string s), которая преобразует строку в 32-битное знаковое целое число.

Алгоритм myAtoi(string s) выглядит следующим образом:

Пробельные символы: Игнорировать ведущие пробельные символы (» »).
Знаковость: Определяем знак, проверяя, является ли следующий символ '-' или '+', предполагая, что ни один из них не является положительным.
Преобразование: Считайте целое число, пропуская ведущие нули, пока не встретится нецифровой символ или не будет достигнут конец строки. Если ни одна цифра не была считана, то результатом будет 0.
Округление: Если целое число выходит за пределы диапазона 32-битных знаковых целых чисел [-231, 231 - 1], то округлите его, чтобы оно осталось в этом диапазоне. В частности, целые числа меньше -231 должны быть округлены до -231, а целые числа больше 231 - 1 должны быть округлены до 231 - 1.
В качестве конечного результата верните целое число.

### Решение

package com.ki.tasks;

public class StringToInteger {
public static void main(String[] args) {
System.out.println(stringToInteger("42"));
System.out.println(stringToInteger("   -42    "));
System.out.println(stringToInteger("-42sssff02"));
System.out.println(stringToInteger("224sfds74dda836df48"));
System.out.println(stringToInteger("sfds74dda836df48"));
}

    private static int stringToInteger(String s) {
        int sign = 1;
        String sTrimmed = s.trim();
        if (sTrimmed.charAt(0) == '-') {
            sign = -1;
        }

        String cleaned = sTrimmed.replaceAll("[^0-9]", "");

        if (cleaned.isEmpty()) return 0;

        int result = 0;
        for (int i = 0; i < cleaned.length(); i++) {
            int digit = cleaned.charAt(i) - '0';

            if (result > Integer.MAX_VALUE / 10 ||
                    (result == Integer.MAX_VALUE / 10 && digit > Integer.MAX_VALUE % 10)) {
                return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
            }

            result = result * 10 + digit;
        }

        return sign * result;
    }
}

-------------

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

Напишите функцию для поиска самой длинной строки с общим префиксом среди массива строк.

Если общего префикса нет, верните пустую строку «».

Example 1:

Input: strs = ["flower","flow","flight"]
Output: "fl"
Example 2:

Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.


Constraints:

1 <= strs.length <= 200
0 <= strs[i].length <= 200
strs[i] consists of only lowercase English letters.

### Решение

package com.ki.tasks;

import java.util.Arrays;

public class PrefixStr {
public static void main(String[] args) {
String[] strs = {"flower", "flow", "flight"};
String[] strs2 = {"flower", "dog", "duck"};
System.out.println(prefixStr(strs));
System.out.println(prefixStr(strs2));
}

    private static String prefixStr(String[] strs) {
        System.out.println(Arrays.toString(strs));
        if (strs == null || strs.length == 0) {
            return "";
        }

        String prefix = strs[0];

        for (int i = 1; i < strs.length; i++) {
            String s = strs[i];
            while (strs[i].indexOf(prefix) != 0) {
                prefix = prefix.substring(0, prefix.length() - 1);
                System.out.println("prefix = " + prefix);
            }
        }
        return prefix;
    }
}