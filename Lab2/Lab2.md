# Лабораторная работа II. Сортировки
## I. Шейкерная сортировка.
При написании сортировки проводилась декомпозиция: отдельно были написаны функции проходов в одну и в другую сторону и сама сортировка, использующая эти функции.
```C++
void forward_step(unsigned *arr, unsigned const begin_i, unsigned const end_i)
{
    unsigned temp;
    for(unsigned i=begin_i; i<end_i; i++)
    {
        if(arr[i] > arr[i+1])
        {
            temp = arr[i];
            arr[i] = arr[i+1];
            arr[i+1] = temp;
        }
    }
}

void backward_step(unsigned *arr, unsigned const begin_i, unsigned const end_i)
{
    unsigned temp;
    for(unsigned i=end_i; i>begin_i; i--)
    {
        if(arr[i] < arr[i-1])
        {
            temp = arr[i];
            arr[i] = arr[i-1];
            arr[i-1] = temp;
        }
    }
}

void shaker_sort(unsigned *arr, unsigned begin_i, unsigned end_i)
{
    while(begin_i < end_i)
    {
        forward_step(arr, begin_i, end_i);
        backward_step(arr, begin_i, end_i);
        begin_i++;
        end_i--;
    }
}
```

Среднее время:

![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab2/images/shaker.png)

График в логарифмическом масштабе:

![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab2/images/shaker%20log.png)

Как видно из графика в логарифмическом масштабе, зависимость времени от размера степенная. С точностью показатель степени равен 2.0817214934973447, таким образом доказано, что зависимость квадратичная.

Среднее время для прямого прохода:

![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab2/images/forward%20step.png)

Логарифмический масштаб:

![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab2/images/forward%20step%20log.png)

Показатель степени равен 2.1071723529592754

Среднее время для обратного прохода:

![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab2/images/backward%20step.png)

Логарифмический масштаб:

![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab2/images/backward%20step%20log.png)

Показатель степени равен 2.138773131646597


Во-первых, из графиков видно, что время слабо завист от размера массива при малых значениях, а при больших зависимость O(N^2).
Во-вторых, сортировка пузырьком с использованием только прямого или обратного прохода немного медленнее, чем шейкерная сортировка, использующая оба прохода.

## II. Сортировка расчёской.
```C++
void comb_sort(unsigned *arr, unsigned length)
{
    double factor = 1.2473309;
    unsigned step = length - 1, temp;

    while(step >= 1)
    {
        for(unsigned i = 0; i + step < length; i++)
        {
            if(arr[i] < arr[i+step])
            {
                temp = arr[i];
                arr[i] = arr[i+step];
                arr[i+step] = temp;
            }

        }
        step /= factor;
    }
}
```
Среднее время:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab2/images/comb.png)

Известно, что ассимптотика должны быть O(nlog(n)). Чтобы проверить это, разделим значение времени на nlog(n). Тогда график должен иметь вид константы.

![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab2/images/comb%20check.png)

Как видно из графика, действительно получилась прямая линия. Значит, ассимтотика алгоритма действительно O(nlog(n))
Как и в шейкерной сортировке, здесь время слабо зависит от размера массива при малых значениях. Разброс особо сильно заметен на втором графике. Чем больше расзмер массива, теб болеее стабильным становится график.

## III. Сортировка Шелла

### 1.

Шаг: d_i = d_i-1 / 2

```C++
void shell_sort_1(unsigned *arr, unsigned length)
{

    unsigned temp;
    for(unsigned d = length/2; d > 0; d /= 2)
    {
        for(unsigned i = d; i < length; i++)
        {
            for(unsigned j = i; j >= d; j -= d)
            {
                if(arr[j] < arr[j-d])
                {
                    temp = arr[j];
                    arr[j] = arr[j-d];
                    arr[j-d] = temp;
                }
            }
        }
    }
}
```

Среднее время:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab2/images/shell%201.png)

График в логарифмическом масштабе:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab2/images/shell%201%20check.png)

Наклон графика равен 1.932.
То есть, ассимптотика близка к O(n^2)

### 2.

Шаг: d_i = 2^i - 1 — последовательность Хиббарда

```C++
void shell_sort_2(unsigned *arr, unsigned length)
{
    unsigned temp;
    unsigned power = floor(log2(length));
    unsigned d = exp(power * log(2)) - 1;
    while(d>0)
    {
        for(unsigned i = d; i < length; i++)
        {
            for(unsigned j = i; j >= d; j -= d)
            {
                if(arr[j] < arr[j-d])
                {
                    temp = arr[j];
                    arr[j] = arr[j-d];
                    arr[j-d] = temp;
                }
            }
        }
        d = (d + 1) / 2 - 1;
    }
}
```

Среднее время:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab2/images/shell%202.png)

График в логарифмическом масштабе:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab2/images/shell%202%20check.png)

Наклон графика равен 1.854
Ассимптотика близка к O(n^2), но быстрее, чем в п. 1

### 3.

Шаг — обратная последовательность фибоначчи

```C++
void shell_sort_3(unsigned *arr, unsigned length, unsigned *fibonacci)
{
    unsigned i=0, s=0, temp;
    while(fibonacci[i++] <= length) s++;

    unsigned d=fibonacci[--s];
    while(d>0)
    {
        for(unsigned i = d; i < length; i++)
        {
            for(unsigned j = i; j >= d; j -= d)
            {
                if(arr[j] < arr[j-d])
                {
                    temp = arr[j];
                    arr[j] = arr[j-d];
                    arr[j-d] = temp;
                }
            }
        }
        d = fibonacci[--s];
    }
}
```

fibonacci — это массив с числами фибоначчи; на нулевом месте ноль.

Среднее время:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab2/images/shell%203.png)

График в логарифмическом масштабе:
![](https://github.com/Squirrrel42/Infa-term-2/blob/main/Lab2/images/shell%203%20check.png)

Наклон графика равен 1.984
Ассимптотика близка к O(n^2)

Самой эффективной сортировкой Шелла из рассмотренных оказалась сортировка с последовательностью Хиббарда.

