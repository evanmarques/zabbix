# Zabbix Documentation Lab

Documentação técnica estruturada para implantação, configuração e operação do Zabbix em ambiente Linux, organizada em camadas (infraestrutura, sistema, banco, aplicação e operação).

Este repositório não é apenas um guia de comandos — ele descreve arquitetura, decisões técnicas, fluxo de instalação e operação contínua do ambiente.

---

## 🎯 Objetivo

Centralizar e padronizar o conhecimento necessário para:

* Implantar o Zabbix do zero
* Entender a arquitetura da solução
* Reproduzir ambientes com consistência
* Facilitar troubleshooting
* Servir como material de estudo e referência profissional
* Evoluir para cenários produtivos

---

## 🧱 Arquitetura abordada

A documentação segue a arquitetura clássica de implantação do Zabbix:

Infraestrutura

↓

Sistema Operacional

↓

Banco de Dados

↓

Zabbix Server

↓

Frontend Web

↓

Agents / Monitoramento

Componentes principais:

* Infraestrutura → VM, rede, requisitos
* Sistema operacional → Ubuntu Server e dependências base
* Banco de dados → MySQL/MariaDB para persistência
* Zabbix Server → motor principal de coleta e processamento
* Frontend → interface web administrativa
* Agents → coleta de métricas dos hosts monitorados

---

## 🗂 Estrutura da documentação

A documentação será organizada em módulos independentes, permitindo leitura progressiva ou consulta pontual.

zabbix/

│

  ├── README.md

  │

  ├── 01-Infraestrutura

  ├── 02-Sistema-Operacional

  ├── 03-Banco-de-Dados

  ├── 04-Zabbix

  ├── 05-Operacao

  ├── 06-Seguranca

  │

  └── glossario

Cada diretório representa uma camada da solução.

---

## 📘 Como usar esta documentação

### 1) Implantação completa

Siga a ordem numérica dos diretórios:

1 → Infraestrutura
2 → Sistema operacional
3 → Banco de dados
4 → Zabbix
5 → Operação
6 → Segurança

---

### 2) Consulta técnica

Cada arquivo é independente.

Exemplo:

* erro de banco → consultar `03-Banco-de-Dados`
* erro de serviço → consultar `05-Operacao`
* firewall → consultar `06-Seguranca`

---

### 3) Estudo da arquitetura

Leia na ordem:

* conceitos
* decisões técnicas
* justificativas
* comandos

A documentação foi desenhada para explicar o porquê, não apenas o como.

---

## 🧠 Filosofia da documentação

Este repositório segue quatro princípios:

### 1) Modularidade

Cada camada é documentada separadamente.

### 2) Reprodutibilidade

Qualquer pessoa deve conseguir recriar o ambiente.

### 3) Clareza técnica

Nada é apenas “rodar comando”.

Sempre conterá:

* objetivo
* contexto
* justificativa
* execução

### 4) Evolução contínua

A doc crescerá para incluir:

* proxy
* alta disponibilidade
* docker
* kubernetes
* hardening
* automação

---

## 📚 Glossário técnico

Para evitar poluição da documentação principal, termos técnicos ficarão centralizados em:

/glossario

Exemplo de uso:

O Zabbix utiliza um Agent para coleta de métricas.
Veja: glossario/termos-zabbix.md#agent

---

## 🔧 Escopo atual

Este repositório cobre inicialmente:

* instalação base do Zabbix
* configuração em VM Linux
* banco MySQL/MariaDB
* frontend web
* primeiros agentes

---

## 🚧 Escopo futuro

Planejado para evolução:

* Zabbix Proxy
* monitoramento distribuído
* HA
* Docker
* Kubernetes
* automação com Ansible
* backup e restore estruturado
* observabilidade completa

---

## 👤 Público-alvo

* profissionais de infraestrutura
* sysadmins
* SRE
* estudantes de redes e Linux
* times de monitoramento
* ambientes corporativos

---

## ⚠️ Observações importantes

Esta documentação:

* não substitui documentação oficial do Zabbix
* complementa com experiência prática
* inclui troubleshooting real
* é baseada em ambiente de laboratório reproduzível

---

## 🧭 Próximos passos do repositório

A evolução seguirá esta ordem:

1. Infraestrutura
2. SO base
3. Banco
4. Instalação Zabbix
5. Configuração
6. Operação
7. Segurança
8. Troubleshooting
9. Automação

---

## 🤝 Contribuição

Sugestões, melhorias e ajustes são bem-vindos.

A ideia é transformar este material em:

* referência técnica
* base de runbook
* documentação profissional reutilizável
