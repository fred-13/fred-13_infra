# fred-13_infra
fred-13 Infra repository

#--------------------Homework 8 -------------------

1. Создана новая ветка ansible-2.
2. Создан файл плейбука reddit_app.yml
3. Добавление модуля template в плейбук (mongod.conf.j2)
4. Определение тэгом таски, затем тестовый прогон "ansible-playbook reddit_app.yml --check --limit db"
5. Добавление handlers в плейбук
6. Разделение сценариев в плейбук reddit_app2.yml
7. Разбиение на несколько плейбуков app.yml, db.yml, deploy.yml
8. Объедние и запуск плебйков из пункта 7 путем их импорта в плебук site.yml
9. Создание образов через packer с помощью Ansible (packer_app.yml, packer_db.yml)
10. Выполнено задание для самостоятельной работы
11. Проверка образов с помощью плейбука site.yml (успех).

#--------------------------------------------------

#--------------------Homework 8 -------------------

1. Создал ветку ansible-1.
2. Установил Ansible 2.7 паекетным менеджером "pip install -r requirements.txt"
3. Создал проект с помощью terraform из stage модуля.
4. Прописал хосты в inventory и отработал команды по проверке коннекта к этим хостам "ansible appserver -i ./inventory -m ping".
5. Прописал значения по умолчанию в ansible.cfg и подкорректировал inventory.
6. Создал файл inventory.yml отработал команды по проверке коннекта к этим хостам "ansible all -m ping -i inventory.yml"
7. Проверил выполнение команд command и shell
8. Создал файл clone.yml для клонирование репозитория.
9. Вывод "ansible-playbook clone.yml"

Наблюдение: 
сначало "ansible app -m command -a 'rm -rf ~/reddit'" 
затем: " ansible-playbook clone.yml"

TASK [Clone repo] **********************************************************
changed: [appserver]

PLAY RECAP *****************************************************************
appserver                  : ok=2    changed=1    unreachable=0    failed=0

10. Выполнены задания со *

#--------------------------------------------------


#--------------------Homework 7 -------------------

1. Создана ветка terraform-2.
2. Перенесен файл файл lb.tf в terraform/files
3. Удалено дефолтное описание файервола на доступ по SSH. Доступ теперь описан в основном файле main.tf и импортирован в терраформ.
4. Зададал IP для инстанса с приложением в виде внешнего ресурса.
5. Запек два интсанса с Ruby и MongDB с помощью инструмента packer описанием в 
db.json и app.json.
6. Создал две VM reddit-app и reddit-db с помощью шаблонов из пункта 5.
7. Создал файл vpc.tf с описанем правила фаервола для ssh доступа.
8. Создал и загрузил модули APP, DB и VPC.
9. Выполнил задания для самостоятельной работы с 1 по 3.
10. Создал два окржуения для инфраструктуры прода и стейджа.
11. Выполнил самостоятельные задания с 1 по 3-ю.

#-------------------------------------------------

#--------------------Homework 6 -------------------

1. Создана новая ветка terraform-1
2. Удалены ssh ключи из метаданных.
3. Установлен Terraform через переменную окружения.
4. Созданы файлы main.tf и .gitignore
5. Проделаны задания по созданию и подключению к инстансу (вывод внешенего айпи в файл outputs.tf).
6. Настройка деплоя с помощью Provisioners.
7. Описание переменнных в файле variables.tf и их определение в terraform.tfvars
8. Выполнены задания для самостоятельного разбора с 1 по 4-й.
9. Выполнено 1-е задание со * Примечание: после выполнения команды terraform apply все ключи перезаписываются,
а добавленые через веб-интерфейс вручную - удаляются.
10. Выполнено второе задание со * Добавлен файл балансировщика, модифицирован основной файл main.tf
для упрощения добавления количества инстансов.

#-------------------------------------------------


#--------------------Homework 5 -------------------

1. Создана новая ветка packer-base
2. Перенесены все наработки с прошлого занятия в директорию config-scripts
3. Скачан и установлен в переменную окружения packer
4. Настроена синхронизация терминала с проектом в google cloud 
5. Собран шаблон ubuntu16.json и на его основе создан базовый образ reddit-base
6. Выполнены задания для самостоятельной работы с 1 по 3-й
7. Выполнены задания со *


#-------------------------------------------------


#--------------------Homework 4 -------------------

testapp_IP = 35.240.22.197
testapp_port = 9292

# Инсталим хомяка запуская скрипт с локальной директории:

gcloud compute instances create reddit-app\
  --boot-disk-size=10GB \
  --image-family ubuntu-1604-lts \
  --image-project=ubuntu-os-cloud \
  --machine-type=g1-small \
  --tags puma-server \
  --restart-on-failure \
  --metadata-from-file startup-script=/home/startup.sh

# Инсталим хомяка запуская скрипт из бакета:

gcloud compute instances create reddit-app\
  --boot-disk-size=10GB \
  --image-family ubuntu-1604-lts \
  --image-project=ubuntu-os-cloud \
  --machine-type=g1-small \
  --tags puma-server \
  --restart-on-failure \
  --metadata startup-script-url=https://console.cloud.google.com/storage/browser/cloud-testapp/startup.sh

# Открываем порт 9292 на входящие подключения из вне:
gcloud compute firewall-rules create default-puma-server \
    --action allow \
    --direction ingress \
    --rules tcp:9292 \
    --source-ranges 0.0.0.0/0 \
    --target-tags puma-server

#----------------------------------------------------------------------------
