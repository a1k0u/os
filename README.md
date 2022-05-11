# Операционные системы

## System info

#### CPU
1. Какими способами можно узнать информацию о CPU? 
- `lshw` `lscpu` `cat /proc/cpuinfo`
- [Bash-скрипт](https://github.com/a1k0u/os/blob/main/cpu-info.sh), 
который выводит информацию о процессоре (_название, архитектуру,
число ядер, частоту работы и размер кэш-памяти_) в txt-файл.

#### RAM
1. Что такое RAM и Swap?


- `RAM` - оперативная память, также память с
произвольным доступом. Во время работы компьютера
каждая запущенная программа частично или полностью
загружается в RAM, сохраняя там команды, данные и 
промежуточные результаты для выполнения процессором.
Работа CPU с оперативной памятью <u>быстрее</u>, чем с 
жёстким диском или твердотельным накопителем.


- `Swap` - это процесс выделение виртуальной памяти,
другими словами, часть данных из RAM перемещается
на хранение в HDD или SSD. Использовать этот
механизм можно, например, когда требуется выделить
больше оперативной памяти, чем доступно.


2. Узнать всю информацию о RAM/Swap можно через
команду `free -h`, которая выводит удобочитаемую
сводку с автоматически выставленными единицами измерения.


3. Так как swap поддерживает влияние из вне, был
написан [bash-скрипт](https://github.com/a1k0u/os/blob/main/swap-change.sh), которому на вход подается один
обязательный аргумент с указанием количества выделенного
места. Для работоспособности прописываем 
`chmod u+x swap-change.sh`. Пример запуска:
`./swap-change.sh 1024M`. Скрипт также отлавливает
неверные входные данные (_1023Md, 3293, 
sdd1023.33M, 1g, g, ..._).
