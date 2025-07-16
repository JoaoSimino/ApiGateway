# ApiGateway
[![Build Status](https://github.com/JoaoSimino/ApiGateway/actions/workflows/ci-cd.yml/badge.svg)](https://github.com/JoaoSimino/ApiGateway/actions/workflows/ci-cd.yml)


## Sumário

- [Descrição](#descrição)
- [Arquitetura e Tecnologias](#arquitetura-e-tecnologias)
- [Funcionalidades](#funcionalidades)
- [Pré-requisitos](#pré-requisitos)
- [Como rodar](#como-rodar)
- [Testes](#testes)
- [Documentação da API](#documentação-da-api)
- [Contribuindo](#contribuindo)
- [Pipeline CI/CD](#pipeline-cicd)
- [Licença](#licença)

## Descrição

ApiGateway é um gateway reverso criado com o YARP (Yet Another Reverse Proxy) no .NET 9. Seu objetivo é unificar e gerenciar o roteamento de requisições para os microsserviços de crédito e faturamento do sistema, servindo como único ponto de entrada (BFF - Backend for Frontend) para o frontend Angular e demais consumidores.

O projeto organiza e encapsula a comunicação entre os serviços CreditScoringEngine e BillingService, simplificando integrações e permitindo rotas limpas e segregadas, inclusive para as documentações Swagger de cada serviço.

## Arquitetura e Tecnologias
- .NET 9 com Minimal APIs

- YARP (Yet Another Reverse Proxy) como engine de roteamento reverso

- Configuração via appsettings.json

- Clean setup voltado para ambientes de microserviços

- GitHub Actions para CI/CD

- Docker para containerização

## Funcionalidades

- Roteamento automático e transparente para os serviços backend:

- CreditScoringEngine:
    - /api/Cliente/**
    - /api/Proposta/**

- BillingService:
    - /api/PropostaAprovada/**
    - /api/Fatura/**
    - /api/Parcelas/**

- Documentação unificada via proxy dos Swaggers dos serviços backend

- Configuração extensível e customizável via ReverseProxy em appsettings.json

## Pré-requisitos

- .NET SDK 9.0 Preview ou superior (Download)

- Docker (opcional, para rodar em container)

- Visual Studio 2022 (versão com suporte ao .NET 9) ou VS Code com extensões C#

## Como rodar

Clone o repositório:

```bash
git clone https://github.com/JoaoSimino/ApiGateway.git
cd ApiGateway
```

Restaurar dependências e rodar a aplicação:

```bash
dotnet restore
dotnet run
```

A API estará disponível em `http://localhost:5000` (ou porta configurada).

## Testes

Para rodar todos os testes:

```bash
dotnet test ApiGateway.sln --configuration Release --verbosity normal
```

Os testes utilizam banco InMemory para isolamento total.

## Documentação da API

A API está configurada com Swagger UI para facilitar testes e visualização da documentação.  
Acesse `http://localhost:5000/swagger` após rodar a aplicação.

Exemplo de requisição curl para listar Clientes:

```bash
curl -X GET http://localhost:5000/api/Cliente
```

## Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. Fork este repositório
2. Crie uma branch feature com o padrão `feature/nome-da-feature`
3. Faça commits claros e descritivos
4. Abra um Pull Request detalhando as alterações

Por favor, siga o padrão de commits [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/).

## Pipeline CI/CD

O projeto utiliza GitHub Actions para:

- Validar o código a cada push/PR na branch `main`
- Executar testes automaticamente
- Buildar e preparar o pacote para release, e subir ja um container atualizar para o Docker hub. 

O workflow está disponível em `.github/workflows/ci-cd.yml`.

## Licença

Este projeto está licenciado sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

Obrigado por usar o ApiGateway!  
Para dúvidas ou sugestões, abra uma issue ou entre em contato comigo.