# Sprint Cloud

## Integrantes

| Nome                   |   RM   |
| :--------------------- | :----: |
| Otavio Miklos Nogueira | 554513 |
| Luciayla Yumi Kawakami | 557987 |

---

### Projeto .NET API

#### Descrição

O projeto é uma api rest implementada em .NET conectada com o banco de dados da Oracle, permitindo assim o CRUD completo das entidades Filial e Area, onde cada filial pode ter várias áreas designadas para diferentes situações e status de motos, melhorando assim a organização geral do pátio

#### Rotas

URL Base -> **http://localhost:5115/**

##### Filiais

| Método | Rota | Query | Descrição |
| :----: | :--- | :---: | :-------- |
| POST   | [/api/filial](localhost:5115/api/filial) | x | Cria uma nova instância de filial |
| GET    | [/api/filial](localhost:5115/api/filial) | x | Retorna todas as filiais |
| GET    | [/api/filial/{id}](localhost:5115/api/filial/1) | x | Retorna a filial com o id fornecido |
| GET    | [/api/filial/search](localhost:5115/api/filial/search?nome=Filial1) | nome: string | Retorna todas as filiais que tem o nome passado na query |
| PUT    | [/api/filial/{id}](localhost:5115/api/filial/1) | x | Atualiza a filial com o id fornecido |
| DELETE | [/api/filial/{id}](localhost:5115/api/filial/1) | x | Deleta a filial com o id fornecido |

###### JSON de uma filial

```javascript
{
    "Nome": string,
    "Endereco": string
}
```

##### Areas

| Método | Rota | Query | Descrição |
| :----: | :--- | :---: | :-------- |
| POST   | [/api/area](localhost:5115/api/area) | x | Cria uma nova instância de area |
| GET    | [/api/area](localhost:5115/api/area) | x | Retorna todas as areas |
| GET    | [/api/area/{id}](localhost:5115/api/area/1) | x | Retorna a area com o id fornecido |
| GET    | [/api/area/search](localhost:5115/api/area/search?filial=Osasco&status=Conserto) | filial: string, status: string | Retorna todas as areas que pertencem a filial e que possuem o mesmo status das queries |
| PUT    | [/api/area/{id}](localhost:5115/api/area/1) | x | Atualiza a area com o id fornecido |
| DELETE | [/api/area/{id}](localhost:5115/api/area/1) | x | Deleta a area com o id fornecido |

###### JSON de uma area

```javascript
{
    "Status": string,
    "FilialId": number
}
```

#### Instalação

1. Clone o repositório `git clone https://github.com/omininola/sprint1_dotnet.git`
2. Entre na pasta do projeto `cd sprint1_dotnet\webapi`
3. Rode o comando `dotnet restore`
4. E por fim rode o projeto `dotnet run` 

---

## Dockerfile

```Dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER app
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["webapi.csproj", "."]
RUN dotnet restore "./webapi.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "./webapi.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./webapi.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "webapi.dll"]
```

## Azure CLI

### Criação da VM

```bash

```

### Abertura de portas

```bash

```