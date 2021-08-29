# Devops - вопросы на собеседованиях

Частые вопросы на devops (middle) собеседованиях в разные IT компании СНГ.

## Общие понятия

* Что такое Devops в вашем понимании? Зачем он нужен?
    > Быстрей и надёжней доставлять ПО на сервера. Частота релизов. Минимум ТТМ (Time to market). Чаще фичи - быстрей соответствуем рынку - быстрей экспансия и больше денег.
* Связь Agile и Devops?

    Взято [тут](https://www.itweek.ru/management/article/detail.php?ID=186691)

    > В плане методологии и развертывания:

        Agile - методика разработки ПО. После того, как ПО создано и выпущено, команда разработчиков формально за него больше не отвечает, приступая к другой работе. DevOps направлен на то, чтобы взять это готовое ПО и развернуть его как можно более безопасным и надежным способом. Это разные дисциплины, которые могут работать совместно.

    > Кросс-функциональность vs разрозненность:

        Важным фактором во многих процессах Agile-разработки является то, что каждый член команды может выполнять любую работу. Идея состоит в том, чтобы член команды не ждал, пока специалист освободится и займется следующим этапом процесса. Напротив, каждый свободный разработчик должен уметь сделать то, что нужно для продвижения проекта вперед. Такой подход не только ускоряет разработку, но и улучшает взаимопонимание и упрощает коммуникацию в команде. DevOps, напротив, подразумевает наличие двух отдельных команд — по разработке и по эксплуатации, члены которых не перемещаются туда-сюда. Однако они часто и регулярно общаются между собой.

    > Команды:

        DevOps, по определению, подразумевает совместную работу нескольких команд. Одни могут работать по модели scrum, другие — по kanban, третьи — по waterfall, но все они должны собраться вместе в момент выпуска релиза для обсуждения с командой по эксплуатации особенностей развертывания. Здесь важно понять, что методика DevOps не зависит ни от одной методики разработки.

    > Планирование:

        Методика Agile подразумевает создание примерно раз в месяц версий, называемых "спринт". Выбирается время для ближайшего "спринта" и набор функций, которые должны в него войти. Команды знают, что потом выйдет следующий "спринт", в котором будет еще больше функций. Они узнают мнение пользователей и заканчивают проверку текущего функционала создаваемого "спринта". Согласно DevOps, развертывание планируется так, чтобы свести к минимуму нарушения в работе бизнеса. Например, можно развертывать каждый "спринт" как только он появляется или подождать появления нескольких "спринтов" и сразу выполнить более масштабное внедрение, чтобы поменьше потревожить бизнес. Приоритетами DevOps являются не быстрое развертывание, а минимальное нарушение работы бизнеса и максимальная надежность.

    > Документация.

        Одним из важных моментов методики Agile является приоритет работающего ПО над подробной документацией. Для DevOps документация необходима, потому ПО переходит от разработчиков к другой команде, которая занимается его внедрением. Автоматизация помогает возместить недостаток документации. Однако если другой команде передается сложное ПО, одной встречи не хватит для передачи всех необходимых знаний. Поэтому члены DevOps-команд считают работающим такое ПО, для которого имеется хорошая документация.

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
