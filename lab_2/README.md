Лабораторная работа №2:
Знакомство с bash-скриптами(сценариями)


1.Добавление Шебанг(абсолютный путь к интерпретатору bash)

    #!/bin/bash

2.Разделение входной строки по ".", проверка полученных значений, их присваивание элементам массива. 

Точка добавлена в конец str, чтобы последняя часть адреса не потерялась.

last - первое числовое значение следующее за ".".

count - индекс элемента из array

array() - сам массив

    str=$1 
    str+='.'
    last=0
    count=0
    array=()

В цикле for проходимся по всем элементам str, если элемент не явлвяется цифрой, то по хорошему, это должно значить, что мы встретили наш разделитель - ".".
Тогда находим длину цепочки из цифр и прсваиваем элементу массива числовую строку. После проверяем, не превосходит ли значение 255. В случае, превышения максимально допустимого десятичного значения программа предварительно завершается и выводится сообщение об ошибке.

    # разделение строки
    for (( i=0; i<${#str}; i++ )); do 
        elem="${str:$i:1}" 
        if ! [[ $elem =~ [0-9] ]]; then
            let len=i-last    
            array[$count]="${str:$last:$len}"
   
            # проверка на корректность 
            if (( array[$count] > 255 )); then
                echo "---Incorrect IP---"
                exit 1
            fi
     
            let last=i+1
            let count=count+1
  
        fi
    done

3.Снова проверка. Состоит ли точно наш адрес только из 4 элементов.

    # проверка на корректность
    if (( ${#array[@]} != 4 )); then
        echo "---Incorrect IP---"
        exit 1
    fi

4.Перевод в двоичную систему счисления. Создается массив всевозможных бинарных восьмизначных чисел.
Получится 2^8 = 256 значений, где CONV[i] = двоичная запись десятичного числа i, где i = 0, 1, 2, ... , 255. В цикле for для каждой части ip находим его двоичную запись и соеднияем в переменную answer. При выводе, лишнюю точку не выводим.

    answer=""
    CONV=({0..1}{0..1}{0..1}{0..1}{0..1}{0..1}{0..1}{0..1})
    for i in ${array[@]}; do
        answer+=${CONV[$i]}
        answer+="."
    done

    echo ${answer[@]:0:35}


Скриншот файла целиком:



![](https://private-user-images.githubusercontent.com/180977102/387310550-8a9ea62b-93e3-416a-80f2-e6f0378391da.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM4NDY5OTEsIm5iZiI6MTczMzg0NjY5MSwicGF0aCI6Ii8xODA5NzcxMDIvMzg3MzEwNTUwLThhOWVhNjJiLTkzZTMtNDE2YS04MGYyLWU2ZjAzNzgzOTFkYS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjEwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIxMFQxNjA0NTFaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT03ZjcwMGRjZmUxOTIyOTVjNmM4YWJmNGQ5NGE1NTNhNTJmMGRjMTg1NzVmYjM0NmFkYmZmOWZlNmZiNjVjNzA3JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.Nu9HNJvonKYr4ginoo83y74n_-wo45vT36AS7Aspmjo)



Пример её работы:



![](https://private-user-images.githubusercontent.com/180977102/387310547-081f7071-b16f-454a-bece-2066a4b67c72.jpeg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM4NDY5OTEsIm5iZiI6MTczMzg0NjY5MSwicGF0aCI6Ii8xODA5NzcxMDIvMzg3MzEwNTQ3LTA4MWY3MDcxLWIxNmYtNDU0YS1iZWNlLTIwNjZhNGI2N2M3Mi5qcGVnP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQVZDT0RZTFNBNTNQUUs0WkElMkYyMDI0MTIxMCUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyNDEyMTBUMTYwNDUxWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9M2M3MjQ3ZThjN2VlYjU4NGIwYzQ2NWE3NGRlMWMwNGE2MTQ4N2ZiMmM5YjkwYzc5YmM1YjUyMWVlZDg3NmRhYSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.PIbdvj_7whL5wk33K1ImheJ2aOI_02JDRK2dUYjaPVY)