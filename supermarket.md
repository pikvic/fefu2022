# Очереди в супермаркете

Напишите программу, которая будет моделировать работу магазина, а именно очереди на кассе.

## Описание предметной области и модели
Моделирование будет проходить каждую секунду с использованием случайных чисел. 
Необходимо реализовать работу со связными списками специального типа: очередями. Каждый элемент очереди - посетитель магазина.
Посетитель имеет случайное имя - случайная маленькая английская буква, случайное время обслуживания - от `1` до `MAX_CUSTOMER_TIME` секунд, случайную сумму попкупки - от `1` до `MAX_CUSTOMER_CHECK`
Каждая касса имеет свою очередь и статус: работает или нет (+ или -). Максимальный размер очереди для касс - `MAX_CASHIER_QUEUE`.

За каждую секунду на кассы может подойти от `0` до `MAX_NEXT_CUSTOMERS` посетителей. Они встают в рабочие кассы слева-направо не более `MAX_CASHIER_QUEUE` на кассу.
Если на следующей секунде (итерации симуляции) кассы не смогут вместить посетителей, то открываются новая касса (максимум `MAX_CASHIERS` касс).
Когда все `MAX_CASHIERS` касс заполнены и не смогут вместить всех новых посетителей, то симуляция заканчивается с сообщением Game Over и сохранением последнего состояния на экране.
Все вычисления происходят в момент времени `t`, а в `t + 1` применяются, после чего в `t + 1` происходят новые вычисления.
Например, при `t = 0` у нас работает 1 касса, мы знаем сколько и какие придут посетители и общее количество человек в очередях. Печатаем информацию.
При `t = 1` пришедшие посетители становятся в очередь на кассу, генерируются посетители для следующего момента времени. Печатаем информацию.
При `t = 2` сначала у первого в очереди посетителя на кассе отнимается 1 секунда от времени его обслуживания. Если 0, то он покидает очередь и она уменьшается на 1. Производится проверка на максимальную очередь и, если надо, открывается ещё одна касса. После этого новые посетители встают в очереди в кассы. Генерируются следующие посетители. Печатаем информацию.

И так далее.

Интерфейс программы показан ниже. Он перерисовывается каждую секунду. Для этого используется `system("clear")` из `stdlib.h` и `sleep(1)` из `unistd.h`. Под Windows очистка экрана посредством команды `system("cls")`. 
Если посетителей слишком мало, то лишние кассы закрываются (приоритет - обслужившим больше всех посетителей).

## Файл с настройками

Настройки в файле `settings.txt` вида параметр=значение. Что должно быть в файле (в любом порядке):
- MAX_CUSTOMER_TIME - максимальное время обслуживания посетителя 
- MAX_CASHIER_QUEUE - максимальный размер очереди на кассе
- MAX_CASHIERS - максимальное количество одновременно работающих касс
- MAX_NEXT_CUSTOMERS - максимальное количество следующих покупателей
- MAX_CUSTOMER_CHECK - максимальная сумма покупки покупателя 

## Должны быть реализовны следующие структуры:

1. Структура посетитель магазина:
- имя - одна строчна буква английского алфавита
- время обслуживания - целое число от `1` до `MAX_CUSTOMER_TIME`
- сумма покупки - целое число от  от `1` до `MAX_CUSTOMER_CHECK`

2. Структура элемент очереди:
- посетитель магазина - тип данных Структура посетитель магазина
- указатель на следующий элемент очереди

3. Структура очередь:
- указатель на первый элемент очереди
- указатель на последний элемент очереди
- длина очереди - целое число

4. Структура касса:
- поле с флагом, что касса включена - целое число, 0 или 1 (или символ +/-)
- количество обслуженных посетителей - целое число
- сумма покупок на кассе - целое число
- текущая очередь на кассе - тип данных Структура очередь

## Должны быть реализовны следующие функции:

1. Любые функции, которые вам понадобятся для написания программы. Сами решите, какие.

## Интерфейс

Ниже приведён пример интерфейса. Во второй строке - номера касс, в третьей - количество обслужанных посетителей с начала симуляции, в четвёртой - статус кассы (работает / не работает).
Далее идут `MAX_CASHIER_QUEUE` строк с посетителями в очередях на каждую кассу (или пустыми местами).
Ниже идёт статистика: текущее время симуляции, список следующих посетителей, общее количество народу на кассах, количество рабочих касс, количество обслужанных посетителей с начала симуляции.

**Пример вывода:**

```
Супермаркет "Реми". Система моделирования очередей.
   1   2   3   4   5   6
  12   4   0   0   0   0  
   +   +   -   -   -   -
  a1  s2  ||  ||  ||  ||
  s3  a1  ||  ||  ||  ||
  d1  q1  ||  ||  ||  ||
  f2  ||  ||  ||  ||  ||
  l3  ||  ||  ||  ||  ||
Время: 8
Следующие посетители: f2 w3 k1
Человек в очередях: 8
Касс работает: 2 из 6
Всего обслужено: 16
Сумма покупок: 20332
Допустимая очередь на кассу: 5
```

## Дополнительные требования

1. Добавьте в код комментарии с пояснением основных шагов программы или кратким описанием функций.
2. Не забывайте про [генератор случайных чисел](https://stackoverflow.com/questions/822323/how-to-generate-a-random-int-in-c).
3. Пример работы: [ссылка](https://youtu.be/EPEPh-bhBqM)

При написании программы следует руководствоваться [Методичкой по Си](https://docs.google.com/document/d/1xBCa22mlYdWKlb4px1vPLPJS1Tqt2mlgsHtbOZa8Xn8/edit) и [Правилами оформления кода на Си](https://docs.google.com/document/d/19whC799AqENdLdcx8VzePjKAjzvyxwbcddJ6Q9FXpA4/edit).