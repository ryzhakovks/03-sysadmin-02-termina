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

**Задание 6. Получится ли находясь в графическом режиме, вывести данные из PTY в какой-либо из эмуляторов TTY? Сможете ли вы наблюдать выводимые данные?**

Я еще не перешол на сторону добра , у меня доступ к linux только по ssh. Я конечно мог для задание развернуть вм с gui, но суть ответа будет как в задание 4. Отправить в другой терминал/
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
Но так
```ruby
echo "Иду в другой термнал" > /dev/pts/1
```

**Задание 7. Выполните команду bash 5>&1. К чему она приведет? Что будет, если вы выполните echo netology > /proc/$$/fd/5? Почему так происходит?**
bash 5>&1 создаёт файловый дескриптор 5 для stdout, при выполнении echo netology > /proc/$$/fd/5 она выовдит его на стандартное устройство вывода

**Задание 8. Получится ли в качестве входного потока для pipe использовать только stderr команды, не потеряв при этом отображение stdout на pty?
Напоминаем: по умолчанию через pipe передается только stdout команды слева от | на stdin команды справа. Это можно сделать, поменяв стандартные потоки местами через промежуточный новый дескриптор, который вы научились создавать в предыдущем вопросе.***
```ruby
root@MMRU59A0000:~# echo "8" > zd8
root@MMRU59A0000:~# ls
zadanie_5  zadanie_5_1  zd8
root@MMRU59A0000:~# cat z
zadanie_5    zadanie_5_1  zd8
root@MMRU59A0000:~# cat zd8
8
root@MMRU59A0000:~# echo "8.1" > zd8.1
root@MMRU59A0000:~# cat -n zd8 && cat -n zd8.1 6>&1 1>&2 2>&6 |wc -l
     1  8
     1  8.1
0
```

**Задание 9.Что выведет команда cat /proc/$$/environ? Как еще можно получить аналогичный по содержанию вывод?**
Переменные  окружения для  текущего процесса

**Задание 10. Используя man, опишите что доступно по адресам /proc/<PID>/cmdline, /proc/<PID>/exe.**
/proc/[pid]/cmdline содержит командную строку и аргументы процесса если это не зомби /proc/[pid]/exe содержит симлинк на исполняемую команду. Можно запустить с помощью этой команды копию процесса. 

** Задание 11.Узнайте, какую наиболее старшую версию набора инструкций SSE поддерживает ваш процессор с помощью /proc/cpuinfo.**
 ```ruby         
  root@MMRU59A0000:~# grep sse /proc/cpuinfo
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc rep_good nopl xtopology tsc_reliable nonstop_tsc cpuid pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand hypervisor lahf_lm abm 3dnowprefetch invpcid_single ssbd ibrs ibpb stibp ibrs_enhanced fsgsbase bmi1 avx2 smep bmi2 erms invpcid avx512f avx512dq rdseed adx smap avx512ifma clflushopt avx512cd sha_ni avx512bw avx512vl xsaveopt xsavec xgetbv1 xsaves avx512vbmi umip avx512_vbmi2 gfni vaes vpclmulqdq avx512_vnni avx512_bitalg avx512_vpopcntdq rdpid fsrm flush_l1d arch_capabilities
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc rep_good nopl xtopology tsc_reliable nonstop_tsc cpuid pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand hypervisor lahf_lm abm 3dnowprefetch invpcid_single ssbd ibrs ibpb stibp ibrs_enhanced fsgsbase bmi1 avx2 smep bmi2 erms invpcid avx512f avx512dq rdseed adx smap avx512ifma clflushopt avx512cd sha_ni avx512bw avx512vl xsaveopt xsavec xgetbv1 xsaves avx512vbmi umip avx512_vbmi2 gfni vaes vpclmulqdq avx512_vnni avx512_bitalg avx512_vpopcntdq rdpid fsrm flush_l1d arch_capabilities
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc rep_good nopl xtopology tsc_reliable nonstop_tsc cpuid pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand hypervisor lahf_lm abm 3dnowprefetch invpcid_single ssbd ibrs ibpb stibp ibrs_enhanced fsgsbase bmi1 avx2 smep bmi2 erms invpcid avx512f avx512dq rdseed adx smap avx512ifma clflushopt avx512cd sha_ni avx512bw avx512vl xsaveopt xsavec xgetbv1 xsaves avx512vbmi umip avx512_vbmi2 gfni vaes vpclmulqdq avx512_vnni avx512_bitalg avx512_vpopcntdq rdpid fsrm flush_l1d arch_capabilities
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc rep_good nopl xtopology tsc_reliable nonstop_tsc cpuid pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand hypervisor lahf_lm abm 3dnowprefetch invpcid_single ssbd ibrs ibpb stibp ibrs_enhanced fsgsbase bmi1 avx2 smep bmi2 erms invpcid avx512f avx512dq rdseed adx smap avx512ifma clflushopt avx512cd sha_ni avx512bw avx512vl xsaveopt xsavec xgetbv1 xsaves avx512vbmi umip avx512_vbmi2 gfni vaes vpclmulqdq avx512_vnni avx512_bitalg avx512_vpopcntdq rdpid fsrm flush_l1d arch_capabilities
```         
sse4_1
