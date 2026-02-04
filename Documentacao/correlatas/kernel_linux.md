# Kernel Linux

## O que é o Kernel Linux

O **kernel** é o núcleo do sistema operacional Linux.  
Ele é a camada mais baixa de software e é responsável por **intermediar tudo entre o hardware e os programas**.

No seu cenário com **Zabbix e Grafana**, absolutamente **nada funciona sem o kernel**.

---

## Funções técnicas do kernel

O kernel controla:
- CPU (escalonamento de processos)
- memória RAM
- acesso a disco
- rede (TCP/IP, sockets, portas)
- permissões e segurança

📌 Nenhum serviço (Zabbix, MySQL, Apache, Docker) acessa hardware diretamente.

---

## Kernel no monitoramento

Quando o Zabbix Agent coleta:
- uso de CPU
- memória
- disco
- processos

Ele está, na prática, **lendo informações expostas pelo kernel**.

Sem kernel:
- não há métricas
- não há rede
- não há processos

---

## Relação com troubleshooting

Problemas no kernel impactam:
- performance do host
- coleta de métricas
- estabilidade dos serviços

Por isso, monitorar kernel é sempre prioridade.
