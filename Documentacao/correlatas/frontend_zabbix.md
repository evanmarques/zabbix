# Frontend Zabbix (Apache + PHP)

## O que é o Frontend

O frontend é a **interface web** do Zabbix.

Ele permite:
- visualizar métricas
- criar hosts e itens
- configurar triggers
- gerenciar usuários

---

## Componentes

Apache:
- servidor HTTP
- recebe requisições do navegador

PHP:
- executa o código do frontend
- consulta dados no banco

---

## O que o frontend NÃO faz

- não coleta métricas
- não processa triggers
- não armazena dados

Ele apenas **exibe informações** já processadas.

---

## Relação com o seu ambiente

Se o frontend cair:
- o monitoramento continua
- mas você perde visibilidade
