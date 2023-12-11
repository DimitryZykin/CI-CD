# CI-CD_Seminar_03

# CI/CD. Семинар 03. Continuous delivery и continuous deployment (непрерывная доставка и развертывание)

## Задача
1. Добавить 2 окружения "preprod" и "production"
2. Добавить отдельные deploy job для каждой среды
3. Добавить переменную "$MyLogin" внутри .gitlab-ci.yml, которая будет меняться в зависимости от среды.
4. Добавить переменную "$MyPassword" не используя .gitlab-ci.yml, которая так же будет меняться в зависимости от среды.
5. Добавить скрипт в .gitlab-ci.yml, который найдёт все запущенные pipeline по названии ветки(ref) и остановит их.



## Решение

### Пункты 1, 2, 3, 4

Добавляем окружение `preprod` и `production`. При этом используем переменную `$MyLogin`.
```yaml
deploy to preprod:
  stage: deploy
  variables:
    TARGET_ENV: preprod
    MyLogin: "Preprod DMITRIY"
  script:
    - echo "Do your deploy here to ${TARGET_ENV}"
    - echo ${DB_SERVER}
    - echo "MyLogin"
    - echo $MyLogin
    - echo "MyPassword"
    - echo $MyPassword
  only:
    - main
  environment:
    name: preprod
```


```yaml
deploy to production:
  stage: deploy
  variables:
    TARGET_ENV: production
    MyLogin: "Production DMITRIY"
  script:
    - echo "Do your deploy here to ${TARGET_ENV}"
    - echo ${DB_SERVER}
    - echo "MyLogin"
    - echo $MyLogin
    - echo "MyPassword"
    - echo $MyPassword
  only:
    - main
  environment:
    name: production
```

Для настройки переменных добавляем переменную `$MyPassword` через интерфейс. Для разных сред исполнения она будет разной. 

![variables page](img/VirtualBox_cibox_03_12_2023_15_22_42.png "variables page")

Pipeline passed
![pipeline passed](img/VirtualBox_cibox_03_12_2023_15_29_27.png "pipeline passed")

Deploy to preprod. На скриншоте — уникальные $MyLogin и $MyPassword для preprod
![deploy to preprod](img/VirtualBox_cibox_03_12_2023_15_31_48.png "deploy to preprod")

Deploy to production. Для production — свои $MyLogin и $MyPassword
![deploy to production](img/VirtualBox_cibox_03_12_2023_15_39_31.png "deploy to production")

### Пункт 5


1
