# Jenkins в Docker — шпаргалка

## Первый запуск

```bash
# 1. Запустить Jenkins
docker run -d --name jenkins --restart=on-failure -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home -v //var/run/docker.sock:/var/run/docker.sock jenkins/jenkins:lts

# 2. Установить Docker и docker-compose внутри Jenkins
docker exec -u root jenkins bash -c "apt-get update && apt-get install -y docker.io && curl -SL https://github.com/docker/compose/releases/download/v2.24.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose && chmod +x /usr/local/bin/docker-compose && chmod 666 /var/run/docker.sock"

# 3. Открыть в браузере
# http://localhost:8080
```

---

## Получить пароль для первого входа

```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
# или
docker logs jenkins 2>&1 | Select-String "password"
```

---

## Управление контейнером

```bash
docker start jenkins      # запустить
docker stop jenkins       # остановить
docker restart jenkins    # перезапустить
docker logs jenkins       # посмотреть логи
docker ps -a              # статус всех контейнеров
```

---

## Если что-то сломалось (полный сброс Lab 3)

```bash
# Удалить всё
docker rm -f jenkins service_1 service_2 gateway
docker network rm lab2-net

# Запустить Jenkins заново (шаги 1–2 из раздела "Первый запуск")
```

После этого открыть http://localhost:8080 → **Build Now**

---

## Разное

```bash
# Зайти внутрь контейнера как root
docker exec -u root -it jenkins bash

# Исправить права на Docker socket (если pipeline не видит Docker)
docker exec -u root jenkins chmod 666 /var/run/docker.sock

# Удалить контейнер Jenkins
docker rm -f jenkins
```










# Kubernetes (Minikube) — шпаргалка

## Установка (один раз)

```bash
winget install Kubernetes.minikube
winget install Kubernetes.kubectl
```

---

## Первый запуск

```bash
# 1. Запустить Minikube
minikube start --driver=docker

# 2. Проверить что работает
minikube status
kubectl get nodes

# 3. Загрузить образы в Minikube
minikube image load service_1-service_1:latest
minikube image load service_2-service_2:latest
minikube image load gateway-gateway:latest

# 4. Задеплоить всё
kubectl apply -f lab4/deployment.yaml

# 5. Проверить что поды запустились
kubectl get pods
kubectl get services

# 6. Открыть gateway в браузере
minikube service gateway
```

---

## Проверка эндпоинтов

```
http://127.0.0.1:<PORT>/api/service-1/
http://127.0.0.1:<PORT>/api/service-2/
```

> Порт узнать через `minikube service gateway`

---

## Если что-то сломалось (полный сброс)

```bash
# Удалить деплой
kubectl delete -f lab4/deployment.yaml

# Если Minikube не работает совсем
minikube delete
minikube start --driver=docker

# Загрузить образы и задеплоить заново (шаги 3–6 из раздела выше)
```