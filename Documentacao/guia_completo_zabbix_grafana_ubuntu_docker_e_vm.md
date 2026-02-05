# Guia Completo e Extremamente Didático — Zabbix 6.0 + Grafana (Linux)

> **Objetivo**  
Este documento existe para eliminar o "copiar e colar sem entender". Aqui cada comando vem acompanhado de **explicação técnica**, **motivo de uso**, **impacto no sistema**, **dependências** e **erros comuns**.

Se você seguir este guia, você não estará apenas instalando Zabbix e Grafana — você estará **aprendendo como Linux, serviços, rede, banco de dados e containers realmente funcionam juntos**.

Perfil: **iniciante absoluto**, mas com mentalidade profissional.


### 🧠 Como ler este guia (muito importante)

Para cada comando, responda mentalmente:
- O que esse comando cria, altera ou inicia?
- Esse comando mexe em disco, memória, rede ou processo?
- Se eu desligar o servidor agora, isso persiste?


### 🧭 Arquitetura COMPLETA (nível sistema)

[ Kernel Linux ] ~ [Clique aqui para saber mais sobre Kernel](correlatas/kernel_linux.md)
      ↑
      
[ Serviços (systemd) ] ~ [Clique aqui para saber mais sobre SystemD](correlatas/systemd.md)
      ↑
      
[ Zabbix Server ] ←→ [ MySQL ] ~ [Clique aqui para saber mais sobre MySQL](correlatas/mysql.md)
      ↑                 ↑
      
[ Zabbix Agent ] Arquivos /var/lib/mysql
      ↑
      
[ Host Monitorado ]


[ Apache + PHP ] → lê dados do banco ~ [Clique aqui para saber mais sobre Frontend Zabbix](correlatas/frontend_zabbix.md)

[ Grafana (Docker) ] → consome API do Zabbix ~ [Clique aqui para saber mais sobre Grafana](correlatas/grafana.md)


📌 **Nada se comunica "magicamente"**. Tudo passa por:
- Sockets ~ [Clique aqui para saber mais sobre Sockets](correlatas/sockets.md)
- portas TCP ~ [Clique aqui para saber mais sobre TCP](correlatas/portas_tcp.md)
- arquivos de configuração ~ [Clique aqui para saber mais sobre Arquivos de configuração](correlatas/arquivos_de_configuracao.md)


# 🗂️ ABA 0 — Root, sudo e execução de comandos

## 🔑 Por que root é necessário?

No Linux, somente o root pode:
- instalar pacotes
- abrir portas
- iniciar serviços
- alterar arquivos em /etc

[CLique aqui para saber mais sobre ROOT](correlatas/root_sudo_execucao_comandos.md)

🧠 Observação importante

Este arquivo já conversa diretamente com outros que você tem:

- systemd.md → quando fala de controle de serviços
- kernel_linux.md → quando explica quem realmente executa a ação
- futuramente → permissões, ownership, chmod, chown

### sudo

```
sudo apt update
```

**Tecnicamente:**
- `sudo` cria um processo temporário com UID 0 (root)
- esse processo executa **apenas esse comando**

Se remover o sudo → erro de permissão.

---

# 🗂️ ABA 1 — MySQL (nível serviço + armazenamento)

## 1️⃣ Instalação

```
sudo apt install -y mysql-server
```

**O que acontece por baixo:**
- binário `mysqld` é instalado
- diretório `/var/lib/mysql` é criado
- serviço `mysql.service` é registrado no systemd

---

## 2️⃣ systemctl start / enable

```
sudo systemctl start mysql
```

- cria um **processo residente na memória**
- abre socket local `/var/run/mysqld/mysqld.sock`

```
sudo systemctl enable mysql
```

- cria link simbólico em `/etc/systemd/system/`
- garante start automático

---

## 3️⃣ Acesso via socket

```
sudo mysql
```

**Por quê funciona sem senha?**
- MySQL confia no usuário do sistema (root)
- autenticação por socket = mais segura localmente

---

# 🗂️ ABA 2 — Zabbix (nível aplicação)

## Repositório

```
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_6.0+ubuntu24.04_all.deb
```

- baixa um pacote `.deb`
- não instala Zabbix ainda

```
sudo dpkg -i zabbix-release_latest_6.0+ubuntu24.04_all.deb
```

- adiciona arquivos em `/etc/apt/sources.list.d/`

```
apt update
```
- atualiza os pacotes instalados
---

## Importação do schema

```
zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix
```

**Fluxo real:**
- arquivo SQL → STDOUT
- pipe `|` → STDIN do mysql
- mysql grava tabelas em disco

Se falhar aqui:
- banco existe
- Zabbix não sobe

---

# 🗂️ ABA 3 — Grafana com Docker (nível container)

## 🧠 Conceito fundamental: container NÃO é VM

- compartilha kernel do host
- isola processo, rede e filesystem

---

## 1️⃣ Instalar Docker

```
sudo apt install -y docker.io
```

Instala:
- daemon `dockerd`
- cliente `docker`

```
sudo systemctl start docker
```

- daemon começa a escutar `/var/run/docker.sock`

---

## 2️⃣ docker run (linha por linha, profundamente)

```
docker run -d \
  --name grafana \
  -p 3000:3000 \
  --restart unless-stopped \
  grafana/grafana-enterprise
```

### docker run
- cria **e** inicia container

### -d
- processo roda em background
- STDOUT vai para logs do Docker

### --name grafana
- cria nome lógico
- evita usar ID aleatório

### -p 3000:3000
- NAT de porta
- host:3000 → container:3000

Se remover isso:
- Grafana sobe
- mas ninguém acessa

### --restart unless-stopped
- Docker registra política de restart
- após reboot, container sobe sozinho

### imagem grafana/grafana-enterprise
- Docker busca no Docker Hub
- baixa camadas (layers)
- cria filesystem isolado

---

## 3️⃣ Persistência (ponto crítico)

Sem volume:
- dashboards se perdem ao recriar container

(Boas práticas ficam para aba avançada)

---

# 🗂️ ABA 4 — Plugin Zabbix no Grafana (nível API)

```
docker exec -it grafana grafana-cli plugins install alexanderzobnin-zabbix-app
```

**Tecnicamente:**
- `exec` entra no container
- `-it` cria terminal interativo
- `grafana-cli` altera diretório interno `/var/lib/grafana/plugins`

```
docker restart grafana
```

- reinicia processo PID 1 do container

---

## Comunicação Grafana ↔ Zabbix

- NÃO acessa banco
- NÃO lê arquivos
- Usa HTTP API

Por isso:
- URL termina em `/zabbix`

---

# 🗂️ ABA 5 — Reset de senha (nível banco)

```
UPDATE users SET passwd = MD5('NovaSenha')
```

- altera hash
- frontend compara hash, não senha pura

---

# 🗂️ ABA 6 — Portas, rede e firewall

- 10050 → agent
- 10051 → server
- 3306 → MySQL
- 80 → Apache
- 3000 → Grafana

Se algo não conecta → pense em porta.

---

## ✅ Conclusão real

Agora você entende:
- processos
- serviços
- containers
- banco
- rede

Isso é **base sólida de infraestrutura**.

