# MySQL

## O que é o MySQL

O **MySQL** é o banco de dados usado pelo Zabbix para armazenar tudo.

Ele guarda:
- métricas
- histórico
- tendências
- usuários
- configurações

---

## MySQL no Zabbix

O Zabbix:
- não grava dados em arquivos próprios
- não mantém estado em memória apenas

Tudo passa pelo banco.

---

## Armazenamento

Os dados ficam fisicamente em:
```
/var/lib/mysql
```

Esse diretório é crítico:
- backups são essenciais
- apagar significa perder histórico

---

## Impacto no monitoramento

Banco lento ou indisponível:
- Zabbix trava
- frontend fica lento
- Grafana não carrega dados
