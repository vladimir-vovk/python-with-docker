Files description:
Описание файлов:
- docker-compose.yml
  Configuration for all docker containers used in your application.

  Файл для запуска всех сервисов (контейнеров) нужных для разработки (деплоя).

- Dockerfile
  Configuration for your python app docker container.

  Описание контейнера вашего python приложения.

Docker must be installed on your local machine, virtual machine or remote server. 
If you run docker on virtual machine or remote server you need to setup you environment.

Docker должн быть установлен на хостовой машине, виртуальной машине или удаленном сервере.
Если docker установлен в виртуальной машине или на удаленном сервере, требуется настройка окружения.
```
docker-machine ls
eval $(docker-machine env <docker_machine_name>)
```

1. Copy all files (docker folder and docker-compose.yml) to your project folder.

   Скопируйте все файлы в папку вашего проекта (папку docker и docker-compose.yml).

2. To download all images and build your python app image run this command from project root folder 
   (folder with docker-compose.yml file)

   Для сборки образов контейнеров запускаем из корня проекта (там где docker-compose.yml):
```
docker-compose build
```

3. Simple way to run you app:

   Запускаем контейнеры и приложение:
```
docker-compose up

# use -d key to run in detached mode (in background)
docker-compose up -d
```

4. 'docker-compose run' command very usefull for development. 

   Для разработки часто удобнее использовать 'docker-compose run'.
```
# all containers listed in docker-compose file will be automatically started
# автоматически запустятся все контейнеры от которых завист app (postgres и другие)
docker-compose run --service-ports app bash

# now you can use this bash session same as usual
# в запустившемся bash можно работать с проектом, так же как работаем локально
ipython
python manage.py runserver 0.0.0.0:8000

# you can run commands in your app's container
# можно сразу запускать команды в контейнере
docker-compose run django bash -c "python manage.py migrate"

# for example run tests
docker-compose run django python manage.py test --settings=project.settings.dev
```

5. Use 'docker exec -ti' if you need to connect to existing running container.

   Чтобы подключиться к запущенному контейнеру используем 'docker exec -it':
```
# connect to running container (for example, run ipython there)
# first find django container name or id with:
docker ps

# then exec bash in running container
docker exec -it <container name or id> bash

# now we inside running container, just run what you need
python manage.py shell_plus
```
