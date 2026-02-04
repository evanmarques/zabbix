# Grafana

## O que é o Grafana

O **Grafana** é uma ferramenta de visualização de dados.

No seu cenário, ele é usado para:
- dashboards avançados
- visualizações customizadas
- consolidação de métricas

---

## Grafana com Zabbix

Grafana:
- NÃO acessa o banco do Zabbix
- NÃO lê arquivos do Zabbix

Ele consome dados via:
- API HTTP do Zabbix

---

## Grafana em Docker

No seu ambiente:
- Grafana roda em container
- escuta na porta 3000
- depende do Docker e da rede

---

## Papel no monitoramento

Grafana é a camada final:
- não coleta
- não processa
- apenas visualiza

Se cair:
- o Zabbix continua funcionando
- dashboards ficam indisponíveis
