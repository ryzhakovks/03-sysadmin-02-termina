**Задание 1.Какого типа команда cd? Попробуйте объяснить, почему она именно такого типа: опишите ход своих мыслей, если считаете, что она могла бы быть другого типа.**

Встроенная команда оболчки, она выполняет одну задачу. Думаю достаточно )
```ruby
type -a cd
cd is a shell builtin
```

**Задание 2. Какая альтернатива без pipe команде grep <some_string> <some_file> | wc -l?
Подсказка
man grep поможет в ответе на этот вопрос.
Ознакомьтесь с документом о других подобных некорректных вариантах использования pipe.**

Взял для примера файл .bashrc c pipe овтет такой

```ruby
root@MMRU59A0000:~# grep alias .bashrc | wc -l
14
```
Без pipe нашел такю комбинацию

```ruby
root@MMRU59A0000:~# grep -c alias .bashrc
14
```

**Задание 3. Какой процесс с PID 1 является родителем для всех процессов в вашей виртуальной машине Ubuntu 20.04?**

systemd получается 

```ruby
root@MMRU59A0000:~#pstree -p
systemd(1)─┬─accounts-daemon(1082)─┬─{accounts-daemon}(1135)
           │                       └─{accounts-daemon}(1147)
           ├─atd(1080)
           ├─chronyd(1390)
           ├─containerd(1481)─┬─{containerd}(1678)
```


**Задание 4. Как будет выглядеть команда, которая перенаправит вывод stderr ls на другую сессию терминала?**
Консоль 1 
```ruby
fpadmin@fp-sys-demo:~$ tty
/dev/pts/0
fpadmin@fp-sys-demo:~$ ls -lha "Чо То пошло не так" 2>/dev/pts/1
```
Консоль2 
```ruby
root@fp-sys-demo:~# ps
  PID TTY          TIME CMD
16863 pts/1    00:00:00 sudo
16868 pts/1    00:00:00 bash
17086 pts/1    00:00:00 ps
root@fp-sys-demo:~# ls: невозможно получить доступ к 'Чо То пошло не так': Нет такого файла или каталога
```

**Задание 5. Получится ли одновременно передать команде файл на stdin и вывести ее stdout в другой файл? Приведите работающий пример.**
```ruby
root@MMRU59A0000:~# ls /var > zadanie_5 | grep -n 'l*' zadanie_5 | tee zadanie_5_1
1:backups
2:cache
3:crash
4:lib
5:local
6:lock
7:log
8:mail
9:opt
10:run
11:snap
12:spool
13:tmp
```


