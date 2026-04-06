# Установка jenkins
docker run -d --name jenkins --restart=on-failure -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home -v //var/run/docker.sock:/var/run/docker.sock jenkins/jenkins:lts
# Получение пароля для jenkins 
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
# Удаление контейнеров jenkins
docker rm -f jenkins
# Открыть jenkins в браузере
http://localhost:8080
# Посмотреть логи в jenkins 
docker logs jenkins
# Найти только пароль
docker logs jenkins 2>&1 | Select-String "password"
# Перазапустить контейнер
docker restart jenkins
# Зайти внутрь как root в docker
docker exec -u root -it jenkins bash
# Выход из root
exit
# Исправление прав на Docker socket
docker exec -u root jenkins chmod 666 /var/run/docker.sock










# Если сломалась Lab 3 — перезапуск Jenkins
## Удалить контейнеры
docker rm -f jenkins service_1 service_2 gateway
docker network rm lab2-net

## Запустить Jenkins
docker run -d --name jenkins --restart=on-failure -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home -v //var/run/docker.sock:/var/run/docker.sock jenkins/jenkins:lts

## Дать права на Docker
docker exec -u root jenkins chmod 666 /var/run/docker.sock

- Открыть http://localhost:8080 → Build Now

# Если не знаешь что делать пиши это как только запустил jenkins
docker exec -u root jenkins bash -c "apt-get update && apt-get install -y docker.io && curl -SL https://github.com/docker/compose/releases/download/v2.24.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose && chmod +x /usr/local/bin/docker-compose && chmod 666 /var/run/docker.sock"