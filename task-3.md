### Подготовка работы с docker - запуск colima:

```bash
$ colima status

> FATA[0000] colima is not running
```

```bash
$ colima start

> INFO[0001] starting colima
  INFO[0001] runtime: docker                         
  INFO[0004] starting ...                                  context=vm
  INFO[0019] provisioning ...                              context=docker
  INFO[0022] starting ...                                  context=docker
  INFO[0023] done  
```

### 1. Загрузите образ node версии 22.22:

```bash
$ docker pull node:22.22

> 4925cf9d8be8: Pull complete
  5e9e90c62a56: Pull complete
  357cb6974fa0: Pull complete
  a6174c95fe74: Pull complete
  737aff54b157: Pull complete
  64538a062a61: Pull complete
  c1be109a62df: Pull complete
  fd1872fa12cc: Pull complete
  Digest: sha256:cd7bcd2e7a1e6f72052feb023c7f6b722205d3fcab7bbcbd2d1bfdab10b1e935
  Status: Downloaded newer image for node:22.22
  docker.io/library/node:22.22
```

### 2. Запустите контейнер с именем first_node из образа node версии 22.22 в фоновом режиме, подключив папку data из текущей директории в /var/first/data контейнера:

```bash
$ mkdir ./data && docker run --name first_node -d -v $(pwd)/data:/var/first/data node:22.22 sleep infinity

> 998e0d72a5f09369edbd61c05e82daa44de2b0f1511331e563ff7c7cd943c281
```

### 3. Запустите контейнер с именем second_node из образа node версии 22.22 в фоновом режиме, подключив папку data из текущей директории в /var/second/data контейнера:

```bash
$ docker run --name second_node -d -v $(pwd)/data:/var/second/data node:22.22 sleep infinity

> 7f39e4957b276008f41ce6bc05f01f756c4699dd6570b5ff1bb405e76db286ca
```

### 4. Подключитесь к контейнеру first_node с помощью exec и создайте текстовый файл любого содержания в /var/first/data:

```bash
$ docker exec -it first_node /bin/bash

  > root@998e0d72a5f0:/# touch /var/first/data/first-container.txt
  
  > root@998e0d72a5f0:/# cat > /var/first/data/first-container.txt <<EOF
    > Привет!
    > Это текстовый файл под названием first-container.txt.
    > Он был создан в первом контейнере, но после монтирования папок доступен будет и на хосте и во втором контейнере.
    > EOF
  
  > root@998e0d72a5f0:/# exit
  exit
```

### 5. Добавьте ещё один файл в папку data на хостовой машине:

```bash
$ echo 'Этот файл под названием host.txt был создан локально на хосте.' > $(pwd)/data/host.txt
```

### 6. Подключитесь к контейнеру second_node с помощью exec и получите список файлов в директории /var/second/data, выведите на экран содержимое файлов:

```bash
$ docker exec -it second_node /bin/bash

  > root@7f39e4957b27:/# ls var/second/data
  first-container.txt  host.txt

  > root@7f39e4957b27:/# cat /var/second/data/first-container.txt
  Привет!
  Это текстовый файл под названием first-container.txt.
  Он был создан в первом контейнере, но после монтирования папок доступен будет и на хосте и во втором контейнере.

  > root@7f39e4957b27:/# cat /var/second/data/host.txt
  Этот файл под названием host.txt был создан локально на хосте.

  > root@7f39e4957b27:/# exit
  exit
```

### 7. Остановите оба контейнера:

```bash
$ docker stop first_node second_node

> first_node
  second_node
```

### 8. Удалите оба контейнера:

```bash
$ docker rm first_node second_node

> first_node
  second_node
```

### 9. Удалите образ node версии 22.22:

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
  INFO[0003] done
```
