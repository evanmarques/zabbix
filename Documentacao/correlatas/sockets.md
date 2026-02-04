# Sockets

## O que é um socket (definição técnica clara)

Um **socket** é um **endpoint de comunicação** criado por um processo para **enviar e receber dados**.

Em termos simples e corretos:

> Um socket é o **meio pelo qual dois processos trocam informações**, seja no mesmo sistema ou pela rede.

Sem socket:
- processos **não conversam**
- serviços **não recebem requisições**
- não existe cliente ↔ servidor

---

## Onde o socket existe no sistema

Um socket **sempre pertence a um processo**.

Quando um serviço inicia, ele normalmente:
1. sobe um processo
2. cria **um ou mais sockets**
3. começa a escutar conexões

Esse socket pode existir como:
- **arquivo** no sistema
- **porta de rede** (TCP/UDP)

---

## Tipos de socket (os que realmente importam)

### Unix Socket (socket de arquivo)

Exemplo real:
```
/var/run/mysqld/mysqld.sock
```

**Características técnicas**
- Existe como **arquivo especial** no filesystem
- Comunicação **local**, dentro do mesmo host
- Não usa IP
- Não passa pela rede
- Extremamente rápido
- Controlado por permissões de arquivo (chmod, chown)

**Quem usa**
- MySQL local
- PostgreSQL local
- systemd
- Docker
- PHP-FPM

**Exemplo prático (MySQL)**

Ao executar:
```
sudo mysql
```

O cliente:
1. localiza o socket padrão
2. abre o arquivo `.sock`
3. envia comandos diretamente ao processo `mysqld`

Se esse arquivo **não existir**:
- o serviço MySQL não está rodando
- ou falhou ao iniciar

---

### Socket de rede (TCP)

Exemplos:
```
127.0.0.1:3306
0.0.0.0:3000
```

Características:
- Não é um arquivo visível
- Existe na pilha de rede do kernel
- Está associado a uma **porta TCP**
- Permite comunicação local ou remota

Usado quando:
- há acesso via navegador
- comunicação entre VMs
- comunicação entre containers
- comunicação entre hosts distintos

---

## Socket ≠ Serviço

- **Serviço** → programa/processo em execução
- **Socket** → ponto de entrada e saída desse serviço

Um serviço pode estar rodando e:
- não criar socket (erro de configuração)
- criar socket, mas não responder corretamente

---

## Segurança relacionada a sockets

Sockets são protegidos por:
- permissões de arquivo (Unix socket)
- firewall, ACL e autenticação (TCP)

Exemplos:
- MySQL via socket → controlado por permissões do sistema
- MySQL via TCP → controlado por usuário, senha e firewall

---

## Relação com Zabbix e Grafana

| Serviço | Tipo de socket |
|-------|----------------|
| MySQL local | Unix socket |
| Zabbix Server | TCP |
| Zabbix Agent | TCP |
| Apache | TCP |
| Grafana | TCP |

---

## Definição curta (para hyperlink)

**Socket**: ponto de comunicação criado por um processo para permitir troca de dados, podendo ser local (Unix socket) ou via rede (TCP).
