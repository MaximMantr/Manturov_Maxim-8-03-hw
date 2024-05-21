## Домашнее задание к занятию «GitLab» 
## `Мантуров Максим Андреевич`



---

### Задание 1 

#### Задачи

- Развернуть GitLab локально, используя Vagrantfile.
- Создайть новый проект и пустой репозиторий в нём.
- Зарегистрировать gitlab-runner для этого проекта и запустить его в режиме Docker.

`Этапы выполнение задания представленны в виде скриншотав`
---
- Развернутый GitLab и созданный в нем проект пустой.
![1-2](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/Instal/2.png)
![1-3](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/Instal/3.png)
![1-1](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/Instal/1.png)
---
- Регистрация gitlab-runner для этого проекта и запустить его в режиме Docker.
![1](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/runner/1.png)
![4](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/runner/4.png)
![2](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/runner/2.png)

`Конфигурация gitlab-runner `
![5](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/runner/5.png)
---

### Задание 2 

#### Задачи

- Запушить репозиторий на GitLab, изменив origin.
- Создать .gitlab-ci.yml, описав в нём все необходимые, на мой взгляд, этапы. 

`Этапы выполнение задания представленны в виде скриншотав`
---
- Запушенный репозиторий и изменненный origin, и последующие залитие его на локальный GitLab
![2-5](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/clone/5.png)
---
- На этом этапе у меня возникли проблемы. На решение которых у меня ушло целых 3 вечера. 
![2-6](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/clone/6.png)
![2-7](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/clone/7.png)
`Вывод который я сделал: Нужно еще больше изучить Git`
---
![2-8](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/clone/8.png)
![2-11](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/clone/11.png)
---
- Работа gitlab-runner при выполнение .gitlab-ci.yml и описанных в этом файле этапов.
`config файл .gitlab-ci.yml Пример`
```
# Этот файл описывает этапы сборки и тестирования проекта

stages:
  - build
  - test
  - deploy

build:
  stage: build
  script:
    - echo "Сборка проекта..."
#   - ./build_script.sh  Пример Этап сборки включает в себя выполнение скрипта build_script.sh, который выполняет сборку проекта
  
test:
  stage: test
  script:
    - echo "Тестирование проекта..."
#    - ./test_script.sh Пример Этап тестирования включает в себя выполнение скрипта test_script.sh, который выполняет тестирование проекта.

deploy:
  stage: deploy
  script:
    - echo "Развертывание проекта..."
#    - ./deploy_script.sh Пример Этап развёртывания включает в себя выполнение скрипта deploy_script.sh, который выполняет развёртывание проекта. 
  only: Пример Этап развёртывания выполняется только при переходе в ветку master.
    - master
```
`Мой config`
![2-9](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/test/9.png)
---
- Этап создания .gitlab-ci.yml и его пройденые тесты 
![2-10](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/test/10.png)
![2-12](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/test/12.png)
![2-13](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/test/13.png)
![2-14](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/gitlab/img/GitLab/test/14.png)
---
> Спасибо за внимание







