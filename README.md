# Домашняя работа по RabbitMQ

## Студент

Михаил Лукьянов

---

# Задание 1

## Выполнение

На виртуальной машине Ubuntu был установлен RabbitMQ и необходимые зависимости.

Проверена работа сервиса:


sudo systemctl status rabbitmq-server
```

Проверен доступ к веб-интерфейсу RabbitMQ Management.

## Результат

RabbitMQ успешно установлен и запущен.

<img width="3837" height="2045" alt="1" src="https://github.com/user-attachments/assets/da4157c5-80be-474e-9116-c1d08dce707b" />


- запуск сервиса RabbitMQ;
- проверка статуса сервиса;
- веб-интерфейс RabbitMQ Management.

---

# Задание 2

## Выполнение

Были созданы:

- exchange;
- queue;
- binding между exchange и queue.

Проверена доставка сообщений через RabbitMQ.

## Результат

Сообщения успешно доставляются через созданные очереди и exchange.

### Скриншоты
<img width="3837" height="1337" alt="2" src="https://github.com/user-attachments/assets/62e58fff-8d52-4f94-98b7-3e23be2547e5" />

<img width="1630" height="1062" alt="2-2" src="https://github.com/user-attachments/assets/2fa30977-cc5e-4509-b998-d2917d6434bf" />

- созданные exchange;
- созданные очереди;
- результаты отправки и получения сообщений.

---
# Задание 3

## Цель

Развернуть кластер RabbitMQ из двух узлов и настроить отказоустойчивость.

## Выполнение

Для выполнения задания были созданы две виртуальные машины:

* rmq01
* rmq02

На обеих машинах установлен RabbitMQ.

После настройки сетевого взаимодействия и синхронизации Erlang Cookie узел `rmq02` был успешно подключён к кластеру `rmq01`.

Проверка выполнена командой:

```bash
sudo rabbitmqctl cluster_status
```

Результат показал наличие двух узлов в кластере:

```text
rabbit@rmq01
rabbit@rmq02
```

Для обеспечения высокой доступности была создана политика зеркалирования:

```bash
sudo rabbitmqctl set_policy ha-all ".*" '{"ha-mode":"all"}'
```

Проверка политики выполнена командой:

```bash
sudo rabbitmqctl list_policies
```

Политика успешно применена.

## Скриншоты

<img width="2962" height="1882" alt="3" src="https://github.com/user-attachments/assets/60fc1ac2-78d4-40ba-a386-2c5a924c6942" />
<img width="3837" height="1572" alt="3-3" src="https://github.com/user-attachments/assets/4397ba43-6763-45ff-97c6-e7a9d3945f84" />
<img width="2240" height="337" alt="3-3-3" src="https://github.com/user-attachments/assets/ec97036d-5564-4d05-bf49-24bc00285942" />
<img width="3145" height="2035" alt="333-333 1 машина" src="https://github.com/user-attachments/assets/7f35af98-0bec-4015-bc70-d3d2d8338864" />
<img width="3837" height="2040" alt="3-3-3-3" src="https://github.com/user-attachments/assets/76439769-f815-4c66-adc3-42c0962780d2" />
<img width="3835" height="2037" alt="Снимок экрана 2026-06-13 172221" src="https://github.com/user-attachments/assets/f5e24ccf-bcbe-4ceb-aac1-9c042717254c" />


## Результат

Кластер RabbitMQ из двух узлов успешно развернут и работает корректно. Политика высокой доступности настроена и применена.

