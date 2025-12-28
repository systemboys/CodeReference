# Deploy e Hospedagem

**Navegação:** [🏠 Início](../README.md) | [⬅️ Voltar](../README.md) | [⬆️ Topo](#topo)

---

## Conteúdo

### 🌐 **Expondo Aplicações Locais**
- [Expondo Aplicações Locais na Web com ngrok](#-expondo-aplica%C3%A7%C3%B5es-locais-na-web-com-ngrok)

---

Esta seção contém guias e instruções para deploy, hospedagem, servidores e ferramentas relacionadas a expor aplicações na web.

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

**📑 [Voltar ao Índice](#conteúdo)**

