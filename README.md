 ### Curso Docker do Basico ao Avançado!

 
 #### Fazer um build de imagem  

```sh
 docker build 
```
ex: docker build . --tag wilsondevops/missaodevops:1.0

 #### Baixar uma imagem para a maquina local  

```sh
 docker pull [image]
```
ex: docker pull  uzyexe/nmap

 #### Subir a imagem para um docker hub  

```sh
 docker push  
```
ex: docker push wilsondevops/missaodevops:1.0


 #### Listar as imagens na minha maquina 

```sh
 docker images 
```

#### Excluir imagens listadas

```sh
 docker rmi <imagTag>
```


#### Listar containers rodando

```sh
 docker ps 
```

#### Listar todos containers 

```sh
 docker ps -a

```

#### Rodar container  

```sh
 docker run [options][image*][comand][args]

 ex: docker run --rm -it ubuntu:18.04
 ex:  docker run -it --name nmap-container uzyexe/nmap -sS google.com (rodando nmap no host google.com)
 
```
- -i =  iniciar container com interação
- -t = iniciar um terminal 
- -d = container em segundo plano 
- -rm = elimina o container ao terminar 
- --name = atribui um nome ao container

#### Parar um container 

```sh
 docker stop [container id]
```
### Hibernar um container

```sh
 docker pause [container id]
```

### Startar um container

```sh
 docker start [container id]
```
### Remover um container

```sh
 docker rm  [container id]
```
## Remover todos os containers parados 

```sh
 docker rm  [container id]
```
### Inspecionar um container 

```sh
docker inspect [container name] | grep I clemage
```

### Pegar os logs do container.

```sh
docker logs [container name] | grep I clemage
```
### Entra no container .
obs: após sair usando exit do container ele entra em estado de hibernação,para sair sem matar o container utilizar o ctrl pq
```sh
docker attach [container name] 
```
### Entra no container em execução.

```sh
docker exec [container name]
ex: docker exec teste ps aux 
    docker exec -d 3985 touch /tmp/aula03
    docker exec -it 3985 bash
```
### Copia arquivos do container para o host e ao contrario
```sh
docker cp  [container name]:dir/arquivo .
```
obs: utilizando o ponto ele copia para o diretorio atual.


### Fazer exportação do container no seu estado atual como .tar

```sh
docker export [ container name ] | gzip > export_container.tar.gz
```

### Fazer importação do container no seu estado atual como .tar

```sh
zcat export_container  | docker import - export_novo
```
obs:Quando faço a importação do container ele é importado como imagem,então ele passa a ser manipulado como imagem 
por exemplo criar novamente com docker run e no final passar a razão dele existir,por exemplo usando o bash.

### Fazer importação da imagem  no seu estado atual como .tar

```sh
  docker save ubuntu | gzip -c > IMAGE.tar.gz
```
### Fazer exportação da imagem  no seu estado atual como .tar

```sh
  docker load < IMAGEM.tar.gz
```


