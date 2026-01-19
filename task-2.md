### Подготовка работы с docker - запуск colima:

```bash
$ colima status

> FATA[0000] colima is not running
```

```bash
$ colima start

> INFO[0001] starting colima                              
  INFO[0001] runtime: docker                              
  INFO[0002] starting ...                                  context=vm
  INFO[0019] provisioning ...                              context=docker
  INFO[0021] starting ...                                  context=docker
  INFO[0022] done
```

### 1. Загрузите образ node версии 22.22:

```bash
$ docker pull node:22.22

> 22.22: Pulling from library/node
  4925cf9d8be8: Pull complete 
  a6174c95fe74: Pull complete 
  c1be109a62df: Pull complete 
  737aff54b157: Pull complete 
  fd1872fa12cc: Pull complete 
  64538a062a61: Pull complete 
  5e9e90c62a56: Pull complete 
  357cb6974fa0: Pull complete 
  Digest: sha256:cd7bcd2e7a1e6f72052feb023c7f6b722205d3fcab7bbcbd2d1bfdab10b1e935
  Status: Downloaded newer image for node:22.22
  docker.io/library/node:22.22
```

### 2. Запустите контейнер node в интерактивном режиме подключения терминала, поименуйте его mynode, передайте две переменные среды NAME=<ваше имя> и SURNAME=<ваша фамилия>:

```bash
$ docker run --name mynode -it --rm -e NAME=Severus -e SURNAME=Snape node:22.22 node

> Welcome to Node.js v22.22.0.
  Type ".help" for more information.
  >
```

### 3. В интерактивной среде выполнения node выполните скрипт, который выведет на экран приветствие: Привет, <ваше имя> <ваша фамилия>!, эти данные должны быть получены из переменных среды:

```bash
$ console.log(`Привет, ${process.env.NAME} ${process.env.SURNAME}!`)

> Привет, Severus Snape!
  undefined
  >
```

### 4. Остановите контейнер:

```bash
$ docker stop mynode

> mynode
```

### 5. Удалите образ node версии 22.22:

```bash
$ docker rmi node:22.22

> Untagged: node:22.22
  Deleted: sha256:cd7bcd2e7a1e6f72052feb023c7f6b722205d3fcab7bbcbd2d1bfdab10b1e935
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
  INFO[0001] stopping ...                                  context=vm
  INFO[0004] done  
```
