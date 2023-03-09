# I. Поиск

Функция для поиска полным перебором. При нахождении нужного элемента возвращает индекс элемента в массиве, а если элемент не найден, возвращает -1.
```C++
 int perebor(int arr[], int n, int key)
{
    for(int i=0; i<n; i++){
        if(arr[i] == key){
            return i;
        }
    }
    return -1;
}
```

Среднее время:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab1/images/%D1%81%D1%80%D0%B5%D0%B4%D0%BD%D0%B5%D0%B5%20%D0%B2%D1%80%D0%B5%D0%BC%D1%8F/%D0%BF%D0%B5%D1%80%D0%B5%D0%B1%D0%BE%D1%80.png)

Худшее время:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab1/images/%D1%85%D1%83%D0%B4%D1%88%D0%B5%D0%B5%20%D0%B2%D1%80%D0%B5%D0%BC%D1%8F/%D0%BF%D0%B5%D1%80%D0%B5%D0%B1%D0%BE%D1%80.png)

Функция для бинраного поиска. При нахождении нужного элемента возвращает индекс элемента в массиве, а если элемент не найден, возвращает -1.
```C++
int binary(int arr[], int n, int key)
{
    int left=0, right=n-1;
    int middle;
    bool is_found = false;

    while(left <= right && !is_found){
        middle = (left + right)/2;

        if(arr[middle] == key){
            is_found = true;
        }

        else if(arr[middle] > key){
            right = middle - 1;
        }

        else{
            left = middle + 1;
        }
    }
    if(is_found) return middle;
    else return -1;
}
```

Среднее время:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab1/images/%D1%81%D1%80%D0%B5%D0%B4%D0%BD%D0%B5%D0%B5%20%D0%B2%D1%80%D0%B5%D0%BC%D1%8F/%D0%B1%D0%B8%D0%BD%D0%B0%D1%80%D0%BD%D1%8B%D0%B9.png)

Худшее время:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab1/images/%D1%85%D1%83%D0%B4%D1%88%D0%B5%D0%B5%20%D0%B2%D1%80%D0%B5%D0%BC%D1%8F/%D0%B1%D0%B8%D0%BD%D0%B0%D1%80%D0%BD%D1%8B%D0%B9%20%D0%BF%D0%BE%D0%B8%D1%81%D0%BA.png)

Прямыми измерениями времени убеждаемся, что для функции с полным перебором время растёт линейно с увеличением размера массива, а для функции бинарного поиска логарифмически.

# II. Сумма двух

Требуется найти два различных элемента, сумма которых даёт заданное число.
Функция полного перебора
```C++
void sum_of_two_perebor(int arr[], int n, int key)
{
    for(int i=0; i<n-1; i++){
        for(int j=i+1; j<n; j++){
            if(arr[i] + arr[j] == key){
                break;
            }
        }
    }
}
```

Среднее время:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab1/images/%D1%81%D1%80%D0%B5%D0%B4%D0%BD%D0%B5%D0%B5%20%D0%B2%D1%80%D0%B5%D0%BC%D1%8F/%D1%81%D1%83%D0%BC%D0%BC%D0%B0%20%D0%B4%D0%B2%D1%83%D1%85%20%D0%BF%D0%B5%D1%80%D0%B5%D0%B1%D0%BE%D1%80.png)

Худшее время:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab1/images/%D1%85%D1%83%D0%B4%D1%88%D0%B5%D0%B5%20%D0%B2%D1%80%D0%B5%D0%BC%D1%8F/%D1%81%D1%83%D0%BC%D0%BC%D0%B0%20%D0%B4%D0%B2%D1%83%D1%85%20%D0%BF%D0%B5%D1%80%D0%B5%D0%B1%D0%BE%D1%80.png)

Функция с линейной зависимостью:
```C++
void sum_of_two_n(int arr[], int n, int key)
{
    int left=0, right=n-1;
    while((left < right) && (arr[left] + arr[right] != key)){
        if(arr[left] + arr[right] > key){
            right--;
        }
        else{
            left++;
        }
    }
}
```

Среднее время:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab1/images/%D1%81%D1%80%D0%B5%D0%B4%D0%BD%D0%B5%D0%B5%20%D0%B2%D1%80%D0%B5%D0%BC%D1%8F/%D1%81%D1%83%D0%BC%D0%BC%D0%B0%20%D0%B4%D0%B2%D1%83%D1%85%20n.png)

Худшее время:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab1/images/%D1%85%D1%83%D0%B4%D1%88%D0%B5%D0%B5%20%D0%B2%D1%80%D0%B5%D0%BC%D1%8F/%D1%81%D1%83%D0%BC%D0%BC%D0%B0%20%D0%B4%D0%B2%D1%83%D1%85%20n.png)

Прямыми измерениями времени убеждаемся, что функция полного перебора имеет квадратичную зависимость, а вторая функция линейную.

# III. Часто используемый элемент

Искать элемент будем функцией перебора из пункта I.

Рассмотрим два случая.
В первом случае при выборе элемента, который необходимо найти, каждый элемент из массива выбирается с одной вероятностью.
Во втором случае случайный элемент из массива выбирается неравномерно.

## Стратегия A

Если мы нашли элемент в массиве, меняем его местами с первым элементом.

```C++
void strategyA(int arr[], int index)
{
    int temp=arr[0];
    arr[0] = arr[index];
    arr[index] = temp;
}
```

Равномерный рандом:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab1/images/%D1%81%D1%82%D1%80%D0%B0%D1%82%D0%B5%D0%B3%D0%B8%D0%B8/%D1%80%D0%B0%D0%B2%D0%BD%D0%BE%D0%BC%D0%B5%D1%80%D0%BD%D0%BE/A.png)

Неравномерый рандом:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab1/images/%D1%81%D1%82%D1%80%D0%B0%D1%82%D0%B5%D0%B3%D0%B8%D0%B8/%D0%BD%D0%B5%D1%80%D0%B0%D0%B2%D0%BD%D0%BE%D0%BC%D0%B5%D1%80%D0%BD%D0%BE/A.png)

## Стратегия B

Если нашли элемент в массиве, меняем его местами с элементом левее его.

```C++
void strategyB(int arr[], int index)
{
    int temp=arr[index];
    arr[index] = arr[index - 1];
    arr[index - 1] = temp;
}
```

Равномерный рандом:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab1/images/%D1%81%D1%82%D1%80%D0%B0%D1%82%D0%B5%D0%B3%D0%B8%D0%B8/%D1%80%D0%B0%D0%B2%D0%BD%D0%BE%D0%BC%D0%B5%D1%80%D0%BD%D0%BE/B.png)

Неравномерный рандом:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab1/images/%D1%81%D1%82%D1%80%D0%B0%D1%82%D0%B5%D0%B3%D0%B8%D0%B8/%D0%BD%D0%B5%D1%80%D0%B0%D0%B2%D0%BD%D0%BE%D0%BC%D0%B5%D1%80%D0%BD%D0%BE/B.png)

## Стратегия C

Вводится дополнительный массив счётчиков. Каждый раз, когда находится элемент массива, увеличиваем соответствующий ему счётчик на один и если счётчик найденного элемента больше счётчика элемента слева, меняем их метсами.

```C++
void strategyC(int arr[], int index, int counters[])
{
    int temp;
    counters[index]++;
    if(counters[index] > counters[index-1]){
        temp = arr[index];
        arr[index] = arr[index - 1];
        arr[index - 1] = temp;

        temp = counters[index];
        counters[index] = counters[index - 1];
        counters[index - 1] = temp;
    }
}
```

Равномерный рандом:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab1/images/%D1%81%D1%82%D1%80%D0%B0%D1%82%D0%B5%D0%B3%D0%B8%D0%B8/%D1%80%D0%B0%D0%B2%D0%BD%D0%BE%D0%BC%D0%B5%D1%80%D0%BD%D0%BE/C.png)

Неравномерный рандом:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab1/images/%D1%81%D1%82%D1%80%D0%B0%D1%82%D0%B5%D0%B3%D0%B8%D0%B8/%D0%BD%D0%B5%D1%80%D0%B0%D0%B2%D0%BD%D0%BE%D0%BC%D0%B5%D1%80%D0%BD%D0%BE/C.png)

Прямыми иземерениями времени убеждаемся, что при равномерном и неравномерном рандоме время поиска при данной стратегии не изменяется. Более того, при любой стратегии время поиска одно и то же.
