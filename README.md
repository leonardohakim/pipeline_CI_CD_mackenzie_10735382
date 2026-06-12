# Pipeline CI/CD - Mackenzie

Projeto da atividade prática de CI/CD com GitHub Actions.

# Pipeline CI/CD com GitHub Actions

Este projeto demonstra na prática como criar um pipeline completo de **Integração Contínua (CI)** e **Entrega/Deploy Contínuo (CD)** utilizando GitHub Actions para publicar automaticamente um site estático no **GitHub Pages**.

## Estrutura do Projeto

```
seu-projeto/
├── site/
│   └── index.html          # Página estática (HTML + Tailwind)
├── .github/
│   └── workflows/
│       ├── ci.yml          # Pipeline de Integração Contínua
│       └── cd.yml          # Pipeline de Deploy Contínuo (GitHub Pages)
└── README.md
```

## O que o Pipeline Faz

### CI (`ci.yml`) — Integração Contínua
Disparado automaticamente em:
- Push para `main` ou `master`
- Pull Requests para `main` ou `master`

**Etapas executadas:**
1. **Checkout** do código
2. **Validação da estrutura** do projeto
3. **Validação do HTML** (tags obrigatórias)
4. **Execução de testes simples**
5. **Geração de artefatos** (build-info + site)
6. **Upload de artefatos** para visualização posterior

### CD (`cd.yml`) — Deploy Contínuo
Disparado automaticamente em:
- Push para `main` ou `master`
- Manualmente via botão **"Run workflow"**

**Etapas executadas:**
1. Checkout do código
2. Configuração do GitHub Pages
3. Upload do conteúdo da pasta `site/` como artefato do Pages
4. Deploy automático para produção

---

## Como Configurar e Executar

### Passo 1: Criar o Repositório no GitHub

1. Acesse [github.com](https://github.com) e crie um **novo repositório** (pode ser público).
2. **Não** inicialize com README, .gitignore ou license (vamos subir manualmente).

### Passo 2: Subir o Projeto

```bash
# Clone seu repositório vazio
git clone https://github.com/SEU-USUARIO/nome-do-repositorio.git
cd nome-do-repositorio

# Copie os arquivos deste projeto para dentro da pasta
# (ou faça unzip do arquivo fornecido)

# Adicione, commite e envie
git add .
git commit -m "feat: adiciona pipeline CI/CD completo com GitHub Actions"
git push -u origin main
```

### Passo 3: Ativar GitHub Pages com Actions

1. Vá até seu repositório no GitHub
2. Clique em **Settings** (Configurações)
3. No menu lateral, clique em **Pages**
4. Em **Source**, selecione **GitHub Actions** (em vez de "Deploy from a branch")
5. Salve as alterações

> **Importante**: Esta etapa é essencial para que o workflow `cd.yml` consiga fazer o deploy.

### Passo 4: Observar a Execução

1. Vá na aba **Actions** do seu repositório
2. Você verá dois workflows sendo executados:
   - **CI - Integração Contínua**
   - **CD - Deploy Contínuo (GitHub Pages)**
3. Clique em cada um para ver os **logs detalhados** em tempo real
4. Após a conclusão do CD, o site estará disponível em:

```
https://SEU-USUARIO.github.io/nome-do-repositorio
```

---

## O que Observar nos Logs

### No workflow de CI:
- Validação da estrutura de pastas
- Verificação das tags HTML
- Resultado dos testes simples
- Geração e upload do artefato `site-build-artifact`

### No workflow de CD:
- Configuração do ambiente GitHub Pages
- Upload do conteúdo da pasta `./site`
- URL final gerada (`page_url`)
- Confirmação de deploy bem-sucedido

---

## Objetivos de Aprendizado Atendidos

- [x] Controle de versão com Git
- [x] Estruturação de projeto com separação clara (site + workflows)
- [x] Pipeline de Integração Contínua (validação + testes)
- [x] Pipeline de Deploy Contínuo
- [x] Publicação automática no GitHub Pages
- [x] Observação de logs, métricas e artefatos
- [x] Boas práticas de YAML e Actions oficiais do GitHub

---

## Personalizações Possíveis

- Adicionar mais jobs no CI (ex: lint HTML mais rigoroso, testes com Cypress, etc.)
- Adicionar ambiente de **staging** antes do deploy em produção
- Usar `workflow_run` para fazer o CD depender explicitamente do CI passar
- Adicionar notificações (Slack, Discord, email) ao final do deploy
- Versionar o site com cache busting ou adicionar um `version.txt`

---

## Referências Oficiais

- [GitHub Actions Documentation](https://docs.github.com/actions)
- [Deploying to GitHub Pages using Actions](https://docs.github.com/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages)
- [actions/configure-pages](https://github.com/actions/configure-pages)
- [actions/deploy-pages](https://github.com/actions/deploy-pages)
- [actions/upload-pages-artifact](https://github.com/actions/upload-pages-artifact)

---
