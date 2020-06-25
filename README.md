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

### Docker Networking
```sh
docker network ls 

docker network inspect bridg

docker inspect c1 | grep IP
```
### Mapeamento de portas 


```sh

docker run -d --name c1_apache -p 9090:80 httpd

obs: a primeira porta é a do host e a segunda do container.
```

### Para saber a porta em que o container está rodando 
 ```sh
 docker port C2_apache
 ```

 ### Persistencia de dados em container e volumes.

 As camadas do container tem a capacidade de escrita e leitura,porém nao tem a capacidade de persistencia de dados, ou seja , se o container morrer ,automaticamente perdermos os dados.
 Os container utilizam sistemas de storage drivers para armazenamento dos dados.

 Tipos de persistência de dados.

 - Bind Mount - Constitui um mapeamento direto no fylesystem do host.Basicamente e criar uma pasta no host e mapear pro container.
 - Volume - Tambem se vale de uma aréa especifica do host .
 - Tmpfs -Persistencia de dados em memoria ram,valido somente para servidores linux.

exemplo com Bind Mount : docker run -itd --name apache -p 9090:80 -v /home/wilsonqueiroz/site:/usr/local/apache2/htdocs httpd:2.4 ,e possivel ter multiplos mapeamentos.

<b>Docker Volume</b>

- volume entre o host e o hospedeiro
- completamente gerenciado pelo Docker - não diretamente  no host;
- uso em produção;
- menos simples porém mais seguros.
- arquivos de origem não "sobrescrevem" dados destino (container);
- criptografia de conteudo,por exemplo;
- dados manipulados por docker cli;
- volume plugins drivers: local,NFS,CIFS,Cluster,SSHFS   

exemplo: Criação do volume : docker volume create vol-web
         Listagem de volume : docker volume ls

ex: docker run -d --name apache_vol -p 9091:80 -v /etc/localtime:/etc/localtime:ro -v vol-web:/usr/local/apache2/htdocs httpd:2.4


### <b>Docker e Microserviços.</b>

<p>Microserviços é conceito onde a aplicação e divida em partes utilizando na maioria das vezes containers.</p>
<p>Nas arquiteturas de serviços convencionais ou Monoloticas a aplicação fica toda em uma unica stack e compartilha recursos de processamentos.Isso causa uma dependencia da linguagem e dos serviços.Outro contra e qunato mais a aplicação cresce mais complexa ela fica e maior o acoplamento e dependencia dela.</p>
<p>A escalabilidade e reduzida,pois eu preciso replicar o monolito completo,e se por acaso faltar algum recurso ,ele faltaria em toda a aplicação.</p>
<p>No caso dos microserviços a aplicação monolitica deixa de existir e eu começo a trabalhar com a componetização via serviços (multi-stack).<p>
<p> Nesse modelo os serviços são pequenos e com deployment independentes e não acoplados,a manutenção e facilitada e a também a sua atualização.Alem disso ele apresenta uma maior resiliencia e flexibilidade </p>

