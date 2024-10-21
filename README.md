# Projeto Korp

Este projeto implementa um servidor proxy reverso utilizando Nginx e Docker, redirecionando requisições HTTP da porta 80 para um container http-https-echo na porta 8080.

## Estrutura do Projeto

```
korp/
├── nginx.conf.d/
│   └── http-https-echo.conf
├── playbook.yml
└── docker-compose.yml
```

## Pré-requisitos

- Ubuntu 24.04
- Ansible Core 2.16 (opcional se já tiver Docker instalado)
- Docker 27.3.1
- Docker Compose 1.28.5

## Configuração e Instalação

Existem duas maneiras de executar este projeto:

### 1. Se você já tem Docker e Docker Compose instalados

1. Clone este repositório
2. Navegue até o diretório do projeto
3. Execute:
   ```bash
   docker compose up -d
   ```

### 2. Instalação completa via Ansible (apenas Ubuntu)

Se você precisa instalar todas as dependências:

1. Clone este repositório
2. Navegue até o diretório do projeto
3. Execute:
   ```bash
   ansible-playbook --ask-become-pass playbook.yml
   ```

## Testando a Instalação

Após a instalação, você pode testar o funcionamento do proxy reverso executando:

```bash
curl localhost:80
```

A resposta deve ser um json gerado pelo container http-https-echo.

## Componentes do Projeto

### nginx.conf.d/http-https-echo.conf
Arquivo de configuração do Nginx que implementa o proxy reverso, redirecionando todas as requisições da porta 80 para o container http-https-echo na porta 8080.

### playbook.yml
Playbook Ansible que automatiza a instalação e configuração de:
- Docker
- Docker Compose
- Dependências necessárias
- Execução do docker-compose.yml

### Volume
O diretório `nginx.conf.d` é montado como um volume no container Nginx, permitindo a configuração dinâmica do proxy reverso.

## Informações Técnicas

- **Proxy Reverso**: Todas as requisições HTTP na porta 80 são redirecionadas automaticamente para o serviço http-https-echo na porta 8080
- **Containers**: O projeto utiliza dois containers Docker:
  - Nginx: Servidor proxy reverso
  - http-https-echo: Serviço de eco HTTP/HTTPS

## Solução de Problemas

Se encontrar problemas durante a instalação ou execução:

1. Verifique se as portas 80 e 8080 não estão em uso
2. Certifique-se de que todos os serviços Docker estão em execução
3. Verifique os logs dos containers:
   ```bash
   docker logs <nome-do-container>
   ```

## Notas de Versão

- Testado no Ubuntu 24.04
- Ansible Core 2.16
- Docker 27.3.1
- Docker Compose 1.28.5