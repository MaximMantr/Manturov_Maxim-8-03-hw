## Домашнее задание к занятию  " 8.2. Что такое DevOps. СI/СD"
## `Мантуров Максим Андреевич`

### Задание №1
- Установить себе Jenkins не используя Docker. 
- Установить на машину с Jenkins golang.
- Используя свой аккаунт на GitHub, сделайте себе форк репозитория.
- Создать в Jenkins Freestyle Project, подключить получившийся репозиторий к нему и произведите запуск тестов и сборку проекта  go test . и docker build ..
---
### `Выполнение задания`
---
#### 1 Установа велась из Vagrant файла на скришоте придставлены хоррактеристики сети. 
![1-1](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/1/1.png)
#### 2 Командой sudo systemctl status jenkins.service мы проверяем работу Jenkins 
![1-1-2](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/1/1-2.png)
![1-4](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/1/4.png)
![1-5](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/1/5.png)
`Установка и настройка golang`
```
wget https://go.dev/dl/go1.17.5.linux-amd64.tar.gz
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.17.5.linux-amd64.tar.gz
echo 'export PATH=$PATH:/usr/local/go/bin' >> /etc/profile

```
#### 3 Запуск тестов и сборки 
![1-10](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/1/10.png)
![1-11](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/1/11.png)
![1-12](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/1/12.png)
---

### Задание №2 
- Создайть новый проект pipeline.
- Переписать сборку из задания 1 на declarative в виде кода.
---
### `Выполнение задания`
---
`Конфигурация`
```
pipeline {
 agent any
 stages {
  stage('Git') {
   steps {git 'https://github.com/MaximMantr/sdvps-materials-01.git'} // Подключение git репозитория
  }
  stage('Test') {
   steps {
    sh '/usr/local/go/bin/go test' // Тест goleng 
   }
  }
  stage('Build') {
   steps {
    sh 'docker build .'  // Произвести сбору проекта из Dockerfile
   }
  }
 }
}

```
`Скришоты успешно выполненного pipeline`
![2-1](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/2/1.png)
![2-2](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/2/2.png)
![2-3](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/2/3.png)
![2-4](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/2/4.png)
![2-5](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/2/5.png)
![2-6](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/2/6.png)
---
### Задание №3 
- Установить на машину Nexus.
- Создать raw-hosted репозиторий.
- Изменить pipeline так, чтобы вместо Docker-образа собирался бинарный go-файл. Команду можно скопировать из Dockerfile.
- Загрузить файл в репозиторий с помощью jenkins.
---
### `Выполнение задания`
---
`Конфигурация`
```
pipeline {

    agent any
    
    stages {
        
        stage('Git') {
            steps {git 'https://github.com/MaximMantr/sdvps-materials-01.git'} // Подключенный git репозиторий.
        
            
        }

        stage('Build Go Binary') {

            steps {
                script {
                    sh '/usr/local/go/bin/go test'  // Команда для теста. 
                    sh '/usr/local/go/bin/go build main.go ' // Команда для сборки go-файла.
                   

                }
            }
        }
        stage('upload file') {
         
            steps {
                script {
                    sh 'tar -cvf main.tar main' // Архивируем получившийся после сбори файл. 
                    sh 'curl -u admin:tty12 http://192.168.56.10:8081/repository/go_bin-NEXUS/ --upload-file main.tar -v'  // Команда для отправки на NTXUS  tar архива.
                    sh 'curl -u admin:tty12 http://192.168.56.10:8081/repository/go_bin-NEXUS/ --upload-file main -v' // Команда для отправки на NTXUS  бинарного go-файла.
                    
                }
                
            }
        }
    }
}

```
`Скришоты успешно выполненного pipeline`
---
#### NEXUS на 192.168.56.10:8081
![3](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/3/1.png)
![3](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/3/2.png)
---
![3](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/3/3.png)
![3](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/3/4.png)
![3](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/3/5.png)
![3](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/3/6.png)
`Скриншот всех удачно выполненых заданий`
![3](https://github.com/MaximMantr/Manturov_Maxim-8-03-hw/blob/jenkins/img/Jenkins/3/7.png)