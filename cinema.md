# Каталог онлайн-кинотеатра

Представим, что мы живём в мире, где есть онлайн-кинотеатры, но нет графического интерфейса :)

Один известный онлайн-кинотеатр заказал вам создание консольного каталога для своей коллекции фильмов. Необходимо сделать логику работы каталога и его отображение (пользовательский интерфейс).

[Как нужно отображать](https://www.jqueryscript.net/demo/Smooth-Card-Carousel-jQuery-CSS3/)

При этом отображение каталога происходит в виде 3 карточек с названием фильма и рейтингом. Карточка в центре должна визуально выделяться как активная. Список фильмов в каталоге замкнут, то есть при достижении последнего фильма при прокрутке врпаво происходит переход на первый фильм и т.д.

Вся информация о фильмах хранится в текстовом файле `films.txt`, каждая запись о фильме имеет следующий формат:
- Строка с названием фильма
- Целое число - год выпуска фильма
- Строка со страной (странами через запятую) происхождения фильма
- Строка с жанром (жарнами через запятую) фильма
- Число с плавающей точкой - рейтинг фильма

Необходимо реализовать следующий функционал работы:

### 1. Каталог фильмов
- Структура фильм, в которой будет хранится информация о фильме, поля как в файле
- Чтение информации о фильмах и создание **двусвязного списка фильмов** (хранит указатель на следующий и предыдущий), который соединён в кольцо (указатель next у последнего элемента хранит адрес первого элемента)
- Вывод списка фильмов в виде карточек с навигацией (влево-вправо, просмотр подробной информации о фильме)
- Просмотр подробной информации о фильме из каталога
- Добавление фильма в список избранного как в режиме каталога, так и в режиме просмотра подробной информации о фильме

### 2. Список избранного
- Просмотр списка избранного в виде карточек с навигацией (как в каталоге)
- Просмотр подробной информации о фильме из списка избранного
- Удаление фильма из списка избранного в режиме просмотра списка избранного
- Удаление фильма из списка избранного в режиме просмотра подробной информации о фильме
- Сохранение списка избранного при выходе из программы в файл и загрузка его при запуске (имя файла = `favorites_имяпользователя.txt`, см. пункт 3)

### 3. Система логинов пользователей
- Структура пользователь для хранения информации о пользователе: `логин` (строка от 3 до 20 символов латинского алфавита), `пароль` (строка от 6 до 20 символов), `номер карты` (строка из 16 цифр), `размер списка избранного` (целое число), `админ ли пользователь` (целое число 1 или 0)
- При создании и изменении пользователя должны быть проверки на логин (от 3 до 20 символов латинского алфавита и цифры), пароль (от 6 до 20 символов латинского алфавита и цифры, обязательно буква в верхнем, нижнем регистре и цифра хоть одна должны быть), номер карты (16 цифр)
- При запуске программы приветствовать пользователя и запрашивать логин или регистрацию нового пользователя
- При регистрации нового сохранять его данные в файл `users.txt`, оттуда же проверять логин-пароль при входе
- При работе с программой отображать имя текущего пользователя
- Реализовать личный кабинет, где пользователь мог бы изменить свои данные
- Список избранного пользователя хранить в текстовом файле в таком же формате, как файл каталога фильмов, а имя файла - `favorites_имяпользователя.txt`

### 4. Режим администратора
- Пользователи, у которых поле `isAdmin == 1`, являются администраторами и имеют возможность зайти в режим администратора. Остальные режимы такие же.
- Администраторы создаются вручную в файле `users.txt`
- Режим администратора позволяет добавлять в каталог новый фильм, а также удалять выбранный фильм как в режиме каталога, так и в режиме просмотра фильма
- Удаление фильма из каталога должно вызывать удаление фильма из списков избранного всех пользователей!
- При добавлении фильма также проверять вводимые значения на корректность, при ошибке указывать на неё

### 5. Меню по работе с программой
- Навигация пошаговая с очисткой экрана (информация на экране всегда перерисовывается, а не добавляется в конец)
- "Красивый" интерфейс :) См. допополнительные требования


## Справочные материалы для написания проекта

1. [Таблица символов](https://theasciicode.com.ar/)
2. [Форматирование при печати](http://youngcoder.ru/lessons/3/formatnyi_vyvod_printf.php)
3. [Работа с файлами](https://younglinux.info/c/fopen)
4. [Работа со строками](http://youngcoder.ru/lessons/9/simvolnie_stroki_vvod_i_vyvod.php)
5. [Очистка экрана](https://www.cyberforum.ru/cpp-beginners/thread26478.html)

## Дополнительные требования

При написании программы можете создавать любые структуры и функции, которые вам помогут написать более структурированный, модульный, читаемый код. Потренируйтесь в проектировании программ ;)

Рекомендуется разбить код на модули (файлы .h и .c), которые будут подключаться к основному файлу или друг к другу.

Необходимо написать интерфейс пользователя для каталога фильмов. Меню должно быть понятным, удобным, с различными визуальными элементами (например из таблицы символов └ или ┴ и т.д.)

**Заведите под разные сущности структуры и используйте указатели на функции в них, чтобы объединить по смыслу атрибуты и действия, присущие сущностям**

**Совместную работу ведите в системе контроля версий Git. Можно создать репозиторий на [github.com](github.com) и подключить его к replit. Используйте ветки для разного функционала и pull request для объедитения с веткой main.**

При написании программы следует руководствоваться [Методичкой по Си](https://docs.google.com/document/d/1xBCa22mlYdWKlb4px1vPLPJS1Tqt2mlgsHtbOZa8Xn8/edit) и [Правилами оформления кода на Си](https://docs.google.com/document/d/19whC799AqENdLdcx8VzePjKAjzvyxwbcddJ6Q9FXpA4/edit).

По всем вопросам пишите в группу или личку.