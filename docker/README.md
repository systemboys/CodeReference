# Docker {#topo}

**Navegação:** [🏠 Início](../README.md) | [⬅️ Voltar](../README.md) | [⬆️ Topo](#topo)

---

## Conteúdo

### 🐳 **Docker**
- [Introdução ao Docker](#-introdu%C3%A7%C3%A3o-ao-docker "Introdução ao Docker")
- [💡 Casos de Uso](#-casos-de-uso "Casos de Uso")
- [📦 Instalação do Docker no Linux (Debian)](#-instala%C3%A7%C3%A3o-do-docker-no-linux-debian "Instalação do Docker no Linux (Debian)")
- [🏗️ Conceitos Fundamentais](#%EF%B8%8F-conceitos-fundamentais "Conceitos Fundamentais")
- [🚀 Criando e Gerenciando Containers](#-criando-e-gerenciando-containers "Criando e Gerenciando Containers")
- [📝 Dockerfile: Criando Imagens Personalizadas](#-dockerfile-criando-imagens-personalizadas "Dockerfile: Criando Imagens Personalizadas")
- [🔧 Comandos Essenciais do Docker](#-comandos-essenciais-do-docker "Comandos Essenciais do Docker")
- [🌐 Docker Compose: Orquestração de Múltiplos Containers](#-docker-compose-orquestra%C3%A7%C3%A3o-de-m%C3%BAltiplos-containers "Docker Compose: Orquestração de Múltiplos Containers")
- [🗄️ Gerenciamento de Volumes e Dados](#-gerenciamento-de-volumes-e-dados "Gerenciamento de Volumes e Dados")
- [🌐 Networking no Docker](#-networking-no-docker "Networking no Docker")
- [🔍 Debugging e Troubleshooting](#-debugging-e-troubleshooting "Debugging e Troubleshooting")
- [⚡ Comandos Avançados para Programadores Experientes](#-comandos-avan%C3%A7ados-para-programadores-experientes "Comandos Avançados para Programadores Experientes")

---

Docker e suas ferramentas complementares revolucionaram o desenvolvimento de software ao proporcionar um ambiente isolado e replicável, permitindo que os desenvolvedores e engenheiros de operações (DevOps) otimizem a entrega de aplicações com agilidade e eficiência.

---

## 🐳 Introdução ao Docker

O **Docker** é uma plataforma de código aberto que utiliza **containerização** para empacotar aplicações e suas dependências em containers leves e portáteis. Diferente das máquinas virtuais tradicionais, os containers Docker compartilham o kernel do sistema operacional host, tornando-os mais eficientes em termos de recursos e mais rápidos para iniciar.

### O que são Containers?

Containers são unidades de software que empacotam código, dependências e configurações em um formato padronizado. Eles garantem que uma aplicação funcione da mesma forma, independentemente do ambiente onde é executada (desenvolvimento, teste, produção).

### Principais Benefícios

- ✅ **Isolamento**: Cada container é isolado do sistema host e de outros containers
- ✅ **Portabilidade**: Funciona em qualquer sistema que suporte Docker
- ✅ **Eficiência**: Menor uso de recursos comparado a máquinas virtuais
- ✅ **Consistência**: Mesmo ambiente em desenvolvimento e produção
- ✅ **Escalabilidade**: Fácil criação e destruição de containers

---

**📑 [Voltar ao Índice](#conteúdo)**

## 💡 Casos de Uso

### 1. Desenvolvimento Local
- **Ambiente consistente**: Todos os desenvolvedores trabalham com as mesmas versões de dependências
- **Isolamento de projetos**: Cada projeto tem seu próprio ambiente sem conflitos
- **Setup rápido**: Novos desenvolvedores podem começar a trabalhar em minutos

### 2. CI/CD (Integração e Deploy Contínuo)
- **Testes automatizados**: Execute testes em containers isolados
- **Builds reproduzíveis**: Garante que builds funcionem da mesma forma em qualquer ambiente
- **Deploy simplificado**: Mesma imagem funciona em desenvolvimento e produção

### 3. Microserviços
- **Isolamento de serviços**: Cada microserviço roda em seu próprio container
- **Escalabilidade independente**: Escale serviços específicos conforme necessário
- **Orquestração**: Use Docker Compose ou Kubernetes para gerenciar múltiplos serviços

### 4. Banco de Dados e Serviços
- **Banco de dados temporário**: Execute MySQL, PostgreSQL, MongoDB sem instalação local
- **Múltiplas versões**: Teste com diferentes versões de bancos de dados simultaneamente
- **Serviços auxiliares**: Redis, Elasticsearch, RabbitMQ, etc.

### 5. Aplicações Legacy
- **Modernização gradual**: Containerize aplicações antigas sem reescrever
- **Compatibilidade**: Execute aplicações que requerem versões específicas de SO

---

**📑 [Voltar ao Índice](#conteúdo)**

## 📦 Instalação do Docker no Linux (Debian)

### Pré-requisitos

- Sistema operacional: Debian 10 (Buster) ou superior
- Acesso de root ou usuário com permissões sudo
- Conexão com a internet

### Passo 1: Atualizar o Sistema

```bash
sudo apt update
sudo apt upgrade -y
```

### Passo 2: Instalar Dependências

```bash
sudo apt install -y \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

### Passo 3: Adicionar a Chave GPG Oficial do Docker

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

### Passo 4: Configurar o Repositório do Docker

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Passo 5: Instalar o Docker Engine

```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Passo 6: Verificar a Instalação

```bash
sudo docker --version
sudo docker run hello-world
```

### Passo 7: Adicionar Usuário ao Grupo Docker (Opcional)

Para executar comandos Docker sem `sudo`:

```bash
sudo usermod -aG docker $USER
```

**Importante**: Faça logout e login novamente para que as mudanças tenham efeito.

### Passo 8: Configurar Docker para Iniciar no Boot

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

### Verificar Status do Serviço

```bash
sudo systemctl status docker
```

### Desinstalar Docker (se necessário)

```bash
sudo apt purge -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

---

**📑 [Voltar ao Índice](#conteúdo)**

## 🏗️ Conceitos Fundamentais

### Imagem (Image)

Uma **imagem** é um template somente leitura usado para criar containers. Ela contém todas as instruções necessárias para criar um container, incluindo código da aplicação, bibliotecas, dependências e configurações.

**Exemplo**: `node:18-alpine` é uma imagem que contém Node.js versão 18 em um sistema Alpine Linux.

### Container

Um **container** é uma instância executável de uma imagem. Você pode criar múltiplos containers a partir da mesma imagem. Containers são isolados uns dos outros e do sistema host.

### Dockerfile

Um **Dockerfile** é um arquivo de texto que contém instruções para construir uma imagem Docker. Ele define o ambiente e as dependências necessárias para sua aplicação.

### Docker Hub

O **Docker Hub** é um repositório público de imagens Docker. Você pode baixar imagens prontas ou fazer upload das suas próprias imagens.

### Volume

**Volumes** são mecanismos para persistir dados gerados e usados por containers. Eles permitem que dados sobrevivam mesmo quando containers são removidos.

### Network

**Networks** permitem que containers se comuniquem entre si e com o mundo externo. Docker cria uma rede virtual por padrão.

---

**📑 [Voltar ao Índice](#conteúdo)**

## 🚀 Criando e Gerenciando Containers

### Executar um Container

```bash
docker run <imagem>
```

**Exemplo**: Executar um container Ubuntu interativo

```bash
docker run -it ubuntu:latest /bin/bash
```

### Flags Comuns

- `-it`: Modo interativo com terminal
- `-d`: Executar em background (detached)
- `--name`: Dar um nome ao container
- `-p`: Mapear portas (host:container)
- `-v`: Montar volumes
- `-e`: Definir variáveis de ambiente
- `--rm`: Remover container automaticamente ao parar

### Exemplos Práticos

#### 1. Container Nginx (Servidor Web)

```bash
docker run -d \
  --name meu-nginx \
  -p 8080:80 \
  nginx:latest
```

Acesse: `http://localhost:8080`

#### 2. Container Node.js

```bash
docker run -it \
  --name meu-node \
  -v $(pwd):/app \
  -w /app \
  node:18-alpine \
  sh
```

#### 3. Container MySQL

```bash
docker run -d \
  --name meu-mysql \
  -e MYSQL_ROOT_PASSWORD=senha123 \
  -e MYSQL_DATABASE=meu_banco \
  -p 3306:3306 \
  mysql:8.0
```

#### 4. Container PostgreSQL

```bash
docker run -d \
  --name meu-postgres \
  -e POSTGRES_PASSWORD=senha123 \
  -e POSTGRES_DB=meu_banco \
  -p 5432:5432 \
  postgres:15-alpine
```

### Listar Containers

```bash
# Containers em execução
docker ps

# Todos os containers (incluindo parados)
docker ps -a

# Apenas IDs
docker ps -q
```

### Parar e Iniciar Containers

```bash
# Parar um container
docker stop <container_id ou nome>

# Iniciar um container parado
docker start <container_id ou nome>

# Reiniciar um container
docker restart <container_id ou nome>
```

### Remover Containers

```bash
# Remover um container parado
docker rm <container_id ou nome>

# Remover um container em execução (força)
docker rm -f <container_id ou nome>

# Remover todos os containers parados
docker container prune
```

### Executar Comandos em Containers em Execução

```bash
docker exec -it <container_id ou nome> <comando>
```

**Exemplo**: Acessar shell do container

```bash
docker exec -it meu-nginx /bin/bash
```

### Ver Logs

```bash
# Ver logs de um container
docker logs <container_id ou nome>

# Seguir logs em tempo real
docker logs -f <container_id ou nome>

# Últimas N linhas
docker logs --tail 100 <container_id ou nome>
```

### Inspecionar Container

```bash
# Informações detalhadas
docker inspect <container_id ou nome>

# Informação específica (ex: IP)
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container_id ou nome>
```

---

**📑 [Voltar ao Índice](#conteúdo)**

## 📝 Dockerfile: Criando Imagens Personalizadas

### Estrutura Básica de um Dockerfile

```dockerfile
# Imagem base
FROM node:18-alpine

# Diretório de trabalho
WORKDIR /app

# Copiar arquivos de dependências
COPY package*.json ./

# Instalar dependências
RUN npm install

# Copiar código da aplicação
COPY . .

# Expor porta
EXPOSE 3000

# Comando para executar
CMD ["node", "index.js"]
```

### Instruções Comuns do Dockerfile

- `FROM`: Define a imagem base
- `WORKDIR`: Define o diretório de trabalho
- `COPY`: Copia arquivos do host para o container
- `ADD`: Similar ao COPY, mas também pode baixar URLs e extrair arquivos
- `RUN`: Executa comandos durante a construção da imagem
- `CMD`: Comando padrão executado quando o container inicia
- `ENTRYPOINT`: Similar ao CMD, mas não pode ser sobrescrito facilmente
- `ENV`: Define variáveis de ambiente
- `EXPOSE`: Documenta a porta que o container usa
- `VOLUME`: Cria um ponto de montagem para volumes

### Exemplo: Dockerfile para Aplicação Node.js

```dockerfile
FROM node:18-alpine

# Instalar dependências do sistema
RUN apk add --no-cache python3 make g++

# Criar diretório da aplicação
WORKDIR /app

# Copiar e instalar dependências
COPY package*.json ./
RUN npm ci --only=production

# Copiar código da aplicação
COPY . .

# Criar usuário não-root
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001

# Mudar para usuário não-root
USER nodejs

# Expor porta
EXPOSE 3000

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD node healthcheck.js

# Comando de inicialização
CMD ["node", "index.js"]
```

### Construir uma Imagem

```bash
# Construir imagem
docker build -t nome-da-imagem:tag .

# Construir com contexto diferente
docker build -t nome-da-imagem:tag -f Dockerfile.prod .

# Construir sem cache
docker build --no-cache -t nome-da-imagem:tag .
```

### Multi-stage Build (Build em Múltiplas Etapas)

Útil para reduzir o tamanho final da imagem:

```dockerfile
# Etapa 1: Build
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Etapa 2: Produção
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package*.json ./
EXPOSE 3000
CMD ["node", "dist/index.js"]
```

---

**📑 [Voltar ao Índice](#conteúdo)**

## 🔧 Comandos Essenciais do Docker

### Gerenciamento de Imagens

```bash
# Listar imagens
docker images

# Baixar imagem
docker pull <imagem>:<tag>

# Remover imagem
docker rmi <imagem_id ou nome>

# Remover imagens não utilizadas
docker image prune

# Remover todas as imagens não utilizadas
docker image prune -a

# Inspecionar imagem
docker inspect <imagem>

# Histórico de uma imagem
docker history <imagem>
```

### Gerenciamento de Containers

```bash
# Criar container sem iniciar
docker create --name meu-container <imagem>

# Executar comando em container parado
docker start -a <container>

# Pausar/Despausar container
docker pause <container>
docker unpause <container>

# Renomear container
docker rename <nome-antigo> <nome-novo>

# Copiar arquivos
docker cp <container>:<caminho> <destino-local>
docker cp <arquivo-local> <container>:<caminho>

# Estatísticas em tempo real
docker stats

# Estatísticas de um container específico
docker stats <container>
```

### Limpeza

```bash
# Remover containers parados
docker container prune

# Remover imagens não utilizadas
docker image prune

# Remover volumes não utilizados
docker volume prune

# Remover networks não utilizadas
docker network prune

# Limpeza completa (cuidado!)
docker system prune -a --volumes
```

### Informações do Sistema

```bash
# Informações do Docker
docker info

# Versão do Docker
docker version

# Uso de disco
docker system df

# Uso detalhado
docker system df -v
```

---

**📑 [Voltar ao Índice](#conteúdo)**

## 🌐 Docker Compose: Orquestração de Múltiplos Containers

O **Docker Compose** permite definir e executar aplicações multi-container usando um arquivo YAML.

### Instalação do Docker Compose

Geralmente já vem instalado com o Docker. Verifique:

```bash
docker compose version
```

### Exemplo: docker-compose.yml

```yaml
version: '3.8'

services:
  # Aplicação Node.js
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DATABASE_URL=postgresql://user:password@db:5432/mydb
    depends_on:
      - db
    volumes:
      - ./:/app
      - /app/node_modules

  # Banco de dados PostgreSQL
  db:
    image: postgres:15-alpine
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=mydb
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"

  # Redis
  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"

volumes:
  postgres_data:
```

### Comandos do Docker Compose

```bash
# Iniciar serviços
docker compose up

# Iniciar em background
docker compose up -d

# Parar serviços
docker compose down

# Parar e remover volumes
docker compose down -v

# Reconstruir imagens
docker compose build

# Ver logs
docker compose logs

# Ver logs de um serviço específico
docker compose logs app

# Executar comando em um serviço
docker compose exec app sh

# Escalar serviços
docker compose up -d --scale app=3

# Listar serviços
docker compose ps
```

---

**📑 [Voltar ao Índice](#conteúdo)**

## 🗄️ Gerenciamento de Volumes e Dados

### Tipos de Volumes

1. **Named Volumes**: Gerenciados pelo Docker
2. **Bind Mounts**: Mapeiam diretórios do host
3. **tmpfs Mounts**: Armazenados na memória (Linux)

### Criar e Gerenciar Volumes

```bash
# Criar volume
docker volume create meu-volume

# Listar volumes
docker volume ls

# Inspecionar volume
docker volume inspect meu-volume

# Remover volume
docker volume rm meu-volume

# Remover volumes não utilizados
docker volume prune
```

### Usar Volumes em Containers

```bash
# Named volume
docker run -v meu-volume:/data <imagem>

# Bind mount
docker run -v /caminho/local:/caminho/container <imagem>

# Volume anônimo
docker run -v /caminho/container <imagem>
```

### Exemplo: Persistir Dados do MySQL

```bash
docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=senha123 \
  -v mysql_data:/var/lib/mysql \
  mysql:8.0
```

### Backup e Restore de Volumes

```bash
# Backup
docker run --rm \
  -v mysql_data:/data \
  -v $(pwd):/backup \
  alpine tar czf /backup/mysql-backup.tar.gz /data

# Restore
docker run --rm \
  -v mysql_data:/data \
  -v $(pwd):/backup \
  alpine sh -c "cd /data && tar xzf /backup/mysql-backup.tar.gz"
```

---

**📑 [Voltar ao Índice](#conteúdo)**

## 🌐 Networking no Docker

### Tipos de Networks

1. **bridge**: Rede padrão para containers
2. **host**: Usa a rede do host diretamente
3. **none**: Sem rede
4. **overlay**: Para Docker Swarm
5. **macvlan**: Atribui endereço MAC ao container

### Gerenciar Networks

```bash
# Listar networks
docker network ls

# Criar network
docker network create minha-rede

# Inspecionar network
docker network inspect minha-rede

# Conectar container a network
docker network connect minha-rede meu-container

# Desconectar container
docker network disconnect minha-rede meu-container

# Remover network
docker network rm minha-rede
```

### Exemplo: Containers na Mesma Rede

```bash
# Criar network
docker network create app-network

# Container 1 (App)
docker run -d \
  --name app \
  --network app-network \
  minha-app:latest

# Container 2 (Database)
docker run -d \
  --name db \
  --network app-network \
  postgres:15-alpine
```

Os containers podem se comunicar usando os nomes: `app` pode acessar `db` diretamente.

---

**📑 [Voltar ao Índice](#conteúdo)**

## 🔍 Debugging e Troubleshooting

### Verificar Status de Containers

```bash
# Ver processos em execução
docker ps

# Ver todos os containers
docker ps -a

# Ver últimas N linhas de logs
docker logs --tail 50 <container>

# Ver logs com timestamp
docker logs -t <container>
```

### Acessar Container em Execução

```bash
# Shell interativo
docker exec -it <container> /bin/bash

# Se bash não estiver disponível, use sh
docker exec -it <container> /bin/sh

# Executar comando específico
docker exec <container> <comando>
```

### Inspecionar Recursos

```bash
# Inspecionar container
docker inspect <container>

# Inspecionar imagem
docker inspect <imagem>

# Inspecionar network
docker network inspect <network>

# Inspecionar volume
docker volume inspect <volume>
```

### Monitoramento de Recursos

```bash
# Estatísticas em tempo real
docker stats

# Estatísticas de container específico
docker stats <container>

# Sem streaming (uma vez)
docker stats --no-stream
```

### Verificar Eventos

```bash
# Ver eventos do Docker
docker events

# Eventos de um container específico
docker events --filter container=<container>
```

### Limpar Recursos

```bash
# Ver uso de disco
docker system df

# Limpeza completa (cuidado!)
docker system prune -a --volumes

# Limpar apenas containers parados
docker container prune

# Limpar apenas imagens não utilizadas
docker image prune -a
```

---

**📑 [Voltar ao Índice](#conteúdo)**

## ⚡ Comandos Avançados para Programadores Experientes

### Build Avançado

```bash
# Build com argumentos
docker build --build-arg NODE_ENV=production -t app:prod .

# Build com target específico (multi-stage)
docker build --target builder -t app:builder .

# Build com cache de uma imagem específica
docker build --cache-from app:latest -t app:latest .

# Build com secrets (Docker BuildKit)
DOCKER_BUILDKIT=1 docker build --secret id=mysecret,src=./secret.txt .
```

### Execução Avançada

```bash
# Executar com recursos limitados
docker run --memory="512m" --cpus="1.0" <imagem>

# Executar com privilégios
docker run --privileged <imagem>

# Executar com capabilities específicas
docker run --cap-add=NET_ADMIN <imagem>

# Executar com variáveis de ambiente de arquivo
docker run --env-file .env <imagem>

# Executar com hostname customizado
docker run --hostname meu-host <imagem>

# Executar com DNS customizado
docker run --dns 8.8.8.8 <imagem>
```

### Logs e Monitoramento Avançado

```bash
# Logs com limite de tamanho
docker logs --tail 1000 <container> | head -100

# Logs com filtro
docker logs <container> 2>&1 | grep ERROR

# Exportar logs
docker logs <container> > container.log

# Estatísticas em formato JSON
docker stats --no-stream --format "{{json .}}"

# Monitorar múltiplos containers
docker stats $(docker ps -q)
```

### Manipulação de Imagens

```bash
# Salvar imagem para arquivo
docker save -o imagem.tar <imagem>:<tag>

# Carregar imagem de arquivo
docker load -i imagem.tar

# Exportar container para tar
docker export <container> > container.tar

# Importar container de tar
docker import container.tar nova-imagem:tag

# Tag de imagem
docker tag <imagem>:<tag> <novo-nome>:<nova-tag>

# Push para registry
docker push <imagem>:<tag>

# Pull de registry privado
docker pull registry.example.com/<imagem>:<tag>
```

### Scripts Úteis

#### Limpar tudo (cuidado!)

```bash
#!/bin/bash
docker stop $(docker ps -aq)
docker rm $(docker ps -aq)
docker rmi $(docker images -q)
docker volume prune -f
docker network prune -f
```

#### Backup de todos os volumes

```bash
#!/bin/bash
for volume in $(docker volume ls -q); do
  docker run --rm \
    -v $volume:/data \
    -v $(pwd):/backup \
    alpine tar czf /backup/$volume-backup.tar.gz /data
done
```

#### Listar tamanhos de imagens

```bash
docker images --format "table {{.Repository}}\t{{.Tag}}\t{{.Size}}" | sort -k3 -h
```

### Docker Compose Avançado

```bash
# Build apenas serviços específicos
docker compose build app db

# Executar comando em serviço
docker compose exec app npm test

# Escalar serviço
docker compose up -d --scale app=5

# Usar arquivo compose alternativo
docker compose -f docker-compose.prod.yml up -d

# Validar arquivo compose
docker compose config
```

### Troubleshooting Comum

#### Container não inicia

```bash
# Ver logs
docker logs <container>

# Verificar eventos
docker events --since 1h | grep <container>

# Inspecionar configuração
docker inspect <container>
```

#### Problemas de rede

```bash
# Verificar networks
docker network ls
docker network inspect <network>

# Testar conectividade entre containers
docker exec <container1> ping <container2>
```

#### Problemas de volume

```bash
# Verificar volumes
docker volume ls
docker volume inspect <volume>

# Verificar montagens
docker inspect <container> | grep -A 10 Mounts
```

---

**📑 [Voltar ao Índice](#conteúdo)**
