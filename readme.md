### Попасть в систему без пароля
Открываем GUI VirtualBox, запускаем виртуальную машину и при выборе ядра для загрузки нажимаем e (edit). Попадаем в окно, где мы можем изменить параметры загрузки.

## Способ 1. init=/bin/sh
В конце строки начинающейся с linux16 добавляем init=/bin/sh и нажимаем сtrl-x для
загрузки в систему
Переходим из режима Read-Only в Read-Write
```
mount -o remount,rw /
```

## Способ 2. rd.break
В конце строки начинающейся с linux16 добавляем rd.break и нажимаем сtrl-x для
загрузки в систему
Попадаем в emergency mode, переходим из режима Read-Only в Read-Write и меняем пароль администратора.
```
mount -o remount,rw /sysroot
chroot /sysroot
passwd root
touch /.autorelabel
```

## Способ 3. rw init=/sysroot/bin/sh
В строке начинающейся с linux16 заменяем ro на rw init=/sysroot/bin/sh и нажимаем сtrl-x для
загрузки в систему.
Попадаем в emergencu mode.

## Различия способов.
В первом способе мы оказываемся в рутовой файловой системе, во втором и третьем изначально попадаем в mergency mode.
В третьем способе файловая система сразу смонирована в Read-Write режиме, в первых двух способах можно заменить ro на rw и получить тот же режим.

 /dev/sda2: UUID="570897ca-e759-4c81-90cf-389da6eee4cc" TYPE="xfs" 
/dev/sda3: UUID="vrrtbx-g480-HcJI-5wLn-4aOf-Olld-rC03AY" TYPE="LVM2_member" 
/dev/mapper/VolGroup00-LogVol00: UUID="b60e9498-0baa-4d9f-90aa-069048217fee" TYPE="xfs" 
/dev/mapper/VolGroup00-LogVol01: UUID="c39c5bed-f37c-4263-bee8-aeb6a6659d7b" TYPE="swap" 

