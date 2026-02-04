# Zabbix Server

## O que é o Zabbix Server

O **Zabbix Server** é o cérebro do sistema de monitoramento.

Ele é responsável por:
- receber métricas
- processar triggers
- gerar alertas
- gravar dados no banco

---

## Funcionamento técnico

- roda como processo residente
- escuta na porta TCP 10051
- comunica-se com agentes e proxies
- depende totalmente do banco de dados

📌 Sem MySQL, o Zabbix Server não funciona.

---

## Papel no seu ambiente

No seu cenário:
- agentes enviam dados
- server processa
- frontend e Grafana consomem resultados

Ele é o ponto central da arquitetura.
