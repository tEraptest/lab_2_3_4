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