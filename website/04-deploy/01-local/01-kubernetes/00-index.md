---
layout: page
title: Deploy Local Kubernetes
description: Deploy Local Kubernetes
keywords: Local Kubernetes, Deploy
permalink: /deploy/local/kubernetes/
---

# Deploy Local Kubernetes

<br/>

### 3 React проекта со скриптами для запуска и инструкциями по запуску в minikube

https://github.com/webmakaka/The-React-Practice-Course-Learn-by-Building-Projects

<br/>

### Предлагал развернуть js приложение (react/nodejs) в локальном Kubernetes кластере

Само приложение можно взять <a href="https://github.com/webmakaka/MERN-Stack-Front-To-Back-v2.0">здесь</a>

А kubernetes кластер поднимается скриптами и для его запуска, достаточно всего выполнить следующие <a href="https://sysadm.ru/devops/containers/kubernetes/kubeadm/vagrant-centos7-3-node-kubernetes-cluster/">инструкции</a>. Правда все это подготовлено для linux.

<br/>

Тем, кто хочет, но пока не знает, что это такое и с чего начать, рекомендую скачать/купить следующие материалы и <a href="/courses/en/">ознакомиться с ними</a>

Upd.  
Само приложение успешно развернулось в kubernetes кластере. Но есть проблемы при обращении к api серверу. С вероятностью ~50% ответ от сервера завершается ошибкой. Пробовал разные версии kubernetes. Менял flannel на calico. Вроде как такая ошибка возникает при использовании vitualbox.

Upd.
Попробовал развернуть <a href="https://github.com/webmakaka/MERN-Stack-Front-To-Back-v2.0/">следующее приложение</a> в minikube. Тоже проблемы. Буду незвозмездно благодарен за помощь в ее решении.
