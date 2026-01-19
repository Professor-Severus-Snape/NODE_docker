### Подготовка работы с docker - запуск colima:

```bash
$ colima status

> FATA[0001] colima is not running
```

```bash
$ colima start

> INFO[0001] starting colima                              
  INFO[0001] runtime: docker                              
  INFO[0002] starting ...                                  context=vm
  INFO[0018] provisioning ...                              context=docker
  INFO[0019] starting ...                                  context=docker
  INFO[0021] done
```

### 1. Загрузите образ busybox последней версии:

```bash
$ docker pull busybox

> Using default tag: latest
  latest: Pulling from library/busybox
  e59838ecfec5: Pull complete 
  Digest: sha256:2383baad1860bbe9d8a7a843775048fd07d8afe292b94bd876df64a69aae7cb1
  Status: Downloaded newer image for busybox:latest
  docker.io/library/busybox:latest
```

### 2. Запустите новый контейнер busybox с командой ping сайта netology.ru и количеством пингов 7, поименуйте контейнер pinger:

```bash
$ docker run --name pinger busybox ping -c 7 netology.ru

> PING netology.ru (51.250.51.8): 56 data bytes
  64 bytes from 51.250.51.8: seq=0 ttl=63 time=0.271 ms
  64 bytes from 51.250.51.8: seq=1 ttl=63 time=0.562 ms
  64 bytes from 51.250.51.8: seq=2 ttl=63 time=0.701 ms
  64 bytes from 51.250.51.8: seq=3 ttl=63 time=0.852 ms
  64 bytes from 51.250.51.8: seq=4 ttl=63 time=0.841 ms
  64 bytes from 51.250.51.8: seq=5 ttl=63 time=0.808 ms
  64 bytes from 51.250.51.8: seq=6 ttl=63 time=0.854 ms

  --- netology.ru ping statistics ---
  7 packets transmitted, 7 packets received, 0% packet loss
  round-trip min/avg/max = 0.271/0.698/0.854 ms
```

### 3. Выведите на экран список всех контейнеров - запущенных и остановленных:

```bash
$ docker ps -a

> CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                      PORTS     NAMES
  474f5d845b26   busybox   "ping -c 7 netology.…"   36 seconds ago   Exited (0) 29 seconds ago             pinger
```

### 4. Выведите на экран логи контейнера с именем pinger:

```bash
$ docker logs pinger

> PING netology.ru (51.250.51.8): 56 data bytes
  64 bytes from 51.250.51.8: seq=0 ttl=63 time=0.271 ms
  64 bytes from 51.250.51.8: seq=1 ttl=63 time=0.562 ms
  64 bytes from 51.250.51.8: seq=2 ttl=63 time=0.701 ms
  64 bytes from 51.250.51.8: seq=3 ttl=63 time=0.852 ms
  64 bytes from 51.250.51.8: seq=4 ttl=63 time=0.841 ms
  64 bytes from 51.250.51.8: seq=5 ttl=63 time=0.808 ms
  64 bytes from 51.250.51.8: seq=6 ttl=63 time=0.854 ms

  --- netology.ru ping statistics ---
  7 packets transmitted, 7 packets received, 0% packet loss
  round-trip min/avg/max = 0.271/0.698/0.854 ms
```

### 5. Запустите второй раз контейнер с именем pinger:

```bash
$ docker start pinger

> pinger
```

### 6. Выведите на экран список всех контейнеров - запущенных и остановленных:

```bash
$ docker ps -a

> CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS                      PORTS     NAMES
  474f5d845b26   busybox   "ping -c 7 netology.…"   5 minutes ago   Exited (0) 11 seconds ago             pinger
```

### 7. Выведите на экран логи контейнера с именем pinger:

```bash
$ docker logs pinger

> PING netology.ru (51.250.51.8): 56 data bytes
  64 bytes from 51.250.51.8: seq=0 ttl=63 time=0.271 ms
  64 bytes from 51.250.51.8: seq=1 ttl=63 time=0.562 ms
  64 bytes from 51.250.51.8: seq=2 ttl=63 time=0.701 ms
  64 bytes from 51.250.51.8: seq=3 ttl=63 time=0.852 ms
  64 bytes from 51.250.51.8: seq=4 ttl=63 time=0.841 ms
  64 bytes from 51.250.51.8: seq=5 ttl=63 time=0.808 ms
  64 bytes from 51.250.51.8: seq=6 ttl=63 time=0.854 ms

  --- netology.ru ping statistics ---
  7 packets transmitted, 7 packets received, 0% packet loss
  round-trip min/avg/max = 0.271/0.698/0.854 ms

  PING netology.ru (51.250.51.8): 56 data bytes
  64 bytes from 51.250.51.8: seq=0 ttl=63 time=0.326 ms
  64 bytes from 51.250.51.8: seq=1 ttl=63 time=0.521 ms
  64 bytes from 51.250.51.8: seq=2 ttl=63 time=0.505 ms
  64 bytes from 51.250.51.8: seq=3 ttl=63 time=0.515 ms
  64 bytes from 51.250.51.8: seq=4 ttl=63 time=0.457 ms
  64 bytes from 51.250.51.8: seq=5 ttl=63 time=0.488 ms
  64 bytes from 51.250.51.8: seq=6 ttl=63 time=0.533 ms

  --- netology.ru ping statistics ---
  7 packets transmitted, 7 packets received, 0% packet loss
  round-trip min/avg/max = 0.326/0.477/0.533 ms
```

### 8. Определите по логам общее количество запусков команды ping и какое общее количество отправленых запросов:

```bash
количество запусков команды ping — 2
количество отправленных запросов — 14
```

### 9. Удалите контейнер с именем pinger:

```bash
$ docker rm pinger

> pinger
```

### 10. Удалите образ busybox:

```bash
$ docker rmi busybox

> Untagged: busybox:latest
  Deleted: sha256:2383baad1860bbe9d8a7a843775048fd07d8afe292b94bd876df64a69aae7cb1
```

### Завершение работы с docker - остановка colima:

```bash
$ colima status

> INFO[0000] colima is running using macOS Virtualization.Framework 
  INFO[0000] arch: x86_64                                 
  INFO[0000] runtime: docker                              
  INFO[0000] mountType: virtiofs                          
  INFO[0000] docker socket: unix:///Users/juliafokanova/.colima/default/docker.sock 
  INFO[0000] containerd socket: unix:///Users/juliafokanova/.colima/default/containerd.sock 
```

```bash
$ colima stop

> INFO[0000] stopping colima                              
  INFO[0000] stopping ...                                  context=docker
  INFO[0000] stopping ...                                  context=vm
  INFO[0003] done   
```