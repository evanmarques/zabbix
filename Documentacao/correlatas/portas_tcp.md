# Portas TCP

## O que é uma porta TCP (definição técnica clara)

Uma **porta TCP** é um **identificador lógico numérico** usado para direcionar dados a um **processo específico** dentro de um sistema operacional.

Em termos diretos:

> A porta TCP diz ao sistema **qual serviço ou aplicação deve receber os dados** que chegaram a um IP.

Sem portas:
- vários serviços não poderiam coexistir no mesmo IP
- o sistema não saberia para qual processo entregar os dados

---

## Relação entre IP, porta e processo

Uma conexão TCP é sempre identificada pelo conjunto:

```
IP : PORTA
```

Exemplo:
```
192.168.1.10:3000
```

Tecnicamente:
- IP → identifica a máquina
- Porta → identifica o serviço/processo
- Processo → consome os dados

📌 **Uma porta nunca existe sozinha**.  
Ela sempre está associada a um **socket TCP criado por um processo**.

---

## Intervalos de portas (conceito importante)

As portas TCP vão de **0 a 65535**.

### 0 – 1023 → Portas bem conhecidas (privilegiadas)
- Requerem root para abrir
- Serviços padrão

Exemplos:
- 22 → SSH
- 80 → HTTP
- 443 → HTTPS

---

### 1024 – 49151 → Portas registradas
- Serviços de aplicações
- Muito usadas por softwares como Zabbix e Grafana

Exemplos:
- 3000 → Grafana
- 3306 → MySQL
- 10050 / 10051 → Zabbix

---

### 49152 – 65535 → Portas efêmeras
- Criadas dinamicamente pelo sistema
- Usadas pelo lado cliente das conexões

📌 Quando seu navegador acessa um site:
- ele usa uma porta efêmera local
- conecta na porta fixa do servidor

---

## Porta aberta ≠ serviço funcional

Esse é um erro clássico.

Um serviço pode:
- abrir a porta
- aceitar conexão TCP
- mas falhar internamente

Exemplos:
- banco sem acesso ao disco
- aplicação sem acesso ao banco
- erro de autenticação

Por isso, porta aberta é **condição necessária**, mas **não suficiente**.

---

## Porta, firewall e segurança

Portas são controladas por:
- firewall (iptables, nftables, ufw)
- regras de rede
- bind de endereço (0.0.0.0 vs 127.0.0.1)

Exemplo:
- `127.0.0.1:3306` → acessível só localmente
- `0.0.0.0:3306` → acessível pela rede

📌 Um serviço pode estar rodando corretamente, mas **inacessível externamente** por firewall.

---

## Portas no cenário Zabbix + Grafana

| Porta | Serviço | Função |
|-----|-------|-------|
| 22 | SSH | acesso administrativo |
| 80 | Apache | frontend Zabbix |
| 3000 | Grafana | dashboards |
| 3306 | MySQL | banco de dados |
| 10050 | Zabbix Agent | coleta de métricas |
| 10051 | Zabbix Server | processamento |

---

## Porta e Docker (ponto crítico)

Dentro de containers:
- serviços escutam portas internas
- o host **não vê essas portas automaticamente**

Exemplo:
```
-p 3000:3000
```

Significa:
- host:3000 → container:3000

Sem esse mapeamento:
- o serviço funciona
- mas é invisível externamente

---

## Definição curta (para hyperlink)

**Porta TCP**: identificador numérico associado a um socket TCP que direciona dados de rede a um processo específico dentro de um sistema.
