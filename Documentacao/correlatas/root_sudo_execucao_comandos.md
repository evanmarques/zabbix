# Root, sudo e execução de comandos

## O que é o usuário root

O **root** é o superusuário do Linux.  
Ele possui **privilégios totais** sobre o sistema operacional.

Tecnicamente, isso significa:
- pode ler e escrever qualquer arquivo
- pode iniciar, parar e matar qualquer processo
- pode instalar ou remover qualquer software
- pode alterar configurações críticas do sistema

📌 Não existe confirmação extra para ações do root.  
Se o comando for executado, o sistema obedece.

---

## Por que root é necessário no monitoramento

No cenário **Zabbix + Grafana**, root é exigido porque:

- instalar Zabbix, MySQL, Apache e Docker altera o sistema
- serviços precisam abrir **portas TCP** (10050, 10051, 80, 3000)
- arquivos em **/etc** precisam ser editados
- serviços precisam ser controlados pelo **systemd**

Tudo isso é **bloqueado para usuários comuns**.

---

## O que é sudo

O **sudo** (Super User DO) permite que:
- um usuário comum execute **um comando específico** como root

Exemplo:
```
sudo apt install zabbix-server-mysql
```

Aqui:
- você continua sendo usuário normal
- apenas esse comando roda como root

---

## Diferença prática: sudo vs root

### sudo
- mais seguro
- reduz risco de erro grave
- cada comando é explícito

### root direto (sudo -i)
- acesso total contínuo
- mais perigoso para iniciantes
- qualquer erro afeta o sistema inteiro

📌 Em ambientes profissionais e provas práticas, **sudo é preferido**.

---

## sudo -i (modo root interativo)

O comando:
```
sudo -i
```

Abre uma sessão completa como root.

Indicadores:
- prompt muda de `$` para `#`
- todos os comandos têm poder total

Para sair:
```
exit
```

---

## Execução de comandos no Linux

Cada comando executado envolve:
1. permissão do usuário
2. acesso a arquivos/binários
3. interação com kernel ou serviços

Exemplo:
```
sudo systemctl restart zabbix-server
```

Fluxo real:
- sudo valida permissão
- systemctl fala com systemd
- systemd reinicia o processo
- kernel executa a ação

---

## Riscos reais ao usar root

Erros comuns:
- apagar arquivos críticos
- sobrescrever configs
- derrubar serviços essenciais

Por isso:
- use sudo sempre que possível
- edite arquivos conscientemente
- evite copiar comandos sem entender

---

## Conclusão

Root não é opcional no monitoramento.  
Mas **controle de privilégio** é sinal de maturidade técnica.

Entender quando e por que usar sudo é parte fundamental do Linux profissional.
