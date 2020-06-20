 ### Curso Docker do Basico ao Avançado!

 
 
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