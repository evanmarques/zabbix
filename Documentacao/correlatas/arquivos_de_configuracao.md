# Arquivos de Configuração

## O que são arquivos de configuração (definição técnica clara)

Arquivos de configuração são **arquivos de texto** que dizem a um programa **como ele deve se comportar**.

Eles não executam código, mas **controlam o funcionamento** do código.

Em termos diretos:

> Um arquivo de configuração é o contrato entre o administrador e o software.

Sem configuração:
- o serviço não sabe onde escutar
- não sabe com quem se conectar
- não sabe onde gravar dados ou logs

---

## Onde ficam os arquivos de configuração no Linux

Por padrão, no Linux:

```
/etc/
```

É o diretório que concentra **configurações do sistema e serviços**.

📌 Regra geral:
- `/etc` → configuração
- `/usr/bin` → executáveis
- `/var/lib` → dados persistentes
- `/var/log` → logs

---

## Como um serviço usa um arquivo de configuração

Fluxo real ao iniciar um serviço:

1. systemd inicia o processo
2. o binário do serviço é carregado
3. o serviço lê seu arquivo de configuração
4. valida parâmetros
5. cria sockets / portas
6. inicia execução normal

Se a configuração estiver errada:
- o serviço pode **nem subir**
- ou subir e **cair imediatamente**
- ou subir “quebrado”

---

## Arquivos de configuração NÃO são mágicos

Eles só funcionam se:
- o caminho estiver correto
- a sintaxe estiver correta
- o usuário tiver permissão de leitura
- os valores fizerem sentido

Erro comum:
- editar o arquivo errado
- esquecer de reiniciar o serviço

---

## Exemplos críticos no Zabbix + Grafana

### Zabbix Server

```
/etc/zabbix/zabbix_server.conf
```

Controla:
- acesso ao banco
- cache
- portas
- paths internos

Exemplo:
```
DBName=zabbix
DBUser=zabbix
DBPassword=SenhaForteAqui
```

📌 Se errar a senha:
- processo inicia
- falha ao conectar
- encerra

---

### Zabbix Agent

```
/etc/zabbix/zabbix_agentd.conf
```

Controla:
- IP do server
- hostname reportado
- itens permitidos

Erro comum:
- Server não autorizado → dados rejeitados

---

### Apache (Frontend)

```
/etc/zabbix/apache.conf
```

Controla:
- timezone
- integração PHP
- frontend do Zabbix

Sem timezone:
- erros no frontend
- gráficos desalinhados

---

### Grafana (container)

Dentro do container:

```
/etc/grafana/grafana.ini
```

Controla:
- porta interna
- autenticação
- banco interno
- plugins

📌 Em Docker, configurações vivem **dentro do container** se não houver volume.

---

## Configuração ≠ aplicação imediata

Depois de alterar um arquivo:

```
sudo systemctl restart SERVIÇO
```

Ou, em Docker:

```
docker restart CONTAINER
```

Sem restart:
- o processo antigo continua usando config antiga

---

## Arquivos de configuração e troubleshooting

Perguntas-chave:
1. O arquivo certo foi editado?
2. A sintaxe está correta?
3. O serviço foi reiniciado?
4. O log aponta erro de configuração?

Logs costumam indicar:
- linha do erro
- parâmetro inválido

---

## Segurança em arquivos de configuração

Arquivos podem conter:
- senhas
- tokens
- chaves

Por isso:
- permissões importam
- acesso deve ser restrito

Exemplo:
```
-rw------- root root
```

---

## Definição curta (para hyperlink)

**Arquivo de configuração**: arquivo de texto que define parâmetros de funcionamento de um serviço, controlando comportamento, conexões, portas e recursos usados.
