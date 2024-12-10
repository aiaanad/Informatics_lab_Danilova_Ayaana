## Отчет к лабораторной работе №5
### Задание 1 - Автоматизация проверки формата файлов при коммите

1) Клонируем репозиторий и переходим в папку лабораторной
```bash
git clone <your repo url>
```
2) Для того чтобы добавить хук, достаточно изменить файл в директории, перейдем в .git/hooks/
```bash
cd .git/hooks
```
3) При создании репозитория также создаются примеры хуков. Для того чтобы начать их использовать, достаточно скопировать интересующий файл, убрав постфикс .sample
```bash
cp pre-commit.sample pre-commit
```
4) Пропишем необходимый скрипт
```bash
#!/bin/bash

for file in $(git diff --cached --name-only | grep '.txt$'); do
        # Проверяем, что файл не пустой
        if [ ! -s "$file" ]; then
                echo "Ошибка: Файл '$file' пустой."
                error_found=true
        fi

        #Проверка на упоминание лабы в имени файла
        if [[ $file == *"lab"* ]]; then
                echo "'$file' содержит lab."
        else
                echo "ERROR. '$file' не содержит lab."
                error_found=true
        fi

        last_line=$(tail -n 1 "$file")
        if [[ $last_line == *"Autor:"* ]]; then
                echo "Автор подписал файл"

```
5) Дадим права на исполнение
```bash
chmod +x pre-commit
```
6) Пишем тестовые тексты и убеждаемся в работоспособности нашего хука
   
![](https://private-user-images.githubusercontent.com/180977102/394012275-9d5b2044-303f-4c47-adb5-b770c79c2ab2.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM3NzkxMzAsIm5iZiI6MTczMzc3ODgzMCwicGF0aCI6Ii8xODA5NzcxMDIvMzk0MDEyMjc1LTlkNWIyMDQ0LTMwM2YtNGM0Ny1hZGI1LWI3NzBjNzljMmFiMi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIwOVQyMTEzNTBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1kNzFlMWQyZmY2YTE2MGVhYzQzMjFjNmE4Y2Y1MDY0OTNlYjYwZjk4ZjQ5YTEyNDIyYmE2NWVkMjA5YTRlYzgxJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.FHbnJYAJRhrfdQ-zFj0wO2yKTlrKXS9SBrKjJlYhDyc)

![](https://private-user-images.githubusercontent.com/180977102/394012656-0741e3ac-2df7-406d-a3a9-3708115b7d8f.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM3NzkxMzAsIm5iZiI6MTczMzc3ODgzMCwicGF0aCI6Ii8xODA5NzcxMDIvMzk0MDEyNjU2LTA3NDFlM2FjLTJkZjctNDA2ZC1hM2E5LTM3MDgxMTViN2Q4Zi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIwOVQyMTEzNTBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT04YzJmMmUyNjU5NTVjOTQ3Njg0M2M1MmJmMjRlZTNiNmIzZmUzNzI0ODVlMjFmZjBkOWQ4MDcyYjY2NjVjNmI3JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.KOHm2p5QBjIkYwqoNO6om6I6RpYv2tr7U7hlEam2bwY)


### Задание 2 - Использование Git Flow в проекте

1) Проверим установлен ли git flow
```bash
git flow version
 ```
2) Создаем в директории пустой репозитарий в виде директория .git
   
![](https://private-user-images.githubusercontent.com/180977102/394327812-a99c28b2-d5e5-4ba3-80e5-dec74a3e3dbf.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM4NDMxNzcsIm5iZiI6MTczMzg0Mjg3NywicGF0aCI6Ii8xODA5NzcxMDIvMzk0MzI3ODEyLWE5OWMyOGIyLWQ1ZTUtNGJhMy04MGU1LWRlYzc0YTNlM2RiZi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjEwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIxMFQxNTAxMTdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0yMzdjNjk2MDkyM2Q3YmIzNTRlOThhOWE0MGYyZjljYzM0OGJhOGIxM2Y3NDlkOGQwZmNhZDRlNjIxN2FjN2NhJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.JGNvhD1mWAgHPBn_xSkkpP7t3hqYwTEp7NZHpe0qYO4)

3) Создаем ветку для новой функциональности "task-management"
   
![](https://private-user-images.githubusercontent.com/180977102/394328996-b14d2232-329f-4c22-b667-42da131008b4.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM4NDMzMzIsIm5iZiI6MTczMzg0MzAzMiwicGF0aCI6Ii8xODA5NzcxMDIvMzk0MzI4OTk2LWIxNGQyMjMyLTMyOWYtNGMyMi1iNjY3LTQyZGExMzEwMDhiNC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjEwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIxMFQxNTAzNTJaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT00NDNiZTI2Nzk3OGRmMjEwMDYxN2Q0NGFmMjZiMzAzOGE3YjNlMzhjODk0NTQ2YTAyNGNlZTIyMTAzNzY3ZGViJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.u_abYCanWgJPzlZoGJzOrejFMxAa-CRkc99Tka2s1qE)

4) Содержимое файла task_manager.py
   
![](https://private-user-images.githubusercontent.com/180977102/394320975-a660e396-2911-4371-b417-59c7a637f86c.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM4NDIyMTQsIm5iZiI6MTczMzg0MTkxNCwicGF0aCI6Ii8xODA5NzcxMDIvMzk0MzIwOTc1LWE2NjBlMzk2LTI5MTEtNDM3MS1iNDE3LTU5YzdhNjM3Zjg2Yy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjEwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIxMFQxNDQ1MTRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1mZWJmYTZjODg2NDQ3YzFkZjUzZjZhOGIxM2Y1ZDFkYTFkY2Q2YmZjMjJmZTE0NGRhZTI1NmI2MzVjYmE0ZmVmJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.3B6erQiljAkVjjT62wZeQwFBcsIX_eciOtFzn3Fh2aI)

5) Выполним коммит изменения по мере разработки
   
![](https://private-user-images.githubusercontent.com/180977102/394330983-bc4e9c3a-d76a-4e24-a473-53b044b14741.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM4NDM2NTIsIm5iZiI6MTczMzg0MzM1MiwicGF0aCI6Ii8xODA5NzcxMDIvMzk0MzMwOTgzLWJjNGU5YzNhLWQ3NmEtNGUyNC1hNDczLTUzYjA0NGIxNDc0MS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjEwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIxMFQxNTA5MTJaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0zNjlmZjJjZDgyZDQyYzYzOTVjM2EzOGFkMjU5ZTNkYjdjMGM1MGZiNTcwNDVmYzljODFkNWEzMjRkNDA2MDgxJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.zA7K_ALwkZMmb3Ucz4_aPPOpQLbffDf_0L7jSFZTfLw)

6) После завершения разработки функции завершаем фичу и объединяем ее с основной веткой
    
![](https://private-user-images.githubusercontent.com/180977102/394331782-31843e6e-efff-40ba-b484-b41c5a204e89.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM4NDM3ODEsIm5iZiI6MTczMzg0MzQ4MSwicGF0aCI6Ii8xODA5NzcxMDIvMzk0MzMxNzgyLTMxODQzZTZlLWVmZmYtNDBiYS1iNDg0LWI0MWM1YTIwNGU4OS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjEwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIxMFQxNTExMjFaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1kOGUzNDAyYzJiNzQ4NGYyMjk2ODYzZTc1NmE0OTdiZTFmMWZhNWY2YzIyYWI3ZjBiZjNhZjEzYTg5NTgwYmEyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.ZhDBC3QqiyfH1-at5zV9P728UHKt7VN6aCs44dCvLUw).

7) Переключимся на ветку "develop" и начинаем создание релиза
   
![](https://private-user-images.githubusercontent.com/180977102/394332860-73b4a07a-1234-4432-a84f-1e12d44a03c0.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM4NDM5MzYsIm5iZiI6MTczMzg0MzYzNiwicGF0aCI6Ii8xODA5NzcxMDIvMzk0MzMyODYwLTczYjRhMDdhLTEyMzQtNDQzMi1hODRmLTFlMTJkNDRhMDNjMC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjEwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIxMFQxNTEzNTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT03NjU0ZTA0NGE5MGI4YzNiZDE4N2FhZmE5NGY3YzljNGQyZjRiZDAzNGY3N2U2Y2EwMzQ2Nzk1YTdkMDNiNDZlJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.xeO10PIiNo2TzoVShUkYhFM7k3iiz6B8wj5mZQ8_AFY)

8) Обновим версию в файле version.txt
   
![](https://private-user-images.githubusercontent.com/180977102/394334129-e62895d6-c6ad-47f5-9952-739d48f88ac8.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM4NDQxMjYsIm5iZiI6MTczMzg0MzgyNiwicGF0aCI6Ii8xODA5NzcxMDIvMzk0MzM0MTI5LWU2Mjg5NWQ2LWM2YWQtNDdmNS05OTUyLTczOWQ0OGY4OGFjOC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjEwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIxMFQxNTE3MDZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0xMTBhNDY5NjIzZDQ5ZTM2YWExNTFjMjg3OTVjNGEzZDk4YjQxYWZmMTYyZWM2OTRlZjZiYWU2YWIxMTg1ZTEyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.eJr2XWA4D39tF0NunqIaGcst_Xb5pKeQ8uXGzStjSAw).

9) Завершим релиз и объединим его с ветками "develop" и "main"
    
![](https://private-user-images.githubusercontent.com/180977102/394335390-28d8f151-2247-4965-b6f0-14744b90cc8f.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM4NDQzMTIsIm5iZiI6MTczMzg0NDAxMiwicGF0aCI6Ii8xODA5NzcxMDIvMzk0MzM1MzkwLTI4ZDhmMTUxLTIyNDctNDk2NS1iNmYwLTE0NzQ0YjkwY2M4Zi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjEwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIxMFQxNTIwMTJaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT03M2QzMWJjNmE1NDc1NzE2M2Q1NmFkZWFhNWY2ZDk5Zjg2NmJhYTY1YjkwNzc4YjAwMzJhMzYzNjE4OGZlM2U5JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.whUpQricyIj0brZltEWexKxy0YLxl6hTnjN_ZMGOtgg)

10) Создадим hotfix
    
![](https://private-user-images.githubusercontent.com/180977102/394336529-9fc4c272-002b-4163-b211-22f93187930b.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM4NDQ0NzYsIm5iZiI6MTczMzg0NDE3NiwicGF0aCI6Ii8xODA5NzcxMDIvMzk0MzM2NTI5LTlmYzRjMjcyLTAwMmItNDE2My1iMjExLTIyZjkzMTg3OTMwYi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjEwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIxMFQxNTIyNTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1lNWUxNjdkMGY5NjI4N2FiZWZkMWFhOTQ4MTIwMGRlNTMxOTY3ZWE5YjIyMjA0ZGViODNmNWNiMDg5M2NmNjdiJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.Av4LGwfgAsi9TGz4TWJu6nqQ6BSHz0yTBouUSRRCEEA)

11) Исправим task_manager.py и закоммитим его
    
![](https://private-user-images.githubusercontent.com/180977102/394338016-fde1e71a-1722-4c63-9f85-3704276db97e.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM4NDQ3MDMsIm5iZiI6MTczMzg0NDQwMywicGF0aCI6Ii8xODA5NzcxMDIvMzk0MzM4MDE2LWZkZTFlNzFhLTE3MjItNGM2My05Zjg1LTM3MDQyNzZkYjk3ZS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjEwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIxMFQxNTI2NDNaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT05NTA5ZThkMDU0NTZkNDJjZTc3NTg1M2UzYTQ5NGM4NzU1YmM0NThlZDViMDc2ZGFiYmZkYzFlNzFjMWQ2NzUxJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.LJIQRRobjOZ5VMu54fiquO4DVIPNRGAgyy0n5ABU7HA)

12) Завершим hotfix и объединим его с ветками "develop" и "main"
    
![](https://private-user-images.githubusercontent.com/180977102/394339271-884d8950-f576-47e1-a52c-1316ff2b2492.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM4NDQ4NzQsIm5iZiI6MTczMzg0NDU3NCwicGF0aCI6Ii8xODA5NzcxMDIvMzk0MzM5MjcxLTg4NGQ4OTUwLWY1NzYtNDdlMS1hNTJjLTEzMTZmZjJiMjQ5Mi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjEwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIxMFQxNTI5MzRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0wOGNmNjhmZWZjMGVkNGEyZmQxMTc1NzlkMjllMDAyNWQ2NTgyMjAxYmRjMDJlNDMyMDliNDQ5ZjE1NTIzNzcyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.aoNg2OaCIXymfzWloySRRjoXc46M-NvWH4ZVgRG7RSE)

13) Завершим работу, отправив изменения на удаленный репозиторий
    
![](https://private-user-images.githubusercontent.com/180977102/394340031-762dcf70-6648-4260-af55-f829022b653b.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzM4NDQ5OTUsIm5iZiI6MTczMzg0NDY5NSwicGF0aCI6Ii8xODA5NzcxMDIvMzk0MzQwMDMxLTc2MmRjZjcwLTY2NDgtNDI2MC1hZjU1LWY4MjkwMjJiNjUzYi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjEwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIxMFQxNTMxMzVaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1iZTRjZGI3MzczNzgwYzcyNzRmNDhiMjhhOGY2ODQ2ODJiOGMyNWQxN2IwNzVhNWNkOGYzMDkxMzhhNTQyNTQ0JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.lstvO5mSiKZ7zjDSdpvqrayTP6PgDNgxg4rXTxtRGbE)