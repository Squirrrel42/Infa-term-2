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

