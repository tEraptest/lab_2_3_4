# Установка миникуб
winget install Kubernetes.minikube
# Установить kubectl
winget install Kubernetes.kubectl
# Запустить Minikube
minikube start --driver=docker
# Проверить что работает
minikube status
kubectl get nodes
# Загрузка image в minikube
minikube image load service_1-service_1:latest
minikube image load service_2-service_2:latest
minikube image load gateway-gateway:latest
# применить YAML файл (задеплоить всё в Kubernetes)
kubectl apply -f lab4/deployment.yaml
# проверить что поды запустились:
kubectl get pods
# Просмотреть все загруженные файлы images 
docker images
# Теперь проверь сервисы и открой gateway в браузере
kubectl get services
# И открой gateway
minikube service gateway







# Если сломалась Lab 4 — перезапуск Kubernetes
## Удалить деплой
kubectl delete -f lab4/deployment.yaml

## Если Minikube не работает
minikube delete
minikube start --driver=docker

## Загрузить образы
minikube image load service_1-service_1:latest
minikube image load service_2-service_2:latest
minikube image load gateway-gateway:latest

## Задеплоить снова
kubectl apply -f lab4/deployment.yaml

## Открыть в браузере
minikube service gateway

# Порты для проверки 
http://127.0.0.1:60761/api/service-1/
http://127.0.0.1:60761/api/service-2/