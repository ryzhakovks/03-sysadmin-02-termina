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
