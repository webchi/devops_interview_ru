# Devops - вопросы на собеседованиях
Частые вопросы на devops (middle) собеседованиях в разные IT компании СНГ.


## Общие понятия 
* Что такое Devops в вашем понимании? Зачем он нужен? 
    > Быстрей и надёжней доставлять ПО на сервера. Частота релизов. Минимум ТТМ (Time to market). Чаще фичи - быстрей соответствуем рынку - быстрей экспансия и больше денег.
* Связь Agile и Devops?

## CI/Cd
### Понятия
* Что такое CI (integration) ? - первоначальная проверка кода, линтеры, артефакты и загрузка в хранилище
* Что такое CD (delivery) ? - доставка из хранилища на сервера в среду. 
* Что такое CD (deployment) ? - то же самое. 
* Отличие continuous delivery от continuous deployment?
* Типовой pipeline: lint -> tests -> docker image build + push -> ssh login: deploy (docker swarm deploy). 
* Бесшовный деплой без потери пакетов. Как сделать чтобы при обновлении докер образов пакеты не терялись при переключении?

### Инструменты
* GitLab - include 
* GitLab - rules 
* GitLab - anchors 
* GitLab - after_script - передаётся ли переменная от script в after_script?

## Git
* Gitflow - основной процесс, основные ветки? 
* Отличие git pull от git fetch
* Отличие rebase от cherry-pick?


## Docker
### Понятия
* Зачем нужен Docker какие задачи он решает? 
    > Осуществляя процесс автоматизации развертывания приложения, Docker может предложить пользователю следующие возможности:
    > - Изоляция запущенных приложений. Можно отделить ваше приложение от ОС хоста и обращаться с ним ?> как с управляемым приложением.
    > - Облегчение процесса разработки, тестирования и развертывания приложений
    > - Нет необходимости в конфигурации среды для запуска – она поставляется вместе с приложением.
    https://vc.ru/newtechaudit/121844-chto-takoe-docker-i-ego-dostoinstva
    > - Что бы не ныли программисты “у меня локально всё работает” - воспроизводимость рабочего окружения

* Какая разница между виртуализацией и контейнеризацнией?
* Какие механизмы  ядра линукс обеспечивающие контейнеризацию? 
    > Cgroup - Если мы запускаем какое-либо приложение в изолированном окружении, мы должны быть уверены в том, что этому приложению выделено достаточно ресурсов и что оно не будет потреблять лишние ресурсы, нарушая тем самым работу остальной системы. Для решения этой задачи в ядре Linux имеется специальный механизм — cgroups
    https://habr.com/ru/company/selectel/blog/303190/
    
    > Namespace - механизм ядра Linux, обеспечивающий изоляцию процессов друг от друга
    https://habr.com/ru/company/selectel/blog/279281/

* Какая используется файловая система и чем она удобна?
    > overlay2 - Есть особый класс файловых систем, которые называются Layer File System (LFS). Основная их идея заключается в том, что файловая система представляется в виде множества отдельных слоёв и результат является продуктом их объединения, можно провести аналогию с git squash.
    > Почему такая система удобна и подходит для докера? Подобная система позволяет фиксировать некоторое состояние файловой системы, и повторно использовать его в том случае, если это состояние является общим для нескольких образов.
    https://vc.ru/newtechaudit/121844-chto-takoe-docker-i-ego-dostoinstva

### Инструменты
* Dockerfile - отличие ADD от COPY ?
* Dockerfile - отличие CMD от ENTRYPOINT ? 
* Dockerfile - Multistage ?

### Задачи
* docker run (задача с потерей файла на выходе из контейнера) - Запустили docker run -it ubuntu создали файл и вышли из интерфейса. Сохраниться ли файл?
* docker networking - На хост системе выключен ipv4.forwarding. Как дать доступ к контейнеру? 
### Ссылки
* https://www.docker.com/blog/top-questions-for-getting-started-with-docker/

## Orchestration
* Что такое оркестратор? Какие задачи он решает?
* k8s - основные примитивы? Для чего они? - pod, service, deployment
* k8s - пять бинарников k8s - какие они? зачем?

## Облака
* Отличие High Availability от Fault Tolerance?

## Linux 
* Место кончилось, нашли большой файл удалили, проблема осталась. Почему?
    > Удаленный файл держит процесс. С помощью команды `lsof` можно посмотреть какой именно. [[Link]](https://ealebed.github.io/posts/2016/что-делать-когда-результат-выполнения-df-и-du-отличается/)
* top - load average - 10 это плохо?

## Monitoring
* Prometheus - какая модель сбора метрик? (pull) 
* Типовые сущности - node_exporter, blackbox, aletrmanager, push gateway
