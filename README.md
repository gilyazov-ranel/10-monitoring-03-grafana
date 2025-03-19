### Задание 1

1. Используя директорию [help](./help) внутри этого домашнего задания, запустите связку prometheus-grafana.
1. Зайдите в веб-интерфейс grafana, используя авторизационные данные, указанные в манифесте docker-compose.
1. Подключите поднятый вами prometheus, как источник данных.
1. Решение домашнего задания — скриншот веб-интерфейса grafana со списком подключенных Datasource.
#### Ответ 
![image](https://github.com/user-attachments/assets/f0e0a1b8-4638-4397-b485-dda81a8c0457)

## Задание 2

Изучите самостоятельно ресурсы:

1. [PromQL tutorial for beginners and humans](https://valyala.medium.com/promql-tutorial-for-beginners-9ab455142085).
1. [Understanding Machine CPU usage](https://www.robustperception.io/understanding-machine-cpu-usage).
1. [Introduction to PromQL, the Prometheus query language](https://grafana.com/blog/2020/02/04/introduction-to-promql-the-prometheus-query-language/).

Создайте Dashboard и в ней создайте Panels:

- утилизация CPU для nodeexporter (в процентах, 100-idle);
- CPULA 1/5/15;
- количество свободной оперативной памяти;
- количество места на файловой системе. 

Для решения этого задания приведите promql-запросы для выдачи этих метрик, а также скриншот получившейся Dashboard.
#### Ответ
![image](https://github.com/user-attachments/assets/91316c3e-29bc-441b-abad-b9f0b6c84d4d)
утилизация CPU для nodeexporter (в процентах, 100-idle)
```
100 - avg(irate(node_cpu_seconds_total{mode="idle"}[5m])) by (instance) * 100
 ```
CPULA 1/5/15
```
node_load1
node_load5
node_load15
 ```
 Количество свободной оперативной памяти
```
node_memory_MemAvailable_bytes{instance="nodeexporter:9100",job="nodeexporter"}
 ```
Количество места на файловой системе
```
    (node_filesystem_size_bytes{mountpoint="/"} - node_filesystem_avail_bytes{mountpoint="/"}) / node_filesystem_size_bytes{mountpoint="/"} * 100  
  ```
## Задание 3

1. Создайте для каждой Dashboard подходящее правило alert — можно обратиться к первой лекции в блоке «Мониторинг».
1. В качестве решения задания приведите скриншот вашей итоговой Dashboard.
#### Ответ
![image](https://github.com/user-attachments/assets/7c7b5d4b-c1b4-4350-abd2-a049fa514852)
![image](https://github.com/user-attachments/assets/a12cd1d0-ce12-4db3-bece-2a1ac9a97fcf)

## Задание 4

1. Сохраните ваш Dashboard.Для этого перейдите в настройки Dashboard, выберите в боковом меню «JSON MODEL». Далее скопируйте отображаемое json-содержимое в отдельный файл и сохраните его.
1. В качестве решения задания приведите листинг этого файла.
#### Ответ
[dashboard](https://github.com/gilyazov-ranel/10-monitoring-03-grafana/blob/main/dashboardTest.json)
