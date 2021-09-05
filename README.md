# Devops - вопросы на собеседованиях

Частые вопросы на devops (middle) собеседованиях в разные IT компании СНГ.

## Общие понятия

* Что такое Devops в вашем понимании? Зачем он нужен?
    > Быстрей и надёжней доставлять ПО на сервера. Частота релизов. Минимум ТТМ (Time to market). Чаще фичи - быстрей соответствуем рынку - быстрей экспансия и больше денег.
* Связь Agile и Devops?

    Взято [тут](https://www.itweek.ru/management/article/detail.php?ID=186691)

    > **В плане методологии и развертывания:**

    > Agile - методика разработки ПО. После того, как ПО создано и выпущено, команда разработчиков формально за него больше не отвечает, приступая к другой работе. DevOps направлен на то, чтобы взять это готовое ПО и развернуть его как можно более безопасным и надежным способом. Это разные дисциплины, которые могут работать совместно.

    > **Кросс-функциональность vs разрозненность:**

    > Важным фактором во многих процессах Agile-разработки является то, что каждый член команды может выполнять любую работу. Идея состоит в том, чтобы член команды не ждал, пока специалист освободится и займется следующим этапом процесса. Напротив, каждый свободный разработчик должен уметь сделать то, что нужно для продвижения проекта вперед. Такой подход не только ускоряет разработку, но и улучшает взаимопонимание и упрощает коммуникацию в команде. DevOps, напротив, подразумевает наличие двух отдельных команд — по разработке и по эксплуатации, члены которых не перемещаются туда-сюда. Однако они часто и регулярно общаются между собой.

    > **Команды:**

    > DevOps, по определению, подразумевает совместную работу нескольких команд. Одни могут работать по модели scrum, другие — по kanban, третьи — по waterfall, но все они должны собраться вместе в момент выпуска релиза для обсуждения с командой по эксплуатации особенностей развертывания. Здесь важно понять, что методика DevOps не зависит ни от одной методики разработки.

    > **Планирование:**

    > Методика Agile подразумевает создание примерно раз в месяц версий, называемых "спринт". Выбирается время для ближайшего "спринта" и набор функций, которые должны в него войти. Команды знают, что потом выйдет следующий "спринт", в котором будет еще больше функций. Они узнают мнение пользователей и заканчивают проверку текущего функционала создаваемого "спринта". Согласно DevOps, развертывание планируется так, чтобы свести к минимуму нарушения в работе бизнеса. Например, можно развертывать каждый "спринт" как только он появляется или подождать появления нескольких "спринтов" и сразу выполнить более масштабное внедрение, чтобы поменьше потревожить бизнес. Приоритетами DevOps являются не быстрое развертывание, а минимальное нарушение работы бизнеса и максимальная надежность.

    > **Документация.**

    > Одним из важных моментов методики Agile является приоритет работающего ПО над подробной документацией. Для DevOps документация необходима, потому ПО переходит от разработчиков к другой команде, которая занимается его внедрением. Автоматизация помогает возместить недостаток документации. Однако если другой команде передается сложное ПО, одной встречи не хватит для передачи всех необходимых знаний. Поэтому члены DevOps-команд считают работающим такое ПО, для которого имеется хорошая документация.

## CI/CD

### Понятия

* Что такое CI (integration) ? - первоначальная проверка кода, линтеры, артефакты и загрузка в хранилище
    > Мы собираем код воедино и проверяем: собирается ли он, проходят ли автотесты. CI позволяет делать такие проверки автоматически.

* Что такое CD (delivery) ?
    > Каждый пайплайн запускается автоматически по триггеру из системы контроля версий. Шаги будут выполняться автоматически только в безопасной среде, а перед деплоем на Production пайплайн остановится и будет ждать ручного подтверждения. Механизм, как это будет реализовано может быть разным. От самого простого, когда ответственный человек должен зайти в пайплайн и нажать кнопку Next, до интерактивного бота с кнопками в корпоративном мессенджере.

* Что такое CD (deployment) ?
    > Каждый пайплайн запускается автоматически по триггеру из системы контроля версий. В случае Continuous Deployment каждый следующий шаг, будет выполнен автоматически если предыдущий был успешный, включая деплой на Production.

* Отличие continuous delivery от continuous deployment?
    > как следует из изложенного выше - отличия состоит в способе передачи артефактов в Production.

* Типовой pipeline: lint -> tests -> docker image build + push -> ssh login: deploy (docker swarm deploy).

* Бесшовный деплой без потери пакетов. Как сделать чтобы при обновлении докер образов пакеты не терялись при переключении?
    > Ответ применительно к K8S. [Существуют различные стратегии деплоя. ](https://habr.com/ru/company/flant/blog/471620/) Для кубера наиболее популярные это rolling, recreate, blue/green, canary, dark. бОльшая часть из них помогает осуществить задачу zero-downtime при обновлении.
### Инструменты

* GitLab - include
* GitLab - rules
* GitLab - anchors
* GitLab - after_script - передаётся ли переменная от script в after_script?

## Git

* Gitflow - основной процесс, основные ветки?
    > [Лучшее объяснение GitFlow](https://www.atlassian.com/ru/git/tutorials/comparing-workflows/gitflow-workflow)

* Отличие git pull от git fetch
    > При использовании pull, git пытается сделать всё за вас. Он сливает любые внесённые коммиты в ветку, в которой вы сейчас работаете. Команда pull автоматически сливает коммиты, не давая вам сначала просмотреть их. При использовании fetch, git собирает все коммиты из целевой ветки, которых нет в текущей ветке, и сохраняет их в локальном репозитории. Однако он не сливает их в текущую ветку. Чтобы слить коммиты в основную ветвь, нужно использовать merge. Грубо говоря, по дефолту git pull — это шоткод для последовательности двух команд: git fetch (получение изменений с сервера) и git merge (сливание в локальную копию). (C)Никита Прияцелюк

* Отличие rebase от cherry-pick?
    > git rebase "сшивает" коммиты текущей и указанной ветки по датам создания. Указанная ветка "растворяется" в текущей. git chery-pick просто забирает указанные коммиты и добавляет их в самый конец истории.

    Хорошие примеры:

    ![rebase](https://habrastorage.org/files/518/b8d/bce/518b8dbce1cd4f96b30de9782ae38fcd.png)

    ![merge](https://habrastorage.org/files/1ba/818/6d8/1ba8186d879d46ff85ea7c1e192328e2.png)

    ![cherry](https://habrastorage.org/files/271/7e3/091/2717e3091f644ef2954aa2de4514f446.png)

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
    > Контейнер - это виртуальная среда, которая обеспечивает интерфейс взаимодействия между пользовательскими приложениями и методами ядра. Виртуальная машина - это полностью изолированная программная среда, эмулирующая аппаратное обеспечение некоторой платформы.

* Какие механизмы  ядра линукс обеспечивающие контейнеризацию?
    > Cgroup - Если мы запускаем какое-либо приложение в изолированном окружении, мы должны быть уверены в том, что этому приложению выделено достаточно ресурсов и что оно не будет потреблять лишние ресурсы, нарушая тем самым работу остальной системы. Для решения этой задачи в ядре Linux имеется специальный механизм — cgroups
    https://habr.com/ru/company/selectel/blog/303190/

    > Namespace - механизм ядра Linux, обеспечивающий изоляцию процессов друг от друга
    https://habr.com/ru/company/selectel/blog/279281/

* Какая используется файловая система для Docker и чем она удобна?
    > overlay2 - Есть особый класс файловых систем, которые называются Layer File System (LFS). Основная их идея заключается в том, что файловая система представляется в виде множества отдельных слоёв и результат является продуктом их объединения, можно провести аналогию с git squash.
    > Почему такая система удобна и подходит для докера? Подобная система позволяет фиксировать некоторое состояние файловой системы, и повторно использовать его в том случае, если это состояние является общим для нескольких образов.
    https://vc.ru/newtechaudit/121844-chto-takoe-docker-i-ego-dostoinstva

### Инструменты

* Dockerfile - отличие ADD от COPY ?
    > COPY будет использовать три слоя, но ADD использует только один слой. COPY копирует файл / каталог с вашего хоста, ADD копирует файл / каталог с вашего хоста в ваш образ, но также может извлекать удаленные URL, извлекать файлы TAR и т.д. Инструкция ADD разархивирует файл только если архив находится в одной папке с Dockerfile. Если ADD скачивает файл, то разархивирования не будет. ADD умеет разархивировать не все виды архивы (например, zip не умеет). [Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/).
* Dockerfile - отличие CMD от ENTRYPOINT ?
    > Docker имеет точку входа по умолчанию, которая /bin/sh -c, но не имеет команды по умолчанию. Команда в CMD запускается через точку входа. ENTRYPOINT - позволяет переопределить точку входа по умолчанию.
* Dockerfile - Multistage ?
    > [Лучше всего описано в доке](https://docs.docker.com/develop/develop-images/multistage-build/). Multistage используются для оптимизации Dockerfile, делают их читабельнее и проще для редактирования. Это позволяет сократить размер образа путем минимализации слоев в конечном.
* Почему неправильно объединять некоторые команды в один слой, например
  ```
  RUN apt install some pacakge && pip3 install -r requirements.py && python3 setup.py
  ```
  > Потому что при пересборке образа собираются только те слои, которые изменились относительно предыдущих. А в данном случае образ будет полностью пересобираться каждый раз: дольше, больше места занимает.

### Задачи

* docker run (задача с потерей файла на выходе из контейнера) - Запустили docker run -it ubuntu создали файл и вышли из интерфейса. Сохраниться ли файл?
    > Containers are immutable and you should not write data into your container that you would like to be persisted after that container stops running. You want to think about containers as unchangeable processes that could stop running at any moment and be replaced by another very easily. So, with that said, how do we write data and have a container use it at runtime or write data at runtime that can be persisted. This is where volumes come into play.

* docker networking - На хост системе выключен ipv4.forwarding. Как дать доступ к контейнеру?

### Ссылки

* https://www.docker.com/blog/top-questions-for-getting-started-with-docker/

## Orchestration

* Что такое оркестратор? Какие задачи он решает?
    > Оркестратор отвечает за автоматическое размещение, координацию и управление контейнерами

* k8s - основные примитивы? Для чего они? - pod, service, deployment, replicaset
    > A Deployment provides declarative updates for Pods and ReplicaSets.

    > A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods.

    > StatefulSet is the workload API object used to manage stateful applications.

    > A DaemonSet ensures that all (or some) Nodes run a copy of a Pod. As nodes are added to the cluster, Pods are added to them. As nodes are removed from the cluster, those Pods are garbage collected. Deleting a DaemonSet will clean up the Pods it created.

    > A Job creates one or more Pods and will continue to retry execution of the Pods until a specified number of them successfully terminate. As pods successfully complete, the Job tracks the successful completions. When a specified number of successful completions is reached, the task (ie, Job) is complete. Deleting a Job will clean up the Pods it created. Suspending a Job will delete its active Pods until the Job is resumed again.

    > A CronJob creates Jobs on a repeating schedule.

    > Service - An abstract way to expose an application running on a set of Pods as a network service. With Kubernetes you don't need to modify your application to use an unfamiliar service discovery mechanism. Kubernetes gives Pods their own IP addresses and a single DNS name for a set of Pods, and can load-balance across them.

    > Ingress - An API object that manages external access to the services in a cluster, typically HTTP. Ingress may provide load balancing, SSL termination and name-based virtual hosting.

* k8s - пять бинарников k8s - какие они? зачем?
    > Такую фразу можно часто услышать в DevOps комьюнити, её сарказм в том, что k8s выглядит простым, но на деле является очень сложным продуктом, с большим количеством вариантов запуска и конфигурирования конкретного кластера.

    > **К компонентам мастера относятся:**

    > kube-apiserver - центральный “роутер”, единственный компонент который может писать и читать etcd

    > kube-controller-manager - набор лупов, которые периодически просыпаются и обрабатывают конкретные сущности

    > etcd - key/value база данных, single source of truth

    > kube-scheduler - гранд-мастер тетриса, решает на какой ноде какой под запустить

    > **К компонентам воркер нод, относятся:**

    > kubelet - связующее звено между apiserver и непосредственно container runtime

    > kube-proxy - сетевая прокси, необходимая для работы service

    **А вот как это все работает:**
    ![А вот как это все работает](https://farm66.staticflickr.com/65535/49238858918_779ac4d57b_o.jpg)
Определения позаимствованы на https://doam.ru/kubernetest_workshop/


 * Паттерны подов (сайдкар, etc)
 * Init-контейнеры
 * Как мониторить кластер K8S?
 * Есть blue pod, blue node, red pod, red node. Как сделать так, чтобы синяя пода попала только на синюю ноду и т.д.?
  > Taints&tolarations или NodeAffinity  

  > T&T Не говорят каким подам на какие ноды можно или нельзя заходить.
    Говорят нодам, какие поды можно на себя принимать согласно толерейшенам  
    taints на ноды  
    tolerations на поды  

  > nodeSelectors Нужен для указания того, какие поды на каких нодах разворачивать. В описании пода указывается nodeSelector и kv-пара лейбла указанного на ноде

  > nodeAffinity нужен, когда мы хотим поместить/не помещать поды на определенные ноды согласно нескольким условиям, например: ИЛИ, НЕ

## Облака

* Отличие High Availability от Fault Tolerance?
    > Хорошая статья вот [тут](http://www.solidex.by/stati/kult-high-availability-i-fault-tolerance/)

## Linux

* Место кончилось, нашли большой файл удалили, проблема осталась. Почему?
    > Удаленный файл держит процесс. С помощью команды `lsof` можно посмотреть какой именно. [[Link]](https://ealebed.github.io/posts/2016/что-делать-когда-результат-выполнения-df-и-du-отличается/)
* top - load average - 10 это плохо?
* Что такое LA?
  > Среднее количество процессов или операций ввода-вывода в очереди для обращения к ядру в разрезе 1/5/15 минут.
* Что такое zombie и orphan (сирота) процессы
  > **zombie** - когда дочерний процесс завершился, сообщил об этом родительскому, но не дождался ответа.  Родительский процесс считывает результат сисколлом wait(). Мы не можем его грохнуть, потому что он уже мертв. Память он не занимает, просто строчка с списке процессов. Как избавиться: проверить, а почему родительский процесс не ответил - может он сам помер. Можно убить родительский, тогда зомби снова отправит сообщение, но уже init (PID 1), а он ответит.

  > **orphan** - когда родительский процесс умирает раньше дочернего, дочернего усыновляет PID 1
* Что такое ``st`` в top? (и вообще разбор top)
* Актуально ли использование swap, когда оперативная память не так уж и дорога?
* Что такое inode и какая информация в них хранится?
* Что находится в директории /proc и как можно использовать данные оттуда?

## Monitoring

* Prometheus - какая модель сбора метрик? (pull)
* Типовые сущности - node_exporter, blackbox, aletrmanager, push gateway
