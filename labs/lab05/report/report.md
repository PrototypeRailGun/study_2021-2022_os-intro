---
## Front matter
title: "Лабораторная работа №5"
subtitle: "Анализ файловой системы Linux."
author: "Старовойтов Егор Сергеевич"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Ознакомление с файловой системой Linux, её структурой, именами и содержанием
каталогов. Приобретение практических навыков по применению команд для работы
с файлами и каталогами,по управлению процессами (и работами),по проверке исполь-
зования диска и обслуживанию файловой системы.

# Задание

1. Выполнитевсепримеры,приведённыевпервойчастиописаниялабораторнойработы.
2. Выполните следующие действия, зафиксировав в отчёте по лабораторной работе используемые при этом команды и результаты их выполнения:
    1. Скопируйте файл/usr/include/sys/io.hв домашний каталоги назовите его
      equipment.Если файлаio.hнет,то используйтелюбойдругой файл в каталоге
      /usr/include/sys/вместо него.
    2. В домашнем каталоге создайте директорию ```~/ski.plases```.
    3. Переместите файлequipmentв каталог ```~/ski.plases```.
    4. Переименуйте файл  ```~/ski.plases/equipment``` в ```~/ski.plases/equiplist```.
    5. Создайте в домашнем каталоге файлabc1 и скопируйте его в каталог
        ```~/ski.plases```, назовите его ```equiplist2```.
    6. Создайте каталог с именемequipmentв каталоге ```~/ski.plases```.
    7. Переместите файлы ```~/ski.plases/equiplist``` и ```equiplist2``` в каталог
        ```~/ski.plases/equipment```.
    8. Создайте и переместите каталог ```~/newdirв каталог``` в ```~/ski.plases``` и назовите
        его ```plans```.

3. Определите опции команды **chmod**, необходимые для того, чтобы присвоить перечис-ленным ниже файлам выделенные права доступа, считая, что в начале таких прав нет:

    1. drwxr--r-- ... australia
    2. drwx--x--x ... play
    3. -r-xr--r-- ... my_os
    4. -rw-rw-r-- ... feathers

При необходимости создайте нужные файлы.


4. Проделайте приведённые ниже упражнения, записывая в отчёт по лабораторной работе используемые при этом команды:

    1. Просмотрите содержимое файла/etc/password.
    2. Скопируйте файл~/feathersв файл~/file.old.
    3. Переместите файл~/file.oldв каталог~/play.
    4. Скопируйте каталог~/playв каталог~/fun.
    5. Переместите каталог~/funв каталог~/playи назовите егоgames.
    6. Лишите владельца файла~/feathersправа на чтение.
    7.Что произойдёт,если вы попытаетесь просмотреть файл~/feathersкомандой
        cat?
    8. Что произойдёт,если вы попытаетесь скопировать файл~/feathers?
    9. Дайте владельцу файла~/feathersправо на чтение.
    10. Лишите владельца каталога~/playправа на выполнение.
    11. Перейдите в каталог~/play.Что произошло?
    12. Дайте владельцу каталога~/playправо на выполнение.

5. Прочитайте man по командам mount, fsck, mkfs, kill и кратко их охарактеризуйте,
приведя примеры.

# Теоретическое введение

## Формат команды
Командой в операционной системе называется записанный по
специальным правилам текст (возможно с аргументами), представляющий собой указание на выполнение какой-либо функций (или действий) в операционной системе.
Обычно первым словом идёт имя команды, остальной текст — аргументы или опции,
конкретизирующие действие.

Общий формат команд можно представить следующим образом:
```<имя_команды><разделитель><аргументы>```.

## Команда man
Команда ```man``` используется для просмотра (оперативная помощь) в диалоговом режиме руководства (manual) по основным командам операционной системы
типа Linux.
Формат команды: ```man <команда>```

Пример (вывод информации о команде man): ```man man```.

Для управления просмотром результата выполнения команды man можно использовать
следующие клавиши:
- Space — перемещение по документу на одну страницу вперёд;
- Enter — перемещение по документу на одну строку вперёд;
- q — выход из режима просмотра описания.

## Команда cd. 
Команда cd используется для перемещения по файловой системе операционной системы типа Linux.

Замечание 1. Файловая система ОС типа Linux — иерархическая система каталогов,
подкаталогов и файлов, которые обычно организованы и сгруппированы по функциональному признаку. 

Самый верхний каталог в иерархии называется корневым
и обозначается символом /. Корневой каталог содержит системные файлы и другие
каталоги.

Формат команды:
```cd [путь_к_каталогу]```

Для перехода в домашний каталог пользователя следует использовать команду ```cd``` без
параметров или ```cd ~```.

Например, команда
```cd /afs/dk.sci.pfu.edu.ru/home```
позволяет перейти в каталог /afs/dk.sci.pfu.edu.ru/home (если такой существует),
а для того, чтобы подняться выше на одну директорию, следует использовать:
```cd ..```.

Подробнее об опциях команды **cd** смотри в справке с помощью команды man:
```man cd```.

## Команда pwd
Для определения абсолютного пути к текущему каталогу используется
команда pwd (print working directory).

Пример (абсолютное имя текущего каталога пользователя dharma):
```bash
pwd
результат:
1 /afs/dk.sci.pfu.edu.ru/home/d/h/dharma
```

Сокращения имён файлов. В работе с командами, в качестве аргументов которых
выступает путь к какому-либо каталогу или файлу, можно использовать сокращённую
запись пути. Символы сокращения приведены в табл. 4.1.

Таблица 4.1
- ```~``` Домашний каталог
- ```.``` Текущий каталог
- ```..``` Родительский каталог

Например, в команде cd для перемещения по файловой системе сокращённую запись пути можно использовать следующим образом (команды чередуются с выводом
результата выполнения команды pwd):
```bash
pwd

/afs/dk.sci.pfu.edu.ru/home/d/h/dharma

cd ..
pwd

/afs/dk.sci.pfu.edu.ru/home/d/h

cd ../..
pwd

/afs/dk.sci.pfu.edu.ru/home

cd ~/work
pwd

/afs/dk.sci.pfu.edu.ru/home/d/h/dharma/work
```
## Команда ls 
Команда ls используется для просмотра содержимого каталога.

Формат команды:
```ls [-опции] [путь]```

Пример:
```bash
cd
cd ..
pwd

/afs/dk.sci.pfu.edu.ru/home/d/h

ls

dharma
```

Некоторые файлы в операционной системе скрыты от просмотра и обычно используются для настройки рабочей среды. Имена таких файлов начинаются с точки. Для
того, чтобы отобразить имена скрытых файлов, необходимо использовать команду **ls**
с опцией **a**:
```ls -a```.

Можно также получить информацию о типах файлов (каталог, исполняемый файл,
ссылка), для чего используется опция F. При использовании этой опции в поле имени
выводится символ, который определяет тип файла (см. табл. 4.2)
Таблица 4.2
- Каталог ```/```
- Исполняемый файл ```*```
- Ссылка ```@```

Чтобы вывести на экран подробную информацию о файлах и каталогах, необходимо
использовать опцию **l**. При этом о каждом файле и каталоге будет выведена следующая
информация:
- тип файла,
- право доступа,
- число ссылок,
- владелец,
- размер,
- дата последней ревизии,
- имя файла или каталога.

Пример:
```bash
cd /
ls
```

Результат:
```bash
bin boot dev etc home lib media mnt
opt proc root sbin sys tmp usr var

```
В этом же каталоге команда
```ls -alF```
даст примерно следующий результат:
```bash
drwxr-xr-x 21 root root 4096 Jan. 17 09:00 ./
drwxr-xr-x 21 root root 4096 Jan. 17 09:00 ../
drwxr-xr-x 2 root root 4096 Jan. 18 15:57 bin/
drwxr-xr-x 2 root root 4096 Apr. 14 2008 boot/
drwxr-xr-x 20 root root 14120 Feb. 17 10:48 dev/
drwxr-xr-x 170 root root 12288 Feb. 17 09:19 etc/
drwxr-xr-x 6 root root 4096 Aug. 5 2009 home/
lrwxrwxrwx 1 root root 5 Jan. 12 22:01 lib -> lib64/
drwxr-xr-x 8 root root 4096 Jan. 30 21:41 media/
drwxr-xr-x 5 root root 4096 Jan. 17 2010 mnt/
drwxr-xr-x 25 root root 4096 Jan. 16 09:55 opt/
dr-xr-xr-x 163 root root 0 Feb. 17 13:17 proc/
drwxr-xr-x 31 root root 4096 Feb. 15 23:57 root/
drwxr-xr-x 2 root root 12288 Jan. 18 15:57 sbin/
drwxr-xr-x 12 root root 0 Feb. 17 13:17 sys/
drwxrwxrwt 12 root root 500 Feb. 17 16:35 tmp/
drwxr-xr-x 22 root root 4096 Jan. 18 09:26 usr/
drwxr-xr-x 17 root root 4096 Jan. 14 17:38 var/
```

## Команда mkdir 
Команда mkdir используется для создания каталогов.

Формат команды:
```mkdir имя_каталога1 [имя_каталога2...]```

Пример создания каталога в текущем каталоге:
```bash
cd
pwd

/afs/dk.sci.pfu.edu.ru/home/d/h/dharma

ls

Desktop public tmp
GNUstep public_html work

mkdir abc
ls

abc GNUstep public_html work
Desktop public tmp
```

Замечание 2. Для того чтобы создать каталог в определённом месте файловой системы,
должны быть правильно установлены права доступа.

Можно создать также подкаталог в существующем подкаталоге:
```bash
mkdir parentdir
mkdir parentdir/dir
```

При задании нескольких аргументов создаётся несколько каталогов:
```bash
cd parentdir
mkdir dir1 dir2 dir3
```

Можно использовать группировку:
```mkdir parentdir/{dir1,dir2,dir3}```

Если же требуется создать подкаталог в каталоге, отличном от текущего, то путь к нему
требуется указать в явном виде:
```bash
mkdir ../dir1/dir2
или
mkdir ~/dir1/dir2
```

Интересны следующие опции:
- **--mode** (или **-m**) — установка атрибутов доступа;
- **--parents** (или **-p**)— создание каталога вместе с родительскими по отношению к нему
каталогами.

Атрибуты задаются в численной или символьной нотации:
```mkdir --mode=777 dir```
или
```mkdir -m a+rwx dir```

Опция **--parents** (краткая форма -p) позволяет создавать иерархическую цепочку
подкаталогов, создавая все промежуточные каталоги:
```mkdir -p ~/dir1/dir2/dir3```

## Команда rm
Команда rm используется для удаления файлов и/или каталогов.

Формат команды:
```rm [-опции] [файл]```

Если требуется, чтобы выдавался запрос подтверждения на удаление файла, то необходимо использовать опцию **i**.

Чтобы удалить каталог, содержащий файлы, нужно использовать опцию **r**. Без указания
этой опции команда не будет выполняться.

Пример:
```bash
cd
mkdir abs
rm abc

rm: abc is a directory

rm -r abc
```

Если каталог пуст, то можно воспользоваться командой **rmdir**. Если удаляемый
каталог содержит файлы, то команда не будет выполнена — нужно использовать 
```rm -r имя_каталога```.

## Команды для работы с файлами и каталогами

### touch
Для создания текстового файла можно использовать команду **touch**.
Формат команды:
```touch имя-файла```

### cat
Для просмотра файлов небольшого размера можно использовать команду **cat**.

Формат команды:
```cat имя-файла```

### less
Для просмотра файлов постранично удобнее использовать команду **less**.

Формат команды:
```less имя-файла```

Следующие клавиши используются для управления процессом просмотра:
- Space — переход к следующей странице,
- ENTER — сдвиг вперёд на одну строку,
- b — возврат на предыдущую страницу,
- h — обращение за подсказкой,
- q — выход из режима просмотра файла.

### head
Команда **head** выводит по умолчанию первые 10 строк файла.

Формат команды:
```head [-n] имя-файла```,
где n — количество выводимых строк.

### tail
Команда **tail** выводит умолчанию 10 последних строк файла.

Формат команды:
```tail [-n] имя-файла```,
где n — количество выводимых строк.


## Копирование файлов и каталогов

### cp
Команда **cp** используется для копирования файлов и каталогов.

Формат команды:
```cp [-опции] исходный_файл целевой_файл```

Примеры:

1. Копирование файла в текущем каталоге. Скопировать файл ~/abc1 в файл april
и в файл may:
```bash
cd
touch abc1
cp abc1 april
cp abc1 may
```

2. Копирование нескольких файлов в каталог. Скопировать файлы april и may в каталог
monthly:
```bash
mkdir monthly
cp april may monthly
```

3. Копирование файлов в произвольном каталоге. Скопировать файл monthly/may в файл
с именем june:
```bash
cp monthly/may monthly/june
ls monthly
```

Опция **i** в команде cp выведет на экран запрос подтверждения о перезаписи файла.
Для рекурсивного копирования каталогов, содержащих файлы, используется команда
**cp** с опцией **r**.

Примеры:

1. Копирование каталогов в текущем каталоге. Скопировать каталог monthly в каталог
monthly.00:
```bash
mkdir monthly.00
cp -r monthly monthly.00
```

2. Копирование каталогов в произвольном каталоге. Скопировать каталог monthly.00
в каталог /tmp
```bash
cp -r monthly.00 /tmp
```

## Перемещение и переименование файлов и каталогов
Команды **mv** и **mvdir** предназначены для перемещения и переименования файлов
и каталогов.

Формат команды mv:
```mv [-опции] старый_файл новый_файл```

Примеры:
1. Переименование файлов в текущем каталоге. Изменить название файла april на
july в домашнем каталоге:
```bash
cd
mv april july
```

2. Перемещение файлов в другой каталог. Переместить файл july в каталог monthly.00:
```bash
mv july monthly.00
ls monthly.00
```
Результат:
```bash
april july june may
```
Если необходим запрос подтверждения о перезаписи файла, то нужно использовать
опцию i.

3. Переименование каталогов в текущем каталоге. Переименовать каталог monthly.00
в monthly.01
```bash
mv monthly.00 monthly.01
```

4. Перемещение каталога в другой каталог. Переместить каталог monthly.01в каталог
reports:
```bash
mkdir reports
mv monthly.01 reports
```

5. Переименование каталога, не являющегося текущим. Переименовать каталог
reports/monthly.01 в reports/monthly:
```bash
mv reports/monthly.01 reports/monthly
```

## Права доступа
Каждый файл или каталог имеет права доступа.
В сведениях о файле или каталоге указываются:
- тип файла (символ (-) обозначает файл, а символ (d) — каталог);
- права для владельца файла (r — разрешено чтение, w — разрешена запись, x — разрешено выполнение, - — право доступа отсутствует);
- права для членов группы (r — разрешено чтение, w — разрешена запись, x — разрешено
выполнение, - — право доступа отсутствует);
- права для всех остальных (r — разрешено чтение, w — разрешена запись, x — разрешено
выполнение, - — право доступа отсутствует).

Примеры:

1. Для файла (крайнее левое поле имеет значение -) владелец файла имеет право на
чтение и запись (rw-), группа, в которую входит владелец файла, может читать файл
(r--), все остальные могут читать файл (r--): ```-rw-r--r--```
2. Только владелец файла имеет право на чтение, изменение и выполнение файла: ```-rwx------```.
3. Владелец каталога (крайнее левое поле имеет значение d) имеет право на просмотр,
изменение и доступа в каталог, члены группы могут входить и просматривать его, все
остальные — только входить в каталог: ```drwxr-x--x```.

## Изменение прав доступа
Права доступа к файлу или каталогу можно изменить, воспользовавшись командой
**chmod**. Сделать это может владелец файла (или каталога) или пользователь с правами
администратора.

Формат команды:
```chmod режим имя_файла```

Режим (в формате команды) имеет следующие компоненты структуры и способ записи:
- ```=``` установить право
- ```-``` лишить права
- ```+``` дать право
- ```r``` чтение
- ```w``` запись
- ```u``` (user) владелец файла
- ```g``` (group) группа, к которой принадлежит владелец файла
- ```o``` (others) все остальные

В работе с правами доступа можно использовать их цифровую запись (восьмеричное
значение) вместо символьной.
Формы записи прав доступа

| Двоичная | Восьмеричная | Символьная |
| :------: | :----------: | :--------: |
|111       |7             |rwx         |
|110       |6             |rw          |
|101       |5             |r-x         |
|100       |4             |r--         |
|011       |3             |-wx         |
|010       |2             |-w          |
|001       |1             |--x         |
|000       |0             |---         |

Примеры:

1. Требуется создать файл ~/may с правом выполнения для владельца:
```bash
cd
touch may
ls -l may
chmod u+x may
ls -l may
```

2. Требуется лишить владельца файла ~/may права на выполнение:
```bash
chmod u-x may
ls -l may
```

3. Требуется создать каталог monthly с запретом на чтение для членов группы и всех
остальных пользователей:
```bash
cd
mkdir monthly
chmod g-r, o-r monthly
```

4. Требуется создать файл ~/abc1 с правом записи для членов группы:
```bash
1 cd
2 touch abc1
3 chmod g+w abc1
```

## Анализ файловой системы
Файловая система в Linux состоит из фалов и каталогов. Каждому физическому носителю соответствует своя файловая система.

Существует несколько типов файловых систем. Перечислим наиболее часто встречающиеся типы:
- ext2fs (second extended filesystem);
- ext2fs (third extended file system);
- ext4 (fourth extended file system);
- ReiserFS;
- xfs;
- fat (file allocation table);
- ntfs (new technology file system).

### mount
Для просмотра используемых в операционной системе файловых систем можно воспользоваться командой **mount** без параметров. В результате её применения можно
получить примерно следующее:

```
mount

proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec)
udev on /dev type tmpfs (rw,nosuid)
devpts on /dev/pts type devpts (rw,nosuid,noexec)
/dev/sda1 on /mnt/a type ext3 (rw,noatime)
/dev/sdb2 on /mnt/docs type reiserfs (rw,noatime)
shm on /dev/shm type tmpfs (rw,noexec,nosuid,nodev)
usbfs on /proc/bus/usb type usbfs
(rw,noexec,nosuid,devmode=0664,devgid=85)
binfmt_misc on /proc/sys/fs/binfmt_misc type binfmt_misc
(rw,noexec,nosuid,nodev)
nfsd on /proc/fs/nfs type nfsd (rw,noexec,nosuid,nodev)
```

В данном случае указаны имена устройств, названия соответствующих им точек монтирования (путь), тип файловой системы и параметрами монтирования.

В контексте команды mount устройство — специальный файл устройства, с помощью
которого операционная система получает доступ к аппаратному устройству. 

Файлы устройств обычно располагаются в каталоге /dev, имеют сокращённые имена (например,
sdaN, sdbN или hdaN, hdbN, где N — порядковый номер устройства, sd — устройства SCSI,
hd — устройства MFM/IDE).

Точка монтирования — каталог (путь к каталогу), к которому присоединяются файлы
устройств.

Другой способ определения смонтированных в операционной системе файловых систем — просмотр файла/etc/fstab. Сделать это можно например с помощью команды

```
cat /etc/fstab

/dev/hda1 / ext2 defaults 1 1
/dev/hda5 /home ext2 defaults 1 2
/dev/hda6 swap swap defaults 0 0
/dev/hdc /mnt/cdrom auto umask=0,user,noauto,ro,exec,users 0 0

none /mnt/floppy supermount dev=/dev/fd0,fs=ext2:vfat,--,
sync,umask=0 0 0
none /proc proc defaults 0 0
none /dev/pts devpts mode=0622 0 0
```

В каждой строке этого файла указано:
- имя устройство;
- точка монтирования;
- тип файловой системы;
- опции монтирования;
- специальные флаги для утилиты dump;
- порядок проверки целостности файловой системы с помощью утилиты fsck.

### df
Для определения объёма свободного пространства на файловой системе можно воспользоваться командой df, которая выведет на экран список всех файловых систем
в соответствии с именами устройств, с указанием размера и точки монтирования. 

Например:

```bash
df

Filesystem 1024-blocks Used Available Capacity Mounted on
/dev/hda3 297635 169499 112764 60% /
```

С помощью команды fsck можно проверить (а в ряде случаев восстановить) целостность файловой системы:

Формат команды:
```fsck имя_устройства```

Пример:
```bash
fsck /dev/sda1
```


# Выполнение лабораторной работы

## Шаг 1 - Выполните все примеры, приведённые в первой части описания лабораторной работы.

### Пример 1
> Копирование файла в текущем каталоге. Скопировать файл ~/abc1 в файл april
и в файл may:

![Пример 1](image/p_1.png)

### Пример 2
> Копирование нескольких файлов в каталог. Скопировать файлы april и may в каталог
monthly:

![Пример 2](image/p_2.png)

### Пример 3
> Копирование файлов в произвольном каталоге.Скопировать файл monthly/may в файл
с именем june:

![Пример 3](image/p_3.png)

### Пример 4
> Копирование каталогов в текущем каталоге. Скопировать каталог monthly в каталог
monthly.00:

![Пример 4](image/p_4.png)

### Пример 5
> Копирование каталогов в произвольном каталоге. Скопировать каталог monthly.00
в каталог /tmp

![Пример 5](image/p_5.png)

### Пример 6
> ереименование файлов в текущем каталоге. Изменить название файла april на
july в домашнем каталоге:

![Пример 6](image/p_6.png)

### Пример 7
> Перемещение файлов в другой каталог. Переместить файл july в каталог monthly.00:

![Пример 7](image/p_7.png)

### Пример 8
> Переименование каталогов в текущем каталоге. Переименовать каталог monthly.00
в monthly.01

![Пример 8](image/p_8.png)

### Пример 9
> Перемещение каталога в другой каталог. Переместить каталог monthly.01 в каталог
reports:

![Пример 9](image/p_9.png)

### Пример 10
> Переименование каталога, не являющегося текущим. Переименовать каталог
reports/monthly.01 в reports/monthly:

![Пример 10](image/p_10.png)

### Пример 11
> Требуется создать файл ~/may с правом выполнения для владельца:

![Пример 11](image/p_11.png)

### Пример 12
> Требуется лишить владельца файла ~/may права на выполнение:

![Пример 12](image/p_12.png)

### Пример 13
> Требуется создать каталог monthly с запретом на чтение для членов группы и всех
остальных пользователей:

![Пример 13](image/p_13.png)

### Пример 14
> Требуется создать файл ~/abc1 с правом записи для членов группы:

![Пример 14](image/p_14.png)

### Пример 15
> Для просмотра используемых в операционной системе файловых систем можно воспользоваться командой mount без параметров. В результате её применения можно
получить примерно следующее

![Пример 15](image/p_15.png)

### Пример 16
> Другой способ определения смонтированных в операционной системе файловых систем — просмотр файла/etc/fstab. Сделать это можно например с помощью команды
cat:

![Пример 16](image/p_16.png)

### Пример 17
> Для определения объёма свободного пространства на файловой системе можно воспользоваться командой df, которая выведет на экран список всех файловых систем
в соответствии с именами устройств, с указанием размера и точки монтирования. Например:

![Пример 17](image/p_17.png)

### Пример 18
> С помощью команды fsck можно проверить (а в ряде случаев восстановить) целостность файловой системы:

![Пример 18](image/p_45.png)


## Шаг 2 - Выполните следующие действия, зафиксировав в отчёте по лабораторной работе используемые при этом команды и результаты их выполнения:

### Шаг 2.1
> Скопируйте файл /usr/include/sys/io.h в домашний каталог и назовите его
equipment. Если файла io.h нет, то используйте любой другой файл в каталоге
/usr/include/sys/ вместо него.

Для копирования файла я воспользовался командой cp, после чего убедился в упешности операции с помощью команд ls и cat.

![Задание 2.1](image/p_18.png)

### Шаг 2.2
> В домашнем каталоге создайте директорию ~/ski.plases.

Я создал нужную директорию с помощью команды mkdir и убедился в результате с помощью команды ls.

![Задание 2.2](image/p_19.png)

### Шаг 2.3
> Переместите файл equipment в каталог ~/ski.plases.

Для перемещения файла я воспользовался командой mv, а затем проверил результат с помощью ls.

![Задание 2.3](image/p_20.png)

### Шаг 2.4
> Переименуйте файл ~/ski.plases/equipment в ~/ski.plases/equiplist.

Для переименования файла я воспользовался командой mv, а затем проверил результат с помощью ls.

![Задание 2.4](image/p_21.png)

### Шаг 2.5
> Создайте в домашнем каталоге файл abc1 и скопируйте его в каталог
~/ski.plases, назовите его equiplist2.

С помощью команды touch я создал файл abc1, затем с помощью команды cp скопировал его в каталог ~/ski.plases под новым именем equiplist2. С помощью команды ls проверил результат.

![Задание 2.5](image/p_22.png)

### Шаг 2.6
> Создайте каталог с именем equipment в каталоге ~/ski.plases.

С помощью комнады cd я перешел в ~/ski.plases, где с помощью makedir создал каталог equipment.

![Задание 2.6](image/p_23.png)

### Шаг 2.7
> Переместите файлы ~/ski.plases/equiplist и equiplist2 в каталог
~/ski.plases/equipment

С данным заданием справляется двухкратный вызов команды mv, а спомощью tree легко увидеть результат.

![Задание 2.7](image/p_23.png)

### Шаг 2.8
> 8. Создайте и переместите каталог ~/newdir в каталог ~/ski.plases и назовите
его plans.

С помощью команды mkdir я создал каталог newdir, после чего переместил его в ~/ski.plases с помощью команды mv. С помощью ls увидел результат.

![Задание 2.8](image/p_24.png)

## Шаг 3 - Определите опции команды chmod, необходимые для того, чтобы присвоить перечисленным ниже файлам выделенные права доступа, считая, что в начале таких прав нет.

На данном этапе я задавал права доступа к файлам в численном виде.

### Шаг 3.1 - drwxr--r-- ... australia
![Задание 3.1](image/p_25.png)

### Шаг 3.2 - drwx--x--x ... play
![Задание 3.2](image/p_26.png)

### Шаг 3.3 - -r-xr--r-- ... my_os
![Задание 3.3](image/p_27.png)

### Шаг 3.4 - -rw-rw-r-- ... feathers
![Задание 3.4](image/p_28.png)

## Шаг 4 - Проделайте приведённые ниже упражнения, записывая в отчёт по лабораторной работе используемые при этом команды:

## Шаг 4.1
> Просмотрите содержимое файла /etc/password.

Я ввел ```cat /etc/password```, но искомого файла не оказалось.

![Задание 4.1](image/p_29.png)

## Шаг 4.2
> Скопируйте файл ~/feathers в файл ~/file.old.

Я использовал команду cp.

![Задание 4.2](image/p_30.png)

## Шаг 4.3
> Скопируйте файл ~/file.old в каталог ~/play.

Я использовал команду cp.

![Задание 4.3](image/p_31.png)

## Шаг 4.4
> Скопируйте каталог ~/play в каталог ~/fun.

Я использовал команду cp с опцией -r.

![Задание 4.4](image/p_32.png)

## Шаг 4.5
> Переместите каталог ~/fun в каталог ~/play и назовите его games.

Я использовал команду mv, результат проверил с помощью команды tree.

![Задание 4.5](image/p_33.png)

## Шаг 4.6
> Лишите владельца файла ~/feathers права на чтение.

Я использовал команду chmod с аргументом u-r.

![Задание 4.6](image/p_34.png)

## Шаг 4.7
> Что произойдёт, если вы попытаетесь просмотреть файл ~/feathers командой cat?

Я получил ошибку "cat: feathers: Permission denied", что означает "отказано в доступе".

![Задание 4.7](image/p_35.png)

## Шаг 4.8
> Что произойдёт, если вы попытаетесь скопировать файл ~/feathers?

Я получил ошибку "cp: cannot open 'feathers' for reading: Permission denied", - программа cp не смогла прочитать файл, так как у пользователя отсутсвует на это право.

![Задание 4.8](image/p_36.png)

## Шаг 4.9
> Дайте владельцу файла ~/feathers право на чтение.

Я использовал команду chmod с аргументом u+r. В изменении прав убедился с помощью ls -l.

![Задание 4.9](image/p_37.png)

## Шаг 4.10 
> Лишите владельца каталога ~/play права на выполнение.

Я использовал команду chmod с аргументом u-x.

![Задание 4.10](image/p_38.png)

## Шаг 4.11
> Перейдите в каталог ~/play. Что произошло?

При попытке перейти в каталог мне было отказано в доступе.

![Задание 4.11](image/p_39.png)

## Шаг 4.12
> Дайте владельцу каталога ~/play право на выполнение.

Я использовал команду chmod с аргументом u+x.

![Задание 4.12](image/p_40.png)

## Шаг 5 - Прочитайте man по командам mount, fsck, mkfs, kill и кратко их охарактеризуйте,приведя примеры.

### mount
Команда **mount** позволяет объединить несколько файловых систем в единое дерево каталогов. Для подмонтирования нового устройства нужно написать ```mount файл_устройства пака_назначения```.

![man mount](image/p_41.png)

### fsck
**fsck** - это утилита для проверки и восстановления файловых систем Linux. Обычно команда fsck автоматически запускается по возможности в параллельном режиме при загрузке ОС. По этой причине обычно нет необходимости запускать ее через командную строку.

![man fsck](image/p_42.png)

### mkfs
Команда **mkfs** используется для создания файловой системы Linux на некотором устройстве, обычно в разделе жесткого диска. В качестве аргумента может выступать название устройства (например /dev/sda1) или точка монтирования (например /, /home).

![man mkfs](image/p_43.png)

### kill
Команда **kill** позволяет отправить сигнал процессу, принимая на вход его PID идентификатор. Например, можно принудительно завершить процесс с PID=2000 набрав ```kill -KILL 2000``` 
![man kill](image/p_44.png)

# Вывод

Я познакомился с файловой системой Linux, ее структурой, именами и содержанием основных каталогов. Также приобрел практические навыки по применению команд для работы с файлами и каталогами, по управлению процессами и по проверке диска и обслуживанию файловых систем.

# Контрольные вопросы

## 1. Дайте характеристику каждой файловой системе, существующей на жёстком диске компьютера, на котором вы выполняли лабораторную работу.

**Tmpfs** - временное файловое хранилище во многих Unix-подобных ОС и в частности Linux. Предназначена для монтирования файловой системы, но размещается в ОЗУ вместо физического диска. 

## 2. Приведите общую структуру файловой системы и дайте характеристику каждой директории первого уровня этой структуры.

![Директории первого уровня](image/p_46.png)

- /bin - каталог, содержащий исполняемые файлы. Монтируется на корневую файловую систему, должен быть доступен даже если никакие другие файловые системы не смонтированы.

- /dev - содержит файлы физических устройств, которые могут входить в состав аппартного обеспечения компьютера.

- /home - каталог, содержащий в себе домашние каталоги пользователей операционный системы, в которых хранятся их данные, настройки, пароли и т.д.

- /lib64 - каталог, присутсвующий на 64-битных системах, содержащий набор библиотек и компонентов компилятора языка C для 64-битных систем.

- /media - точка для автоматического монтирования различных устройств: USB-накопители, CD-ROM и т.д.

- /opt - содержит подкаталоги для дополнительных пакетов программного обеспечения.

- /root - Домашний каталог пользователя root. Он мог бы лежать в папке /home, но находится на первом уровне для большей надежности системы.

- /sbin - содержит иполняемые файлы, предназначеные для запуска пользователем при администрировании системы.

- /sys - точка монтирования виртуальной файловой системы sysfs с информацией об устройствах, драйверах, ядре ОС, гипервизоре и т.д.

- /usr - бинарные файлы, используемые только пользователями, например игры.

- /boot - файлы, нужные для запуска ОС (образы ядер Linux и файлы менеджеров загрузки).

- /etc - содержит основные конфигурационные файлы операционной системы и различных программ.

- /lib - директория, предназначенная для хранения системных библиотек и компонентов компилятора языка C, необходимых для работы программ из каталогов /bin и /sbin.

- /lost+found - При сбое в работе файловой системы и дальнейшей проверки файлов все найденные поврежденные файлы помещаются в каталог /lost+found, чтобы их можно было попытаться восстановить.

- /mnt - Точка ручного монтирования (используется для временного монтирования с применением команды mount).

- /proc - содержит файлы ядра и процессора. В эту директорию примонтирована виртуальная файловая система procfs, в которой содержатся специальные файлы, в которых находится информация о системе и выполняющихся процессах.

- /run - каталог для хранения вспомогательных временных файлов приложений.

- /srv - содержит данные сервисных служб, предоставляемых системой.

- /tmp - содержит временные файлы, которые удаляются при выключении или перезагрузке системы.

- /var - содержит журналы ОС, системные логи и cache-файлы.

## 3. Какая операция должна быть выполнена, чтобы содержимое некоторой файловой системы было доступно операционной системе?

Ответ: mkfs.

## 4. Назовите основные причины нарушения целостности файловой системы. Как устранить повреждения файловой системы?

Основной причиной нарушения целостности файловой системы является останова ОС в момент обновления метаданных файлов. Это может привести к дублированию или наоборот потере файлов из-за нарушения инварианта счетчика ссылок или другой важной информации.

Для диагности и исправления ошибок файловой системы используется команда fsck.

## 5. Как создаётся файловая система?

Создать новую файловую систему можно с помощью команды mkfs.

## 6. Дайте характеристику командам для просмотра текстовых файлов.

- cat - подходит для просмотра файлов небольшого размера, выводит всё их содержимое в консоль.
- less - подходит для постраничного просмотра файла, можно переключаться между страницами.
- head - выводит несколько первых строк файла, по умолчанию - 10, но можно указать и другое число.
- tail - выводит несколько последних строк файла, по умолчанию - 10, но можно указать и другое число.

## 7. Приведите основные возможности команды cp в Linux.

Команда cp применяется для копирования файлов и каталогов, имеется возможность копирования несколько файлов в один каталог одной командой. Можно копировать файлы в произвольном каталоге, указывая полный или при возможности относительный путь. Для копирования каталогов вместе с их содержимым указывается опция -r.
Подробнее об этой команде написано в теоретическом введении.

## 8. Приведите основные возможности команды mv в Linux.

Команда mv применется для перемещения и смены имени файлов и каталогов.
Подробнее об этой команде написано в теоретическом введении.

## 9. Что такое права доступа? Как они могут быть изменены?

Права доступа - набор значений, устанавливающий возможности тех или иных пользователей читать,изменять или исполнять конкретный файл или директорию. Права доступа к файлу можно изменить с помощью команды chmod. Подробнее об этой команде написано в теоретическом введении.