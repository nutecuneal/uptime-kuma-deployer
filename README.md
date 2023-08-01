# Uptime Kuma Deployer

O [Uptime Kuma](https://uptime.kuma.pet) é uma ferramenta de monitoramento projetada para ser uma maneira fácil de monitorar HTTP(s), TCP, HTTP(s) Keyword, Ping, DNS Record, Push, Steam Game Server e Containers Docker.

## Sumário

- [Uptime Kuma Deployer](#uptime-kuma-deployer)
  - [Sumário](#sumário)
  - [1. Requisitos e Dependências](#1-requisitos-e-dependências)
  - [2. Instalação](#2-instalação)
    - [Diretórios](#diretórios)
    - [Docker-Compose](#docker-compose)
      - [Portas](#portas)
      - [Volumes](#volumes)
      - [Rede](#rede)
        - [Proxy Reverso](#proxy-reverso)

## 1. Requisitos e Dependências

- [Docker e Docker-Compose](https://docs.docker.com/)

## 2. Instalação

### Diretórios

```bash
# Crie os diretórios.

# Dir. Data
$ mkdir $(pwd)/data
```

### Docker-Compose

#### Portas

```yml
# (docker-compose|stack.docker-compose).yml (Em services.app)

# Descomente (e/ou altere) as portas/serviços que você deseja oferecer.

ports:
# Porta Web (HTTP)
  - 3001:3001
```

Obs: não recomendado o uso da **Porta Web** via HTTP, use um proxy reverso no local com HTTPS. Por isso, só descomente essa instrução se realmente souber o que está fazendo.

#### Volumes

```yml
# (docker-compose|stack.docker-compose).yml (Em services.app)

# Aponte para as pastas criadas anteriormente.

# Antes
volumes:
  - $(pwd)/lib_upkdata:/app/data

# Depois (exemplo)
volumes:
  - /var/lib/uptime-kuma:/app/data
```

#### Rede

```yml
# docker-compose.yml (Em networks.uptime-kuma-net.ipam)

# Altere o valor caso necessário. 

config:
# Endereço da rede
  - subnet: '172.18.0.0/28'
```

##### Proxy Reverso

```yml
# docker-compose.yml (Em networks)

# Ajuste o campo "name" para ingressar na rede do seu proxy reverso.

reverse-proxy:
  name: 'reverse-proxy'
  external: true
```