# HomeLab Infrastructure: Hybrid Cloud & GitOps

Este repositório contém a infraestrutura como código (IaC) do meu laboratório pessoal, focado em práticas de DevOps, Cybersecurity e Cloud Híbrida. O projeto evoluiu de uma stack Docker tradicional rodando uma aplicação de backup de fotos(immich) para um cluster Kubernetes (K3s) orquestrado em um hardware físico (ThinkPad).

## 🏗️ Arquitetura Atual

O ambiente é composto por um servidor local integrado à Cloudflare para exposição segura de serviços.

- **Orquestração:** K3s (Lightweight Kubernetes)
- **Container Runtime:** Docker
- **Ingress Controller:** Traefik (nativo do K3s)
- **Segurança de Rede:** Cloudflare Tunnel (Zero Trust) para exposição de serviços sem abertura de portas no roteador.
- **Armazenamento:** RAID 1 local para persistência de dados críticos e resiliência de hardware.

## 🛠️ Tecnologias Utilizadas

- **Sistemas:** Linux (Ubuntu), K3s, Docker.
- **Redes:** Traefik Ingress, Cloudflare Zero Trust, AdGuard Home (DNS Sinkhole).
- **IaC & Configuração:** Kubernetes Manifests (YAML), Git, Terraform (em implementação).
- **Monitoramento:** Metrics Server (configurado), Uptime Kuma (deployment ativo).

## 📂 Estrutura do Repositório

- `/k8s`: Manifestos do Kubernetes divididos por namespaces.
  - `/management`: Ferramentas de suporte (Uptime Kuma, Ingress, etc).
- `/docker-compose`: Configurações legadas e serviços auxiliares (Immich, AdGuard).
- `/scripts`: Automações de correção de rede e manutenção do RAID.

## 🏁 Marcos Alcançados (Roadmap)

- [x] Configuração de Servidor Linux em hardware físico com RAID 1.
- [x] Implementação de Cloudflare Tunnel para acesso externo seguro (Zero Trust).
- [x] Instalação e provisionamento do cluster K3s.
- [x] Configuração de Metrics Server para telemetria de recursos.
- [x] Deploy do **Uptime Kuma** com Service e Ingress via Traefik.
- [ ] Implementação de Observabilidade com Prometheus & Grafana.
- [ ] Provisionamento de recursos em nuvem (AWS) via Terraform.
- [ ] Migrar a aplicação immich para o k3s com replicas e auto healing.

## 🛡️ Notas de Segurança (Hardening)

- **Secrets Management:** Nenhuma credencial sensível é armazenada no Git. Utilizei arquivos `.env` protegidos por `.gitignore` e exemplos documentados em `.env.example`.
- **Ingress Security:** As regras de Ingress são configuradas para validação de Host e integradas ao firewall da Cloudflare.
