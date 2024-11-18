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



![img_1.png](https://private-user-images.githubusercontent.com/180977102/387310543-a7cadcf9-dc5a-46fc-9d42-6e496f9d87ed.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzE5NDg2MzgsIm5iZiI6MTczMTk0ODMzOCwicGF0aCI6Ii8xODA5NzcxMDIvMzg3MzEwNTQzLWE3Y2FkY2Y5LWRjNWEtNDZmYy05ZDQyLTZlNDk2ZjlkODdlZC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMTE4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTExOFQxNjQ1MzhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT05NzY3OWM3ODU1YTc3NjViZWNhNDRmYmU1NmY1MGI0MTZkYjc5YzE0MjM2ZjY0ODg4ZTUwYjEzN2M5ZWM3ZTcyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.nEQHWxaRZcuk8HERK0aBMZPGAq8-UZzne-v6kXOabJ0)




Пример её работы:



![img.png](https://private-user-images.githubusercontent.com/180977102/387310535-21cbcf2f-bb61-41c7-a89a-f2c1428caada.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzE5NDg2MzgsIm5iZiI6MTczMTk0ODMzOCwicGF0aCI6Ii8xODA5NzcxMDIvMzg3MzEwNTM1LTIxY2JjZjJmLWJiNjEtNDFjNy1hODlhLWYyYzE0MjhjYWFkYS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMTE4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTExOFQxNjQ1MzhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1hZTU2YWYwOGIyNTViMjY4MWRkNzIyZDc1YWNiYTdhNzQ2NDY2MTBmZjEzY2YzMGM4N2MyZDcxYjNiNzRlMjI0JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.k_fcwhjXcLjTOtqArsGyZ_FPLhYCDWeqnkURIm8ng24)
