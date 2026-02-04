# systemd

## O que é o systemd

O **systemd** é o gerenciador de serviços do Linux moderno.

Ele é responsável por:
- iniciar serviços no boot
- parar, iniciar e reiniciar processos
- manter serviços rodando

---

## systemd no Zabbix e Grafana

Todos os serviços abaixo são controlados pelo systemd:
- zabbix-server
- zabbix-agent
- mysql
- apache2
- docker

Quando você usa:
```
systemctl start zabbix-server
```
Você está falando com o systemd, não com o Zabbix diretamente.

---

## systemd e dependências

O systemd garante que:
- o banco suba antes do Zabbix
- a rede esteja ativa antes dos serviços

Sem systemd:
- inicialização seria manual
- serviços não sobreviveriam a reboot
