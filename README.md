# Операционные системы

## System info

#### CPU
1. Какими способами можно узнать информацию о CPU? 

- `lshw` `lscpu` `cat /proc/cpuinfo` `sudo dmidecode --type processor`
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


4. С помощью `sudo lshw -class memory` и 
`sudo dmidecode -t memory` можно узнать всю информацию
о RAM, в том числе: название (_product_, _Part Number_), 
производителя (_vendor_, _Manufacturer_), серийный номер
(_serial_, _Serial_), формат (_type_), объем (_size_, _Size_)
и частоту работы (_clock_).

#### Disk Usage
5. Очень длинная программа за счет конвейера,
которая выводит **размер свободного места на диске**.
Конечно, никто не мешает сократить её, засунув в 
bashrc с alias.
```bash
 df -h --total 
    | grep "total" 
    | grep -E -o "[0-9]+[BKMGTP]" 
    | echo "Available disk storage $(tail -1)"
 ```

6. Немного видоизмененная команда для вывода
используемого дискового пространства папкой /home.
```shell
df -h /home 
    | grep -E -o "[0-9]+[BKMGTP]" 
    | tail -2 
    | echo "/home used $(head -1) of disk storage"
```


7. Команда `top` предназначена для вывода
списка процессов компьютера.