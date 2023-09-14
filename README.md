# Reverse-Integer
Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-2**31, 2**31 - 1], then return 0.

Assume the environment does not allow you to store 64-bit integers (signed or unsigned).

 

Example 1:

Input: x = 123
Output: 321
Example 2:

Input: x = -123
Output: -321
Example 3:

Input: x = 120
Output: 21

# Intuition
Интуитивно, мы можем использовать математические операции для обращения числа x. Одна из возможных стратегий - это извлечение последней цифры от x и добавление ее к результирующему числу. Затем мы можем делить x на 10, чтобы удалить последнюю цифру. Этот процесс будет продолжаться до тех пор, пока x не станет равным 0

# Approach
При выполнении этого подхода необходимо учитывать особые случаи, такие как отрицательные числа и переполнение. Если x отрицательное число, мы должны сохранить знак - и работать с абсолютным значением x. Если обращение числа приводит к выходу за пределы диапазона 32-разрядных целых чисел, мы должны вернуть 0.

Такой подход позволяет нам решить задачу без необходимости преобразования числа в строку.

# Complexity
- Time complexity:
Временная сложность: O(log(x)), где x - входное число. Мы выполняем операцию деления на 10 для каждой цифры в числе x, поэтому количество итераций цикла while равно количеству цифр в x, то есть log(x) по основанию 10.

- Space complexity:
Пространственная сложность: O(1). Мы используем только константное количество дополнительной памяти для хранения переменных reversed, digit и x.
```C++ []
int reverse(int x) {
    int reversed = 0;
    while (x != 0) {
        int digit = x % 10;
        x /= 10;
        
        // Проверка на переполнение
        if (reversed > INT_MAX / 10 || (reversed == INT_MAX / 10 && digit > 7))
            return 0;
        if (reversed < INT_MIN / 10 || (reversed == INT_MIN / 10 && digit < -8))
            return 0;
        
        reversed = reversed * 10 + digit;
    }
    
    return reversed;
    }
```
```python []
def reverse(self, x: int) -> int:
    reversed = 0
    sign = -1 if x < 0 else 1
    x = abs(x)
    
    while x != 0:
        digit = x % 10
        x //= 10
        
        # Проверка на переполнение
        if reversed > (2**31 - 1) // 10 or (reversed == (2**31 - 1) // 10 and digit > 7):
            return 0
        if reversed < (-2**31) // 10 or (reversed == (-2**31) // 10 and digit > 8):
            return 0
        
        reversed = reversed * 10 + digit
    
    return sign * reversed
```
```ruby []
# @param {Integer} x
# @return {Integer}
def reverse(x)
    reversed = 0
    sign = x < 0 ? -1 : 1
    x = x.abs
    
    while x != 0
        digit = x % 10
        x /= 10
        
        # Проверка на переполнение
        if reversed > (2**31 - 1) / 10 || (reversed == (2**31 - 1) / 10 && digit > 7)
            return 0
        end
        if reversed < (-2**31) / 10 || (reversed == (-2**31) / 10 && digit < -8)
            return 0
        end
        
        reversed = reversed * 10 + digit
    end
    
    return sign * reversed
end
```
```java []
public int reverse(int x) {
    int reversed = 0;
    
    while (x != 0) {
        int digit = x % 10;
        x /= 10;
        
        // Проверка на переполнение
        if (reversed > Integer.MAX_VALUE / 10 || (reversed == Integer.MAX_VALUE / 10 && digit > 7))
            return 0;
        if (reversed < Integer.MIN_VALUE / 10 || (reversed == Integer.MIN_VALUE / 10 && digit < -8))
            return 0;
        
        reversed = reversed * 10 + digit;
    }
    
    return reversed;
    }
```

```C# []
int reverse(int x)
{
    int reversed = 0;

    while (x != 0)
    {
        int digit = x % 10;
        x /= 10;

        // Проверка на переполнение
        if (reversed > int.MaxValue / 10 || (reversed == int.MaxValue / 10 && digit > 7))
            return 0;
        if (reversed < int.MinValue / 10 || (reversed == int.MinValue / 10 && digit < -8))
            return 0;

        reversed = reversed * 10 + digit;
    }

    return reversed;
}

```
```C []
int reverse(int x){
    int reversed = 0;
    while (x != 0) {
        int digit = x % 10;
        x /= 10;
        
        // Проверка на переполнение
        if (reversed > INT_MAX / 10 || (reversed == INT_MAX / 10 && digit > 7))
            return 0;
        if (reversed < INT_MIN / 10 || (reversed == INT_MIN / 10 && digit < -8))
            return 0;
        
        reversed = reversed * 10 + digit;
    }
    
    return reversed;
}
```
```JavaScript []
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
    let reversed = 0;
    let sign = x < 0 ? -1 : 1;
    x = Math.abs(x);

    while (x !== 0) {
        let digit = x % 10;
        x = Math.floor(x / 10);

        // Проверка на переполнение
        if (reversed > (Math.pow(2, 31) - 1) / 10 || (reversed === (Math.pow(2, 31) - 1) / 10 && digit > 7)) {
            return 0;
        }
        if (reversed < -(Math.pow(2, 31)) / 10 || (reversed === -(Math.pow(2, 31)) / 10 && digit < -8)) {
            return 0;
        }

        reversed = reversed * 10 + digit;
    }

    return sign * reversed;
};
```
