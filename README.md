# 🚀 Automação de API E2E - ServeRest

![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)
![Newman](https://img.shields.io/badge/Newman-000000?style=for-the-badge&logo=npm&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)

Este repositório contém uma suíte de testes E2E (End-to-End) de API, desenvolvida para validar fluxos complexos e regras de negócio utilizando a API do [ServeRest](https://serverest.dev/).

O foco deste projeto é demonstrar a arquitetura de testes contínuos (CI/CD) com **independência de dados**, garantindo que a esteira possa rodar infinitas vezes sem falhas por duplicidade ou sujeira no banco de dados.

## 🎯 Diferenciais Técnicos Aplicados
- **Massa de Dados Dinâmica:** Geração de emails e nomes de produtos em tempo de execução (`Date.now()`) para evitar falsos negativos por dados duplicados (Status 400).
- **Gestão de Tokens (Auth):** Extração, tratamento e armazenamento automático do *Bearer Token* durante o fluxo de login para uso nas requisições subsequentes.
- **Fluxo End-to-End Interligado:** O teste não apenas bate em rotas isoladas. Ele *Cria um usuário > Realiza o Login > Cria um Produto com o Token > Consulta o Produto para validar a integridade no banco de dados*.
- **Tratamento de Strings:** Limpeza de cabeçalhos de autorização nativos (`.replace()`) para evitar bloqueios de formatação de JWT.

## ⚙️ Pipeline CI/CD (GitHub Actions)
Este projeto possui integração contínua. Qualquer push para a `main` dispara a execução automatizada via **Newman**. 
O relatório visual detalhado da execução fica salvo como artefato e pode ser baixado em formato `.html` na aba [Actions](../../actions).

## 🚀 Como executar localmente

Para rodar os testes localmente e gerar o relatório HTML (htmlextra), certifique-se de ter o Node.js instalado e execute:

```bash
# Instale o Newman e o gerador de relatórios globalmente
npm install -g newman newman-reporter-htmlextra

# Execute a collection passando o Environment
newman run serverest-collection.json -e serverest-env.json -r htmlextra
```
