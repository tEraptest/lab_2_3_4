# Для показа Lab 3 (Jenkins)
## Показать что Jenkins запущен
docker ps | findstr jenkins
## Открыть в браузере
start http://localhost:8080
## В браузере показываешь:
- Dashboard с job lab_2_3_4
- Последний успешный билд
- Console Output с логами сборки
- Запущенные контейнеры через docker ps

# Для показа Lab 4 (Kubernetes)
## Запустить Minikube если не запущен
minikube start --driver=docker
## Показать что кластер работает
kubectl get nodes
## Показать запущенные поды
kubectl get pods
## Показать сервисы
kubectl get services
## Показать все сразу
kubectl get all

# Порядок действий перед защитой
## 1. Запустить Jenkins
docker start jenkins
## 2. Запустить Minikube
minikube start --driver=docker
## 3. Проверить всё
docker ps
kubectl get nodes