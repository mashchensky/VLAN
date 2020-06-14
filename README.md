# Домашнее задание "Сетевые пакеты"

## Описание тестового стенда

в Office1 в тестовой подсети добавлены сервера с доп интерфейсами и адресами
в internal сети testLAN
- testClient1 - 10.10.10.254
- testClient2 - 10.10.10.254
- testServer1- 10.10.10.1
- testServer2- 10.10.10.1

Вланами разведены
testClient1 <-> testServer1
testClient2 <-> testServer2

Между centralRouter и inetRouter "проброшены" 2 линка (общая inernal сеть) и объеденины в бонд.
