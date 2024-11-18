## Отчет к лабораторной работе №4

1)  Создадим директорию лабораторной и перейдем к ней
```linux
mkdir lab4 && cd lab4
```

2) Создадим Dockerfile и откроем редактор
```linux
touch Dockerfile && nano Dockerfile
```
3) Пропишем в нашем файле следующее:
```linux
FROM ubuntu:latest
RUN apt-get update && apt-get install -y libaa-bin fortune && apt-get install iputils-ping -y
```