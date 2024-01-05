### Você provavelmente já pensou em usar o Postgres em um container Docker, mas e o PGAdmin? Que tal usar os dois juntos? Neste repositório, te ensino como subir uma instância de cada um dos serviços e fazer os containers conversarem entre si!

# Docker Network 

Antes de tudo, você precisa criar uma network para que os containers consigam se cominuar. <br>
Abra seu terminal e execute o seguinte comando:

```
docker network create --driver bridge my-network
```
> [!NOTE]
> O `my-network` será o nome da sua rede, mas você pode mudar caso necessário.

<br>

Agora verifique se a rede foi criada com sucesso:

```
docker network ls
```

# Docker Container

O proximo passo agora é criar os contâiners rodando a aplicação. Execute o seguinte comando para subir o servidor postgres:

<br>

```
docker container run -d --name my-postgres --network=my-network -p 5432:5432 -e POSTGRES_PASSWORD=postgres postgres
```

> [!NOTE]
> No `--name` você coloca o nome do contâiner de sua preferência, no `--network=` depois do simbolo de igualdade, você coloca o nome da rede que foi criado anteriormente.
>
> O `-e` são variáveis de ambientes como `POSTGRES_PASSWORD ou POSTGRES_USER`,podendo mudá-las conforme necessário.

<br>

**Agora você deve subir o PGAdmin:**

```
docker container run -d --name my-pgadmin --network=my-network -p 8080:80  -e PGADMIN_DEFAULT_EMAIL=teste@gmail.com -e PGADMIN_DEFAULT_PASSWORD=postgres dpage/pgadmin4
```

> [!IMPORTANT]
> O PGAdmin é uma aplicação WEB, por isso ele roda na porta 80, mas podendo ser mapeado em qualquer porta do PC.

<br>

Verifique se os contâiners foram criados com sucesso:

```
docker container ls
```

# Acessando o PGAdmin

O proximo passo é acessar seu PGAdmin, abra seu navegador e coloque o seguinte link:

```
localhost:8080
```
> Depois dos dois pontos, coloque a porta que você mapeou no container para acessá-lo

Em seguida faça o login e acesse seu PostgreSever

 <img width=100% src="https://github.com/ksilva-kwn/postgre-pgadmin-docker/blob/main/Fotos-Postgre/Captura%20de%20tela%202024-01-05%20152626.png"/>

 Depois de Fazer o Login acesse seu servidor Postgres:

 <img width=100% src="https://github.com/ksilva-kwn/postgre-pgadmin-docker/blob/main/Fotos-Postgre/Captura%20de%20tela%202024-01-05%20152709.png"/>

> [!IMPORTANT]
> Em seguida Clique com o botão direito em `Servers` depois em `register` e em seguida `Server`
>
> Depois insira um nome para seu Banco de Dados

<img width=100% src="https://github.com/ksilva-kwn/postgre-pgadmin-docker/blob/main/Fotos-Postgre/Captura%20de%20tela%202024-01-05%20153323.png"/>

Agora clique em `Connection` e coloque as variáveis de ambiente.

> [!NOTE]
> Host name/address = `Nome do container` <br>
> Port = `Porta padrão do BD` <br>
> Username = `Nome de usuário que você configurou (por padrão ela vem como "postgres") ` <br>
> Password = `Senha que você configurou` 

<img width=100% src="https://github.com/ksilva-kwn/postgre-pgadmin-docker/blob/main/Fotos-Postgre/Captura%20de%20tela%202024-01-05%20153514.png"/>

Em seguida salve e você ja estará acessando o BD.

<img width=100% src="https://github.com/ksilva-kwn/postgre-pgadmin-docker/blob/main/Fotos-Postgre/Captura%20de%20tela%202024-01-05%20154716.png"/>
