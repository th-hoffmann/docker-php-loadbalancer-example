# 🐳 Exemplo Docker PHP com Load Balancer

![Status](https://img.shields.io/badge/status-conclu%C3%ADdo-brightgreen?style=for-the-badge) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white) ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white) ![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white) ![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)

[🇺🇸 Read in English](https://github.com/th-hoffmann/docker-php-loadbalancer-example/blob/main/README.md) • 🇧🇷 Português

**Demonstração prática de containers Docker em cenários de microsserviços com balanceamento de carga e integração com banco de dados**

## 📋 Sobre o Projeto

Este projeto foi desenvolvido como uma demonstração prática da real função do Docker em ambientes de microsserviços, mostrando como containers podem ser efetivamente aplicados em cenários do dia a dia de desenvolvimento. O projeto implementa uma arquitetura completa de microsserviços com balanceamento de carga Nginx, aplicações PHP e integração com banco de dados MySQL.

### 🎯 Objetivo

Criar um exemplo prático que demonstre a real função de containers em cenários de microsserviços, respondendo questões-chave sobre aplicações práticas do Docker em fluxos de desenvolvimento moderno e fornecendo exemplos práticos que podem ser aplicados em projetos reais.

## 🏗️ Visão Geral da Arquitetura

O projeto implementa um ecossistema completo de microsserviços demonstrando padrões da indústria:

| Componente | Tecnologia | Propósito | Configuração |
|------------|------------|-----------|--------------|
| **Load Balancer** | Nginx | Distribuição de tráfego | Porta 4500 |
| **Serviços Web** | PHP/Apache | Lógica da aplicação | Múltiplas instâncias |
| **Banco de Dados** | MySQL | Persistência de dados | Servidor MySQL remoto |
| **Orquestração** | Docker | Gerenciamento de serviços | Rede customizada |

## ⚡ Funcionalidades

### 🔧 Arquitetura de Microsserviços
• ✅ **Balanceamento de Carga** → Configuração upstream do Nginx com múltiplos servidores backend
• ✅ **Descoberta de Serviços** → Registro e descoberta automática de serviços
• ✅ **Escalabilidade Horizontal** → Múltiplas instâncias de aplicação PHP
• ✅ **Integração com Banco** → Conectividade MySQL com pool de conexões

### 🛡️ Padrões para Produção
• 🔄 **Alta Disponibilidade** → Múltiplas instâncias de serviço para redundância
• 📊 **Distribuição de Carga** → Algoritmo de balanceamento round-robin
• 🌐 **Isolamento de Rede** → Rede Docker customizada para segurança
• 🚀 **Orquestração de Containers** → Gerenciamento eficiente de recursos

### ⚙️ Fluxo de Desenvolvimento
• 🎯 **Deploy Simplificado** → Orquestração de containers com um comando
• 📝 **Gerenciamento de Configuração** → Arquivos de configuração externalizados
• 🔧 **Paridade de Ambiente** → Ambientes de desenvolvimento/produção consistentes
• 💡 **Valor Educacional** → Perfeito para aprender padrões de microsserviços

## 🚀 Como Usar

### 📋 Pré-requisitos

• **Docker Engine**: 20.10+ com suporte ao BuildKit
• **Docker Compose**: 2.0+ para orquestração multi-container
• **Requisitos do Sistema**: 4GB RAM, 10GB espaço em disco
• **Acesso à Rede**: Conexão com internet para download de imagens

### 🔧 Instalação e Deploy

1. **Clone o repositório:**
```bash
git clone https://github.com/th-hoffmann/docker-php-loadbalancer-example.git
cd docker-php-loadbalancer-example
```

2. **Configure o ambiente:**
```bash
# Revise e ajuste os arquivos de configuração
nano nginx.conf  # Configuração do load balancer
nano index.php   # Configuração da aplicação
```

3. **Execute os serviços:**
```bash
# Construa o container do load balancer Nginx
docker build -t nginx-loadbalancer .

# Inicie o load balancer
docker run -d -p 4500:4500 --name loadbalancer nginx-loadbalancer

# Verifique o deploy
docker ps
```

4. **Verifique a implantação:**
```bash
# Verifique a saúde do serviço
curl http://localhost:4500

# Monitore os logs
docker logs loadbalancer

# Acesse a aplicação
# Navegue para: http://localhost:4500
```

## 📁 Estrutura do Projeto

```
docker-php-loadbalancer-example/
├── 🐳 dockerfile                    # Container do load balancer Nginx
├── ⚙️  nginx.conf                   # Configuração do load balancer
├── 🐘 index.php                     # Código da aplicação PHP
├── 🗄️  banco.sql                    # Schema do banco de dados
├── 📖 README.md                     # Documentação (Inglês)
└── 📖 README_pt-br.md              # Documentação (Português)
```

## ⚙️ Detalhes da Configuração

### 🌐 Configuração do Load Balancer

A configuração do Nginx implementa padrões avançados de balanceamento de carga:

```nginx
http {
    upstream all {
        server 172.31.0.37:80;
        server 172.31.0.151:80;
        server 172.31.0.149:80;
    }

    server {
         listen 4500;
         location / {
              proxy_pass http://all/;
         }
    }
}

events { }
```

### 🐘 Integração com Banco de Dados

A aplicação PHP demonstra padrões adequados de conectividade com banco:

```php
$servername = "54.234.153.24";
$username = "root";
$password = "Senha123";
$database = "meubanco";

$link = new mysqli($servername, $username, $password, $database);

// Insere dados aleatórios para demonstrar funcionalidade
$valor_rand1 = rand(1, 999);
$valor_rand2 = strtoupper(substr(bin2hex(random_bytes(4)), 1));
$host_name = gethostname();

$query = "INSERT INTO dados (AlunoID, Nome, Sobrenome, Endereco, Cidade, Host) 
          VALUES ('$valor_rand1', '$valor_rand2', '$valor_rand2', '$valor_rand2', '$valor_rand2', '$host_name')";
```

### 🗄️ Schema do Banco de Dados

```sql
CREATE TABLE dados (
    AlunoID int,
    Nome varchar(50),
    Sobrenome varchar(50),
    Endereco varchar(150),
    Cidade varchar(50),
    Host varchar(50)
);
```

## 🛡️ Segurança

### 🔐 Boas Práticas Aplicadas

• **Segmentação de Rede** → Redes de container isoladas
• **Variáveis de Ambiente** → Gerenciamento seguro de configuração
• **Controle de Acesso** → Princípio do menor privilégio
• **Segurança de Container** → Execução com usuário não-root

### ⚠️ Considerações de Segurança

> 🚨 **Nota**: Este projeto foi projetado para fins educacionais e de desenvolvimento. Para deploy em produção, considere:

• Terminação SSL/TLS no load balancer
• Criptografia de conexão com banco de dados
• Gerenciamento de secrets com Docker Secrets
• Scan de vulnerabilidades em imagens de container
• Políticas de rede e regras de firewall
• Gerenciamento seguro de credenciais do banco

## 📚 Conceitos Aplicados

### 🏗️ Arquitetura de Microsserviços

• **Decomposição de Serviços** → Quebra de monólitos em serviços
• **Gerenciamento de Dados** → Padrão de banco por serviço
• **Padrões de Comunicação** → Comunicação inter-serviços baseada em HTTP
• **Independência de Deploy** → Deploy individual de serviços

### 🐳 Docker e Containerização

• **Orquestração de Containers** → Gerenciamento de aplicação multi-container
• **Otimização de Imagens** → Imagens de container eficientes
• **Networking** → Configuração de rede customizada
• **Gerenciamento de Volumes** → Padrões de persistência de dados

## 🤝 Contribuindo

Contribuições são bem-vindas! Sinta-se à vontade para:

• 🐛 Reportar bugs
• 💡 Sugerir melhorias
• 🔧 Enviar pull requests
• 📖 Melhorar a documentação

## 📄 Licença

Este projeto está licenciado sob a Licença MIT. Veja o arquivo LICENSE para detalhes.

## 👨‍💻 Autor

Desenvolvido por [th-hoffmann](https://github.com/th-hoffmann) baseado no treinamento prático de Docker por Denilson Bonatti da Digital Innovation One.

### ⭐ Se este projeto foi útil, considere dar uma estrela!

🔙 [Voltar ao topo](#-exemplo-docker-php-com-load-balancer)

---

## Sobre

**Demonstração de microsserviços Docker com balanceamento de carga Nginx, aplicações PHP e integração MySQL. Perfeito para aprender orquestração de containers e padrões de arquitetura de microsserviços.**

### Tópicos

`docker` `microsserviços` `nginx` `php` `mysql` `balanceamento-de-carga` `containers` `devops` `arquitetura` `escalabilidade` `alta-disponibilidade` `desenvolvimento-web` `integração-banco-dados` `infraestrutura` `automação` `orquestração` `redes`
