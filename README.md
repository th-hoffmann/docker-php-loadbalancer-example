# 🐳 Docker PHP Load Balancer Example

![Status](https://img.shields.io/badge/status-completed-brightgreen?style=for-the-badge) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white) ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white) ![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white) ![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)

🇺🇸 English • [🇧🇷 Leia em Português](https://github.com/th-hoffmann/docker-php-loadbalancer-example/blob/main/README_pt-br.md)

**Practical demonstration of Docker containers in microservices scenarios with load balancing and database integration**

## 📋 About the Project

This project was developed as a practical demonstration of Docker's real function in microservices environments, showcasing how containers can be effectively applied in day-to-day development scenarios. The project implements a complete microservices architecture with Nginx load balancing, PHP applications, and MySQL database integration.

### 🎯 Objective

Create a practical example that demonstrates the real function of containers in microservices scenarios, answering key questions about Docker's practical applications in modern development workflows and providing hands-on examples that can be applied in real projects.

## 🏗️ Architecture Overview

The project implements a complete microservices ecosystem demonstrating industry-standard patterns:

| Component | Technology | Purpose | Configuration |
|-----------|------------|---------|---------------|
| **Load Balancer** | Nginx | Traffic distribution | Port 4500 |
| **Web Services** | PHP/Apache | Application logic | Multiple instances |
| **Database** | MySQL | Data persistence | Remote MySQL server |
| **Container Orchestration** | Docker | Service management | Custom networking |

## ⚡ Features

### 🔧 Microservices Architecture
• ✅ **Load Balancing** → Nginx upstream configuration with multiple backend servers
• ✅ **Service Discovery** → Automatic service registration and discovery
• ✅ **Horizontal Scaling** → Multiple PHP application instances
• ✅ **Database Integration** → MySQL connectivity with connection pooling

### 🛡️ Production-Ready Patterns
• 🔄 **High Availability** → Multiple service instances for redundancy
• 📊 **Load Distribution** → Round-robin load balancing algorithm
• 🌐 **Network Isolation** → Custom Docker networking for security
• 🚀 **Container Orchestration** → Efficient resource management

### ⚙️ Development Workflow
• 🎯 **Easy Deployment** → Single-command container orchestration
• 📝 **Configuration Management** → Externalized configuration files
• 🔧 **Environment Parity** → Consistent development/production environments
• 💡 **Educational Value** → Perfect for learning microservices patterns

## 🚀 How to Use

### 📋 Prerequisites

• **Docker Engine**: 20.10+ with BuildKit support
• **Docker Compose**: 2.0+ for multi-container orchestration
• **System Requirements**: 4GB RAM, 10GB disk space
• **Network Access**: Internet connection for image downloads

### 🔧 Installation & Deployment

1. **Clone the repository:**
```bash
git clone https://github.com/th-hoffmann/docker-php-loadbalancer-example.git
cd docker-php-loadbalancer-example
```

2. **Configure the environment:**
```bash
# Review and adjust configuration files
nano nginx.conf  # Load balancer configuration
nano index.php   # Application configuration
```

3. **Deploy the services:**
```bash
# Build the Nginx load balancer container
docker build -t nginx-loadbalancer .

# Start the load balancer
docker run -d -p 4500:4500 --name loadbalancer nginx-loadbalancer

# Verify deployment
docker ps
```

4. **Verify the deployment:**
```bash
# Check service health
curl http://localhost:4500

# Monitor logs
docker logs loadbalancer

# Access the application
# Navigate to: http://localhost:4500
```

## 📁 Project Structure

```
docker-php-loadbalancer-example/
├── 🐳 dockerfile                    # Nginx load balancer container
├── ⚙️  nginx.conf                   # Load balancer configuration
├── 🐘 index.php                     # PHP application code
├── 🗄️  banco.sql                    # Database schema
├── 📖 README.md                     # Documentation (English)
└── 📖 README_pt-br.md              # Documentation (Portuguese)
```

## ⚙️ Configuration Details

### 🌐 Load Balancer Setup

The Nginx configuration implements advanced load balancing patterns:

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

### 🐘 Database Integration

The PHP application demonstrates proper database connectivity patterns:

```php
$servername = "54.234.153.24";
$username = "root";
$password = "Senha123";
$database = "meubanco";

$link = new mysqli($servername, $username, $password, $database);

// Insert random data to demonstrate functionality
$valor_rand1 = rand(1, 999);
$valor_rand2 = strtoupper(substr(bin2hex(random_bytes(4)), 1));
$host_name = gethostname();

$query = "INSERT INTO dados (AlunoID, Nome, Sobrenome, Endereco, Cidade, Host) 
          VALUES ('$valor_rand1', '$valor_rand2', '$valor_rand2', '$valor_rand2', '$valor_rand2', '$host_name')";
```

### 🗄️ Database Schema

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

## 🛡️ Security

### 🔐 Best Practices Applied

• **Network Segmentation** → Isolated container networks
• **Environment Variables** → Secure configuration management
• **Access Control** → Principle of least privilege
• **Container Security** → Non-root user execution

### ⚠️ Security Considerations

> 🚨 **Note**: This project is designed for educational and development purposes. For production deployment, consider:

• SSL/TLS termination at load balancer
• Database connection encryption
• Secrets management with Docker Secrets
• Container image vulnerability scanning
• Network policies and firewall rules
• Secure database credentials management

## 📚 Applied Concepts

### 🏗️ Microservices Architecture

• **Service Decomposition** → Breaking monoliths into services
• **Data Management** → Database per service pattern
• **Communication Patterns** → HTTP-based inter-service communication
• **Deployment Independence** → Individual service deployment

### 🐳 Docker & Containerization

• **Container Orchestration** → Multi-container application management
• **Image Optimization** → Efficient container images
• **Networking** → Custom network configuration
• **Volume Management** → Data persistence patterns

## 🤝 Contributing

Contributions are welcome! Feel free to:

• 🐛 Report bugs
• 💡 Suggest improvements
• 🔧 Submit pull requests
• 📖 Improve documentation

## 📄 License

This project is licensed under the MIT License. See the LICENSE file for details.

## 👨‍💻 Author

Developed by [th-hoffmann](https://github.com/th-hoffmann) based on the practical Docker training by Denilson Bonatti from Digital Innovation One.

### ⭐ If this project was helpful, consider giving it a star!

🔙 [Back to top](#-docker-php-load-balancer-example)

---

## About

**Docker microservices demonstration with Nginx load balancing, PHP applications, and MySQL integration. Perfect for learning container orchestration and microservices architecture patterns.**

### Topics

`docker` `microservices` `nginx` `php` `mysql` `load-balancing` `containers` `devops` `architecture` `scalability` `high-availability` `web-development` `database-integration` `infrastructure` `automation` `orchestration` `networking`
