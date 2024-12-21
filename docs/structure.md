# Project structure

```
├── /src
│   ├── /Tradutube.Api                   # API Project (C# ASP.NET Core)
│   │   ├── /Controllers                 # Controllers da API
│   │   ├── /Models                      # Modelos de dados da API
│   │   ├── /DTOs                        # Data Transfer Objects
│   │   ├── /Services                    # Lógica de negócios (serviços)
│   │   ├── /Validators                  # Validações de entrada (ex. Model State)
│   │   ├── /Helpers                     # Funções auxiliares, classes utilitárias
│   │   ├── /Filters                     # Filtros para interceptar requisições
│   │   ├── /Configurations              # Configurações específicas da API (ex. middleware)
│   │   └── /Properties                  # Arquivos de configuração (ex. appsettings.json)
│   │
│   ├── /Tradutube.Application           # Aplicação: lógica de negócios
│   │   ├── /Interfaces                  # Interfaces de serviços
│   │   ├── /Services                    # Implementações de serviços (TTS, Tradução, etc.)
│   │   └── /DTOs                        # Transferência de dados entre a API e a aplicação
│   │
│   ├── /Tradutube.Domain                # Camada de domínio (entidades e regras de negócio)
│   │   ├── /Entities                    # Entidades (ex. Video, Translation, User)
│   │   ├── /ValueObjects                # Objetos de valor (ex. URL, Idioma)
│   │   └── /Enums                       # Enumerações usadas nas entidades
│   │
│   ├── /Tradutube.Infrastructure        # Camada de Infraestrutura (conexões com banco, serviços externos)
│   │   ├── /Repositories                # Repositórios para persistência de dados
│   │   ├── /Data                        # Configurações de banco de dados (contexto, migrações)
│   │   └── /ExternalServices            # Integrações com serviços externos (YouTube API, TTS, etc.)
│   │
│   └── /Tradutube.Tests                 # Camada de Testes
│       ├── /UnitTests                   # Testes unitários
│       ├── /IntegrationTests            # Testes de integração
│       └── /MockData                    # Dados falsos para testes
│
├── /docs                                # Documentação do projeto
│   └── arquitetura.md                   # Documento com a arquitetura do sistema
│
├── /scripts                             # Scripts auxiliares (ex. deployment)
│   ├── /docker                          # Arquivos para contêineres Docker
│   └── /ci-cd                           # Scripts de CI/CD
│
└── /README.md                          # Descrição geral do projeto
```

## Description

```
    +---------------------------+-----------------------------------------------------------------------+
    |         Folders           |                          Responsability                               |
    +---------------------------+-----------------------------------------------------------------------+
    |                           | Contém a camada de API, onde estão os Controllers, modelos para       |
    |      Tradutube.Api        | entrada/ saída dedados (DTOs), e serviços que fazem a conexão com as  |  
    |                           | funcionalidades  da aplicação                                         |
    |---------------------------|-----------------------------------------------------------------------|
    |-> Controllers             | Controladores que lidam com as requisições HTTP                       |
    |---------------------------|-----------------------------------------------------------------------|
    |-> Models                  | Modelos que representam a entrada e saída de dados                    |
    |---------------------------|-----------------------------------------------------------------------|
    |-> Services                | Lógica de negócios que processa a requisição                          |
    |---------------------------|-----------------------------------------------------------------------+
    |-> Validators              | Validação dos dados recebidos via requisições                         |
    |---------------------------|-----------------------------------------------------------------------|
    |-> Helpers                 | Funções auxiliares como conversores, validadores genéricos, etc.      |
    |---------------------------|-----------------------------------------------------------------------|
    |-> DTOs                    | Objectos de transferência de Dados usados para comunicar entre API    |
    |                           | e aplicação                                                           |
    |---------------------------|-----------------------------------------------------------------------|
    |---------------------------|-----------------------------------------------------------------------|
    |                           | Lógica de negócios centralizada. Aqui ficam os serviços               |
    |   Tradutube.Application   | que implementam as regras de negócio do sistema, como a               |
    |                           | tradução, transcrição, etc.                                           |
    |---------------------------|-----------------------------------------------------------------------|
    |-> Services                | Implementações dos serviços de tradução, etc.                         |
    |---------------------------|-----------------------------------------------------------------------|
    |-> DTOs                    | Tranferência de dados entre aplicação e API                           |
    |---------------------------|-----------------------------------------------------------------------|
    |-> Interfaces              | Interfaces de serviços para garantir que a aplicação siga             |
    |                           | o princípio da inversão de dependência.                               |
    |---------------------------|-----------------------------------------------------------------------|
    |---------------------------|-----------------------------------------------------------------------|
    |                           | Camada de domínio com as entidades e regras de negócio                |
    |    Tradutube.Domain       | Aqui ficam os modelos principais do sistema                           |
    |                           |                                                                       |
    |---------------------------|-----------------------------------------------------------------------|
    |-> Entities                | Entidades do domínio (ex. Vídeo, Usuáio, Tradução)                    |
    |---------------------------|-----------------------------------------------------------------------|
    |-> ValueObjects            | Objectos que representam valores imutávies (eg. Idioma, URL)          |
    |---------------------------|-----------------------------------------------------------------------|
    |-> Enums                   | Enumeração utilizadas pelas entidades                                 |
    |---------------------------|-----------------------------------------------------------------------|
    |---------------------------|-----------------------------------------------------------------------|
    |                           | Conexões com a infraestrutura, como banco de dados                    |
    | Tradutube.Infrastructure  | e serviços externos (APIs, TTS, etc.)                                 |
    |                           |                                                                       |
    |---------------------------|-----------------------------------------------------------------------|
    |-> Repositories            | Implementações de repositórios para interação com o banco de dados    |
    |---------------------------|-----------------------------------------------------------------------|
    |-> Data                    | Configurações de banco de dados, como contexto e migrações            |
    |---------------------------|-----------------------------------------------------------------------|
    |-> ExternalServices        | Integrações com serviços externos (ex. YouTube API, TTS)              |
    |---------------------------|-----------------------------------------------------------------------|
    |---------------------------|-----------------------------------------------------------------------|
    |                           |                                                                       |
    |   Tradutube.Tests         |  Contém os testes automatizados do sistema                            |
    |                           |                                                                       |
    |---------------------------|-----------------------------------------------------------------------|
    |-> UnitTests               | Testes unitários, verificando componentes isolados                    |
    |---------------------------|-----------------------------------------------------------------------|
    |-> IntegrationTests        | Testes de integração para verificar o funcionamento entre as camadas  |
    |---------------------------|-----------------------------------------------------------------------|
    |-> MockData                | Dados simulados para testar as funcionalidades do sistema             |
    |---------------------------|-----------------------------------------------------------------------|
    |---------------------------|-----------------------------------------------------------------------|
    |                           | Documentação do projeto. Ex.: Arquivo com a arquitetura do            |
    |      /docs                | sistema, fluxos de trabalho, diagramas e informações                  |
    |                           | importantes para desenvolvimento e manutenção.                        |
    |---------------------------|-----------------------------------------------------------------------|
    |---------------------------|-----------------------------------------------------------------------|
    |                           | Scripts auxiliares para deployment, Docker, e CI/CD para              |
    |     /scripts              | configurar containers Docker ou pipelines de CI/CD.                   |
    |                           |                                                                       |
    |---------------------------|-----------------------------------------------------------------------|
    |---------------------------|-----------------------------------------------------------------------|
``` 






