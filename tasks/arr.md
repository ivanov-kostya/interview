
## Remove Duplicates from Sorted Array (Удаление дубликатов из отсортированного массива)

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
Return k.
Custom Judge:

The judge will test your solution with the following code:

int[] nums = [...]; // Input array
int[] expectedNums = [...]; // The expected answer with correct length

int k = removeDuplicates(nums); // Calls your implementation

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
assert nums[i] == expectedNums[i];
}
If all assertions pass, then your solution will be accepted.

Из целочисленного массива nums, отсортированного в неубывающем порядке, удалите дубликаты на месте так, чтобы каждый уникальный элемент встречался только один раз. Относительный порядок элементов должен остаться прежним. Затем верните количество уникальных элементов в nums.

Если считать, что количество уникальных элементов в nums равно k, то для его получения необходимо выполнить следующие действия:

Изменить массив nums таким образом, чтобы первые k элементов nums содержали уникальные элементы в том порядке, в котором они присутствовали в nums изначально. Остальные элементы nums не важны, как и размер nums.
Возвращаем k.
Пользовательский судья:

Судья проверит ваше решение с помощью следующего кода:

int[] nums = [...]; // Входной массив
int[] expectedNums = [...]; // Ожидаемый ответ с правильной длиной

int k = removeDuplicates(nums); // Вызывает вашу реализацию

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
assert nums[i] == expectedNums[i];
}
Если все утверждения пройдут, то ваше решение будет принято.

Example 1:

Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
Example 2:

Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).


Constraints:

1 <= nums.length <= 3 * 104
-100 <= nums[i] <= 100
nums is sorted in non-decreasing order.

### Решение

package com.ki.tasks.array;

import java.util.Arrays;
import java.util.HashSet;

public class RemoveDuplicatesFromSortedArray {
    public static void main(String[] args) {
        int[] nums1 = {1, 1, 2, 2, 3, 4};
        int[] nums2 = {0, 0, 1, 1, 1, 2, 3, 3, 4, 4, 4, 4, 5};
        System.out.println(removeDuplicates(nums1));
        System.out.println("=============");
        System.out.println(removeDuplicatesHashSet(nums1));
        System.out.println(removeDuplicatesHashSet(nums2));
    }

    private static int removeDuplicatesHashSet(int[] nums) {
        if (nums.length == 0) return 0;

        HashSet<Integer> hashSet = new HashSet<>();

        for (int i = 0; i < nums.length; i++) {
            hashSet.add(nums[i]);
        }

        return hashSet.size();
    }

    private static int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;

        int j = 0;

        for (int i = 1; i < nums.length; i++) {
            System.out.println(Arrays.toString(nums));
            if (nums[j] != nums[i]) {
                j++;
                nums[j] = nums[i];
            }
            System.out.println("j = " + j);
        }

        return j + 1;
    }
}

### Пояснение:

* Если массив пустой, сразу возвращаем 0.
* Используем два указателя: i для отслеживания уникальных элементов и j для прохода по массиву.
* Каждый раз, когда находим новый уникальный элемент (nums[j] != nums[i]), увеличиваем i и обновляем nums[i] текущим элементом nums[j].
* По завершении цикла, значение i + 1 будет количеством уникальных элементов в массиве.

## Best Time to Buy and Sell Stock II (Лучшее время для покупки и продажи акций II)

You are given an integer array prices where prices[i] is the price of a given stock on the ith day.

On each day, you may decide to buy and/or sell the stock. You can only hold at most one share of the stock at any time. However, you can buy it then immediately sell it on the same day.

Find and return the maximum profit you can achieve.

Вам дан целочисленный массив prices, где prices[i] - это цена данной акции на i-й день.

В каждый день вы можете принять решение о покупке и/или продаже акции. В любой момент времени вы можете держать не более одной акции. Однако вы можете купить ее и тут же продать в тот же день.

Найдите и верните максимальную прибыль, которую вы можете получить.

Example 1:

Input: prices = [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Total profit is 4 + 3 = 7.
Example 2:

Input: prices = [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Total profit is 4.
Example 3:

Input: prices = [7,6,4,3,1]
Output: 0
Explanation: There is no way to make a positive profit, so we never buy the stock to achieve the maximum profit of 0.


Constraints:

1 <= prices.length <= 3 * 104
0 <= prices[i] <= 104

### Решение


--------

## Rotate Array (Поворот массива)

Given an integer array nums, rotate the array to the right by k steps, where k is non-negative.

Задав целочисленный массив nums, поверните его вправо на k шагов, где k - неотрицательное число.

Example 1:

Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
Example 2:

Input: nums = [-1,-100,3,99], k = 2
Output: [3,99,-1,-100]
Explanation:
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]


Constraints:

1 <= nums.length <= 105
-231 <= nums[i] <= 231 - 1
0 <= k <= 105

### Алгоритм
Решение за 3 шага
- Переворачиваем исходный массив
- Переворачиваем первые 3 элемента перевернутого массива
- Переворачиваем остальные элементы массива

Такой алгоритм потребляет меньше памяти, за счет того, что мы работаем с одним и тем же массивом.


### Решение

public class RotateArray {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5, 6, 7};
        rotate(arr, 2);
    }

    private static void rotate(int[] nums, int k) {
        reverse(nums, 0, nums.length - 1);

        reverse(nums, 0, k - 1);

        reverse(nums, k, nums.length - 1);
    }

    private static void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}

-----

## Contains Duplicate (Содержит дубликаты)

Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

Если задан целочисленный массив nums, верните true, если любое значение встречается в массиве хотя бы дважды, и верните false, если каждый элемент отличается от другого.

Example 1:

Input: nums = [1,2,3,1]

Output: true

Explanation:

The element 1 occurs at the indices 0 and 3.

Example 2:

Input: nums = [1,2,3,4]

Output: false

Explanation:

All elements are distinct.

Example 3:

Input: nums = [1,1,1,3,3,4,3,2,4,2]

Output: true

Constraints:

1 <= nums.length <= 105
-109 <= nums[i] <= 109

### Алгоритм

1) Для решения поиска дубликата в массиве используем HashSet - структура данных, которая имеет только уникальные значения, но не гарантирует порядок добавления элементов. Т.к. нам не важен порядок, то можно его использовать.
2) Проходим по каждому элементу массива и проверяем есть ли он в HashSet, если есть, то возвращаем true.


### Решение

package com.ki.tasks.array;

import java.util.HashSet;

public class TwiceElementInArray {
public static void main (String[] args) {
int[] nums = {1,2,3,1};
System.out.println(containsDuplicate(nums));

        int[] nums2 = {1,2,3};
        System.out.println(containsDuplicate(nums2));

        int[] nums3 = {1,2,3,4,5,4};
        System.out.println(containsDuplicate(nums3));
    }

    private static boolean containsDuplicate(int[] nums) {
        HashSet<Integer> hashSet = new HashSet<>();

        for (int num : nums) {
            if (hashSet.contains(num)) {
                return true;
            }
            hashSet.add(num);
        }

        return false;
    }

}

-------

## Single Number (Одиночный номер)

Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

В непустом массиве целых чисел nums каждый элемент встречается дважды, кроме одного. Найдите этот единственный элемент.

Вы должны реализовать решение с линейной сложностью во время выполнения и использовать только постоянное дополнительное пространство.


Example 1:

Input: nums = [2,2,1]
Output: 1
Example 2:

Input: nums = [4,1,2,1,2]
Output: 4
Example 3:

Input: nums = [1]
Output: 1


Constraints:

1 <= nums.length <= 3 * 104
-3 * 104 <= nums[i] <= 3 * 104
Each element in the array appears twice except for one element which appears only once.

### Алгоритм

- Для поиска числа, которое не повторяется, используем побитовое сравнение XOR.
- Вводим переменную int result = 0
- Проходимся по массиву и сравниваем с 0
- 2 одинаковых числа обнуляются

Также можно решить через HashSet, но если в задаче сказано, что **использовать только постоянное дополнительное пространство**, то это значит, что нельзя использовать дополнительные структуры данных.

### Решение

package com.ki.tasks.array;

import java.util.HashSet;

public class SingleNumber {
public static void main (String[] args) {
        int[] nums1 = {1,1,2,3,5,5,2};
        int[] nums2 = {1,1,2};

        System.out.println(getSingleNumber(nums1));
        System.out.println(getSingleNumber(nums2));

        System.out.println(getSingleNumberViaHashSet(nums1));
        System.out.println(getSingleNumberViaHashSet(nums2));
    }

    private static int getSingleNumber(int[] nums) {
    int result = 0;

        for (int num : nums) {
            result = result ^ num;
        }

        return result;
    }

    private static int getSingleNumberViaHashSet(int[] nums) {
    HashSet<Integer> hashSet = new HashSet<>();

        for (int num: nums) {
            if (hashSet.contains(num)) {
                hashSet.remove(num);
            } else {
                hashSet.add(num);
            }
        }

        return hashSet.iterator().next();

    }
}

----------

## Intersection of Two Arrays II (Пересечение двух массивов II) 

Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays and you may return the result in any order.

Если даны два целочисленных массива nums1 и nums2, верните массив их пересечения. Каждый элемент в результате должен встречаться столько раз, сколько раз он отображается в обоих массивах, и вы можете вернуть результат в любом порядке.

Example 1:

Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
Example 2:

Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
Explanation: [9,4] is also accepted.


Constraints:

1 <= nums1.length, nums2.length <= 1000
0 <= nums1[i], nums2[i] <= 1000


Follow up:

What if the given array is already sorted? How would you optimize your algorithm?
What if nums1's size is small compared to nums2's size? Which algorithm is better?
What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

### Алгоритм

1) Создаем HashMap<Integer, Integer> для 1ого массива и записываем туда key - это значение из массива 1 и value - это сколько раз встречается (hashMap.put(key, hashMap.getOrDefault(key, 0) + 1))
2) Создаем ArrayList для результата пересечений. Если элемент из 2ого массива находится как ключ hashMap, то добавляем его в ArrayList и отнимает количество из hashMap
3) Переводим ArrayList в обычный массив размеров new int[result.size()]

### Решение

package com.ki.tasks.array;

import java.util.Arrays;
import java.util.Map;
import java.util.HashMap;
import java.util.List;
import java.util.ArrayList;

public class IntersectionOfTwoArrays {
    public static void main (String[] args) {
        int[] int1 = {1,2,3,1,3,3,3,2,4,4,5,6,5};
        int[] int2 = {2,2,4,7,1};

        System.out.println(Arrays.toString(intersect(int1, int2)));
    }

    private static int[] intersect (int[] int1, int[] int2) {
       Map<Integer, Integer> hashMapForInt1 = new HashMap<>();

       for (int num : int1) {
            hashMapForInt1.put(num, hashMapForInt1.getOrDefault(num, 0) + 1);
       }

       System.out.println(hashMapForInt1);

       List<Integer> result = new ArrayList<>();

       for (int num : int2) {
            if (hashMapForInt1.containsKey(num) && hashMapForInt1.get(num) > 0) {
                result.add(num);
                hashMapForInt1.put(num, hashMapForInt1.get(num) - 1);
            }
       }

       int[] resultArray = new int[result.size()];
       for (int i = 0; i < result.size(); i++) {
            resultArray[i] = result.get(i);
       }

       return resultArray;

    }
}

-------

## Plus One (Плюс один)

You are given a large integer represented as an integer array digits, where each digits[i] is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.
Increment the large integer by one and return the resulting array of digits.

Вам дано большое целое число, представленное в виде целочисленного массива digits, где каждая digits[i] - это i-я цифра целого числа. Цифры упорядочены от наибольшего значения к наименьшему в порядке слева направо. Большое целое число не содержит ведущих 0.
Увеличьте большое целое число на единицу и верните полученный массив цифр.


Example 1:

Input: digits = [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Incrementing by one gives 123 + 1 = 124.
Thus, the result should be [1,2,4].
Example 2:

Input: digits = [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
Incrementing by one gives 4321 + 1 = 4322.
Thus, the result should be [4,3,2,2].
Example 3:

Input: digits = [9]
Output: [1,0]
Explanation: The array represents the integer 9.
Incrementing by one gives 9 + 1 = 10.
Thus, the result should be [1,0].



### Алгоритм
- Проходим по массиву с обратной стороны, т.е. если массив {1,2,3}, то начинаем с 3 и увеличиваем на 1, получаем 4
- Затем 4 проверяем с 10, если меньше, то возвращаем число
- Допустим у нас {1,2,3,9}, то идем по массиву с 9 и увеличиваем на 1, получаем 10, 10 не меньше 10, значит 3 индекс массива обнуляем 0 и переходим к следующему индексу массива, а там 3, увеличиваем на 1, получаем 4, 4 < 10 - возвращаем массив 1,2,4,0
- Если у нас {9,9}, то начинаем с 9 с конца, увеличиваем на 1, получаем 10, обнуляем и переводим указатель на следующий индекс, там тоже 9 - обнуляем и переводим указатель, но цикл закончился, значит нам надо создать новый массив, у которого будет размер больше на 1, чем исходный, т.е. int[] result = new int[digits.length + 1]. В result[0] = 1, получаем {1,0,0} 

### Решение

package com.ki.tasks.array;

import java.util.*;

public class PlusOne {
    public static void main(String[] args) {
        int[] digits = {1,2,3};
        System.out.println(Arrays.toString(plusOne(digits)));

        int[] digits1 = {1,2,9};
        System.out.println(Arrays.toString(plusOne(digits1)));

        int[] digits2 = {9};
        System.out.println(Arrays.toString(plusOne(digits2)));
    }

    private static int[] plusOne(int[] digits) {
        for (int i = digits.length - 1; i >= 0; i--) {
            System.out.println(digits[i]);
            digits[i]++;
            if (digits[i] < 10) {
                return digits;
            }

            digits[i] = 0;
        }

        int[] result = new int[digits.length + 1];
        result[0] = 1;

        return result;
    }

}

--------

## Move Zeroes (Переставьте нули)

Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.
Note that you must do this in-place without making a copy of the array.

Задав целочисленный массив nums, переместите все 0 в его конец, сохранив относительный порядок ненулевых элементов.
Обратите внимание, что вы должны сделать это на месте, не создавая копию массива.


Example 1:

Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
Example 2:

Input: nums = [0]
Output: [0]


Constraints:

1 <= nums.length <= 104
-231 <= nums[i] <= 231 - 1


Follow up: Could you minimize the total number of operations done?

### Алгоритм
- Создаем переменную nonZeroIndex - это индекс не нулевого элемента. Изначально он 0;
- Проходим по массиву и если не нулевой элемент, то ставим его на индекс nonZeroIndex и nonZeroIndex увеличиваем на 1
- Оставшиеся элементы массива заполняем нулями, т.е. i = nonZeroIndex; i < nums.length; i++ 


### Решение

package com.ki.tasks.array;

import java.util.*;

public class MovesZeroes {
    public static void main(String[] args) {
        int[] nums = {0,1,0,3,12};

        System.out.println(Arrays.toString(movesZeroes(nums)));
    }

    private static int[] movesZeroes(int[] nums) {
        int nonZeroIndex = 0;

        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != 0) {
                nums[nonZeroIndex] = nums[i];
                nonZeroIndex++;
            }
        }

        for (int i = nonZeroIndex; i < nums.length; i++) {
            nums[i] = 0;
        }

        return nums;
    }

}

--------

## Two Sum (Две суммы)

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

Учитывая массив целых чисел nums и целое число target, верните индексы этих двух чисел так, чтобы их сумма равнялась target.
Вы можете предположить, что каждый вход будет иметь ровно одно решение, и не можете использовать один и тот же элемент дважды.
Вы можете возвращать ответы в любом порядке.

Example 1:

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
Example 2:

Input: nums = [3,2,4], target = 6
Output: [1,2]
Example 3:

Input: nums = [3,3], target = 6
Output: [0,1]


Constraints:

2 <= nums.length <= 104
-109 <= nums[i] <= 109
-109 <= target <= 109
Only one valid answer exists.


Follow-up: Can you come up with an algorithm that is less than O(n2) time complexity?

### 



###