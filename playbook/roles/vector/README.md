# Задание 08-ansible-05-testing

## Molecule

1. molecule test -s ubuntu_focal

![Stage1](./pictures/Stage1.png)

2. molecule init scenario --driver-name docker

![Stage2](./pictures/Stage2.png)

3. molecule test

![Stage3_1_err](./pictures/Stage3_1_err.png)
![Stage3_2_err](./pictures/Stage3_2_err.png)
![Stage3_3_err](./pictures/Stage3_3_err.png)
![Stage3_4_err](./pictures/Stage3_4_err.png)

Ошибки:
 - в используемых RedHat-подобных ОС отсутствует sudo
 - в RedHat-подобных ОС ошибки инициализации systemd
Решение:
 - использование существующих пользовательских прав
 - уход от использования сервиса vector, переход на использование tmux

molecule test

![Stage3_1_ok](./pictures/Stage3_1_ok.png)
![Stage3_2_ok](./pictures/Stage3_2_ok.png)
![Stage3_3_ok](./pictures/Stage3_3_ok.png)
![Stage3_4_ok](./pictures/Stage3_4_ok.png)
![Stage3_5_ok](./pictures/Stage3_5_ok.png)
![Stage3_6_ok](./pictures/Stage3_6_ok.png)

