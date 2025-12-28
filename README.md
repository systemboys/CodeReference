# CodeReference

> **Documentação profissional de código para desenvolvedores**

Uma coleção organizada de snippets, exemplos e guias práticos para desenvolvimento web moderno, focada em **Node.js**, **React.js**, **Prisma ORM** e tecnologias relacionadas.

---

## 📚 Sobre

**CodeReference** é um repositório de referência técnica criado para consolidar conhecimento e acelerar o desenvolvimento. Documentar e organizar o que você aprende é uma das melhores formas de consolidar conhecimento e se preparar para desafios futuros. 🔥

Este projeto reúne exemplos práticos, padrões de código, configurações e soluções para problemas comuns no desenvolvimento de aplicações fullstack.

---

## 🛠️ Stack Tecnológica

- **Backend:** Node.js + Express + Prisma ORM + TypeScript
- **Frontend:** React.js + JavaScript/TypeScript
- **Banco de Dados:** MySQL, PostgreSQL, SQLite
- **Ferramentas:** Docker, Vite, Nginx

---

## 📖 Estrutura do Projeto

```
CodeReference/
├── frontend/          # Guias e exemplos de React.js
├── backend/           # Guias e exemplos de Node.js + Prisma
├── scripts/           # Scripts prontos e utilitários
└── docker/            # Configurações e guias Docker
```

---

## 🚀 Navegação Rápida

### Frontend
- [React.js - Componentes e Hooks](./frontend/README.md)
- [Formulários e Validação](./frontend/README.md#formulários)
- [Roteamento e Navegação](./frontend/README.md#roteamento)
- [Estilização e Layout](./frontend/README.md#estilização)

### Backend
- [Node.js + Express](./backend/README.md)
- [Prisma ORM](./backend/README.md#prisma-orm)
- [APIs RESTful](./backend/README.md#apis-restful)
- [Gerenciamento de Banco de Dados](./backend/README.md#banco-de-dados)

### Scripts Prontos
- [CRUD Completo](./scripts/README.md#crud-completo)
- [Utilitários JavaScript](./scripts/README.md#utilitários)
- [Automações](./scripts/README.md#automações)

### Deploy e Testes
- [Expondo Aplicações Locais na Web com ngrok](#expondo-aplica%C3%A7%C3%B5es-locais-na-web-com-ngrok)

---

## 🌐 Expondo Aplicações Locais na Web com ngrok

O **ngrok** é uma ferramenta que permite expor aplicações rodando em `localhost` para a internet, criando um túnel seguro. Isso é útil para compartilhar projetos em desenvolvimento com colegas, testar webhooks, ou demonstrar aplicações em tempo real.

### 📋 Pré-requisitos

- Conta no [ngrok](https://ngrok.com) (gratuita ou paga)
- Aplicação rodando localmente em uma porta específica (ex: `http://localhost:3000`)

### 🔧 Configuração Inicial

#### 1. Obter o Authtoken

1. Acesse o [painel do ngrok](https://dashboard.ngrok.com)
2. Faça login na sua conta
3. Procure a seção **"Your Authtoken"** no painel
4. Torne seu Authtoken visível (clicando no ícone de olho)
5. Copie o token (exemplo: `37TZsNByXgt88CJFymuOrXxOewD_5jqWj2vG7c2pNAPLbQFax`)

#### 2. Instalar o ngrok

**No Linux (Debian/Ubuntu):**

```bash
curl -sSL https://ngrok-agent.s3.amazonaws.com/ngrok.asc \
  | sudo tee /etc/apt/trusted.gpg.d/ngrok.asc >/dev/null \
  && echo "deb https://ngrok-agent.s3.amazonaws.com bookworm main" \
  | sudo tee /etc/apt/sources.list.d/ngrok.list \
  && sudo apt update \
  && sudo apt install ngrok
```

**Alternativa (Download direto):**

Baixe o binário do [site oficial](https://ngrok.com/download) e coloque em um diretório acessível.

#### 3. Configurar o Authtoken

Execute o comando abaixo substituindo `<SEU_AUTHTOKEN>` pelo token copiado:

```bash
ngrok config add-authtoken <SEU_AUTHTOKEN>
```

**Exemplo:**

```bash
ngrok config add-authtoken 37TZsNByXgt88CJFymuOrXxOewD_5jqWj2vG7c2pNAPLbQFax
```

Você verá uma mensagem de confirmação:

```bash
Authtoken saved to configuration file: /root/.config/ngrok/ngrok.yml
```

### 🚀 Usando o ngrok

#### Expor uma aplicação local

Execute o comando abaixo substituindo `<PORTA>` pela porta onde sua aplicação está rodando:

```bash
ngrok http <PORTA>
```

**Exemplo:**

Se sua aplicação está rodando em `http://localhost:3000`:

```bash
ngrok http 3000
```

#### Saída esperada

Após executar o comando, você verá algo como:

```bash
ngrok                                                                               (Ctrl+C to quit)

⚠️ Free Users: Agents ≤3.19.x stop connecting 2/17/26. Update or upgrade: https://ngrok.com/pricing  

Session Status                online                                                                
Account                       Seu Nome (Plan: Free)                            
Version                       3.34.1                                                                
Region                        South America (sa)                                                    
Latency                       76ms                                                                  
Web Interface                 http://127.0.0.1:4040                                                 
Forwarding                    https://kiley-uncelebrated-enzo.ngrok-free.dev -> http://localhost:3000

Connections                   ttl     opn     rt1     rt5     p50     p90                           
                              0       0       0.00    0.00    0.00    0.00
```

#### Acessar a aplicação

1. **Copie o endereço HTTPS** mostrado em `Forwarding` (ex: `https://kiley-uncelebrated-enzo.ngrok-free.dev`)
2. **Compartilhe o link** com quem precisa acessar
3. **Acesse no navegador** - na primeira vez, pode aparecer uma página de aviso do ngrok; clique em **"Visit Site"** para continuar

### 📌 Observações Importantes

- ⚠️ **O túnel permanece ativo apenas enquanto o comando `ngrok` estiver em execução**
- 🔒 **URLs gratuitas mudam a cada execução** - para URLs fixas, considere um plano pago
- 🌍 **A aplicação local deve estar rodando** antes de iniciar o ngrok
- 🔄 **Para parar o túnel**, pressione `Ctrl+C` no terminal onde o ngrok está rodando
- 📊 **Interface Web**: Acesse `http://127.0.0.1:4040` para ver estatísticas e requisições em tempo real

### 💡 Casos de Uso

- ✅ Compartilhar projetos em desenvolvimento com colegas
- ✅ Testar webhooks de serviços externos (GitHub, Stripe, etc.)
- ✅ Demonstrar aplicações para clientes sem deploy
- ✅ Testar aplicações mobile conectadas a APIs locais
- ✅ Debugging de integrações em tempo real

---

## 📝 Como Usar

1. **Navegue pelos diretórios** para encontrar o tópico desejado
2. **Copie e adapte** os exemplos para seu projeto
3. **Contribua** melhorando os exemplos existentes

---

## 🎯 Objetivo

Fornecer uma referência rápida e confiável para:
- Padrões de código reutilizáveis
- Soluções para problemas comuns
- Boas práticas de desenvolvimento
- Configurações de ambiente
- Integrações entre frontend e backend

---

## 📄 Licença

Este projeto é de uso pessoal e educacional.

---

**Desenvolvido por:** [Marcos Aurélio Rocha da Silva](https://github.com/systemboys/ "Programador sênior") (Engenheiro de Software - bacharelado)
**Última atualização:** 2024

