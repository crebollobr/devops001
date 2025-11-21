# Aula 04: Gerenciamento do Sistema Operacional

## 1. Gerenciamento de Aplicativos (O mundo `apt`)

No Windows, estamos acostumados a baixar um `.exe` de um site qualquer e instalar. No Linux (especialmente Servidores), isso é considerado má prática e inseguro. Nós usamos **Gerenciadores de Pacotes**.

### O Conceito de Repositórios
Imagine que o Linux tem uma "App Store" oficial, segura e auditada, mas sem ícones coloridos. Chamamos isso de **Repositórios**.
O comando `apt` (Advanced Package Tool) é o "balconista" que vai até o depósito buscar o software para você.



### O Ciclo de Vida da Instalação

Existem 4 comandos que você usará todos os dias. É importante explicar a diferença entre *update* e *upgrade*.

1.  **`sudo apt update`**
    * **O que faz:** *Não atualiza os programas!* Ele apenas baixa a **lista** mais recente de softwares disponíveis. É como pegar o catálogo novo do supermercado para ver os preços atuais.
    * *Regra:* Sempre rode isso antes de tentar instalar qualquer coisa.

2.  **`sudo apt upgrade`**
    * **O que faz:** Agora sim, ele olha o que você tem instalado, compara com a lista nova e atualiza as versões dos programas.

3.  **`sudo apt install nome_do_pacote`**
    * **O que faz:** Baixa e instala um programa (e todas as dependências necessárias).
    * *Exemplo:* `sudo apt install git` ou `sudo apt install htop`.

4.  **`sudo apt remove nome_do_pacote`**
    * **O que faz:** Desinstala o programa.

---

## 2. Rede do Linux (Nível Básico)

Como os alunos ainda não tiveram a aula de teoria de redes (TCP/IP, máscaras, gateways), o foco aqui é **Verificação** e **Diagnóstico Simples**.

> "O servidor tem internet? Qual é o endereço dele?"

### Descobrindo meu Endereço (IP)
Antigamente usava-se o `ifconfig`, mas ele foi substituído. O padrão moderno é o comando `ip`.

* **Comando:** `ip addr` (ou `ip a`)
* **O que procurar:**
    * Interface `lo` (Loopback): É o endereço interno (127.0.0.1). Ignore por enquanto.
    * Interface `eth0` ou `enp0s3` (Ethernet): Esta é sua placa de rede. Procure a palavra `inet` seguida de números (ex: `192.168.0.15`). Esse é o endereço do seu servidor.

### Testando a Conexão (Ping)
Como saber se o servidor consegue "falar" com o mundo exterior? Usamos o **Ping** (igual a um sonar de submarino).

* **Comando:** `ping google.com`
* **O que significa:**
    * Se aparecerem linhas com `time=xx ms`, a internet está funcionando.
    * Se travar ou der `Destination Host Unreachable`, você está sem rede.
* **Dica:** No Linux, o ping é infinito. Use **Ctrl + C** para parar.

### Onde fica a configuração? (Apenas visualização)
No Ubuntu moderno, a configuração de rede é feita pelo **Netplan**.
* **Arquivo:** `/etc/netplan/00-installer-config.yaml` (ou similar).
* *Ação:* Apenas mostre o arquivo com `cat`. Explique que ali definimos se o IP é fixo ou automático (DHCP). Não edite agora para não quebrar a VM dos alunos antes da aula de redes.

---

## 3. Configurações Gerais e Monitoramento

Um bom admin precisa saber cuidar da saúde da máquina.

### Monitoramento de Processos ("Gerenciador de Tarefas")
O servidor está lento? Quem está comendo toda a memória?

* **Comando:** `top`
    * Mostra uma lista em tempo real dos processos, uso de CPU e Memória RAM.
* **Comando Melhorado:** `htop`
    * (Geralmente precisa instalar: `sudo apt install htop`). É mais colorido, interativo e fácil de ler.



### Espaço em Disco
O disco encheu?

* **Comando:** `df -h`
    * `df`: Disk Free.
    * `-h`: Human Readable (converte números gigantes de bytes para MB ou GB).
    * Olhe a coluna **Use%** da raiz `/`.

### Gerenciamento de Usuários
Às vezes você precisa criar um usuário para um colega ou para um serviço específico.

* **Criar usuário:** `sudo adduser nome_do_usuario` (Seguir os passos na tela).
* **Trocar de usuário:** `su - nome_do_usuario` (Switch User).
* **Mudar senha:** `sudo passwd nome_do_usuario`.
* **Alterar o nome da máquina (Hostname):**
    * Comando: `sudo hostnamectl set-hostname novo-nome`
    * *Por que?* Importante para identificar servidores em um cluster (ex: `web-01`, `db-01`).

---

## 4. Resumo da Aula (Cheat Sheet)

| Ação | Comando |
| :--- | :--- |
| Atualizar lista de repositórios | `sudo apt update` |
| Instalar programa | `sudo apt install [programa]` |
| Ver meu IP | `ip addr` |
| Testar internet | `ping google.com` |
| Ver uso de CPU/RAM | `top` ou `htop` |
| Ver espaço em disco | `df -h` |
| Criar novo usuário | `sudo adduser [nome]` |

---

### Sugestão de Exercício Prático para a aula:
1.  Atualizar os repositórios (`update`).
2.  Instalar o pacote `htop` e o `net-tools`.
3.  Descobrir o IP da máquina.
4.  Verificar o espaço em disco disponível.
5.  Rodar o `htop` e identificar quanto de memória RAM está sendo usada.
