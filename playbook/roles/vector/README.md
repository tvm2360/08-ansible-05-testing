# Задание 08-ansible-05-testing

## Molecule

1. Тест
``` bash
molecule test -s ubuntu_focal
```
![Stage1](./pictures/Stage1.png)

2. Добавление сценария
``` bash
molecule init scenario --driver-name docker
```
![Stage2](./pictures/Stage2.png)

3. Проверка на ошибки
``` bash
molecule test
```

![Stage3_1_err](./pictures/Stage3_1_err.png)
![Stage3_2_err](./pictures/Stage3_2_err.png)
![Stage3_3_err](./pictures/Stage3_3_err.png)
![Stage3_4_err](./pictures/Stage3_4_err.png)

Ошибки:
 - в используемых RedHat-подобных ОС отсутствует sudo
 - в RedHat-подобных ОС ошибки инициализации systemd

Решение:
 - использование существующих пользовательских прав
 - уход от использования сервиса для vector, переход на использование tmux

``` bash
molecule test
```

![Stage3_1_ok](./pictures/Stage3_1_ok.png)
![Stage3_2_ok](./pictures/Stage3_2_ok.png)
![Stage3_3_ok](./pictures/Stage3_3_ok.png)
![Stage3_4_ok](./pictures/Stage3_4_ok.png)
![Stage3_5_ok](./pictures/Stage3_5_ok.png)
![Stage3_6_ok](./pictures/Stage3_6_ok.png)

4. verify.yml
``` ansible
- name: Verify vector
  hosts: all
  gather_facts: false
  tasks:
  - name: "stat file vector exists"
    stat:
      path: "/opt/vector/bin/vector"
    register: file_vector_stat
  - name: "stat file vector config exists"
    stat:
      path: "/opt/vector/config/vector.yaml"
    register: file_vector_config_stat
  - name: "check if file vector exists"
    assert:
      that:
        - file_vector_stat.stat.exists == True
      success_msg: "vector exists"
      fail_msg: "vector doesn't exist"
  - name: "check if file vector config exists"
    assert:
      that:
        - file_vector_config_stat.stat.exists == True
      success_msg: "vector config exists"
      fail_msg: "vector config doesn't exist"
```

5. Проверка успешна
![Stage5](./pictures/Stage5.png)
