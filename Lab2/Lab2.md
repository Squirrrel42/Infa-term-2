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
