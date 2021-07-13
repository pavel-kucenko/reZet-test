### Задача 1
В массиве, содержащем 3 или более чисел, определить подходит ли
каждая группа из трех чисел условию a > b < c или a < b > c. Оформить
решение в виде функции которая принимает исходный массив и возвращает
массив с результатом проверки каждой группы, где 1 удовлетворяет
условию и 0 - нет.

Например:
Исходный массив:
```
[1, 3, 5, 4, 5, 7]
```
Рассмотрим каждую группу:
1, 3, 5 => 1 < 3 < 5 - нет
3, 5, 4 => 3 < 5 > 4 - да
5, 4, 5 => 5 > 4 < 5 - да
4, 5, 7 => 4 < 5 < 7 - нет
Результат:
```
[0, 1, 1, 0]
```
### Решение:
```
function checkArr(arr) {
    let result = [];

    return function control() {
        if (arr.length >= 3) {
           let check = arr.slice(0,3);
           if((check[0] > check[1] && check[1] < check[2]) || (check[0] < check[1] && check[1] > check[2])) {
            result.push(1);
           } else {
               result.push(0);
           }
           arr.splice(0,1);
           control()                     
        }
        return result;
    }
  }  
  
  console.log(checkArr([1, 3, 5, 4, 5, 7])()); // [0, 1, 1, 0]
```
### Задача 2
Дана матрица из целых чисел от 1 до 9, размером 3 * N, где N может быть
больше либо равна 3. Необходимо определить содержит ли каждый участок
матрицы 3 * 3 все числа от 1 до 9.
Например:
Входные данные:
```
[
[1,2,3,2,7]
[4,5,6,8,1]
[7,8,9,4,5]
]
```
1 участок:
1 2 3
4 5 6
7 8 9
содержит все цифры от 1 до 9
2 участок:
2 3 2
5 6 8
8 9 4
не содержит все цифры от 1 до 9
3 участок:
3 2 7
6 8 1
9 4 5
содержит все цифры от 1 до 9
Результат:
```
[true, false, true]
```
### Решение
```
function checkArr(arr) {
    let result = [];
    
    return function control() {
        if (arr[0].length >= 3) {
            let uniqArray = [];
            for(let i=0;i < 3;i++) {
                uniqArray.push(arr[i].slice(0,3));
                arr[i].splice(0,1);
            }
            uniqArray = [...new Set([...uniqArray[0], ...uniqArray[1], ...uniqArray[2]])]
            if (uniqArray.length == 9) {
                result.push(true)
            } else {
                result.push(false);
            }
            control()
        }
        return result;
    }    
    
}
console.log(checkArr([[1, 2, 3, 2, 7], [4, 5, 6, 8, 1], [7, 8, 9, 4, 5]])()); // [true, false, true]
```
