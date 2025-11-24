# Aula 06: Acesso Remoto e O Ambiente de Nuvem

## 1\. O Novo Cenário: Infraestrutura na Nuvem

Até agora, simulamos um servidor dentro do seu computador. Mas no mundo real, os servidores não ficam embaixo da sua mesa; eles ficam em Data Centers ao redor do mundo (Nuvem).

  * **O que muda hoje:**
      * Cada aluno receberá um **IP Público** (o endereço da sua casa na internet).
      * O servidor estará ligado 24h (enquanto durar o laboratório).
      * Não temos mais "telinha do VirtualBox". O acesso é 100% remoto via terminal.

-----

## 2\. O Protocolo SSH (Secure Shell)

Como controlamos um computador que está em outro país de forma segura? Usamos o **SSH**.

### O que é?

O SSH cria um "Túnel Criptografado" entre o seu computador (Cliente) e o Servidor na nuvem. Tudo o que você digita viaja protegido por esse túnel. Se um hacker interceptar a conexão, ele verá apenas lixo criptografado.

### Como usar (A Sintaxe Universal)

Não importa se você usa Windows (PowerShell/CMD), Mac ou Linux, o comando padrão hoje em dia é o mesmo:

```bash
ssh usuario@endereco_ip
```

  * **Exemplo:** `ssh aluno01@203.0.113.10`
  * **O "Aperto de Mão" (Fingerprint):** Na primeira vez que você conectar, o SSH vai perguntar: *"Não conheço esse servidor. Tem certeza que é ele?"*.
      * Você deve digitar `yes` e dar Enter. Isso salva a identidade do servidor no seu computador.

-----

## 3\. O Poder do `sudo` (SuperUser DO)

Ao entrar na VM da nuvem, você provavelmente logará com um usuário comum (ex: `ubuntu` ou `aluno`). Por segurança, esse usuário **não** tem poder total. Ele não pode instalar programas ou mudar configurações de rede diretas.

### Por que não logar direto como "root" (Chefe Supremo)?

Segurança e Rastreabilidade. Se todos usam a conta `root`, não sabemos quem apagou o banco de dados. Se cada um usa seu usuário e pede permissão (`sudo`), temos um registro (log).

### Como funciona?

Pense no `sudo` como um crachá temporário de gerente ou a palavra mágica "Simão Disse".

  * `apt update` -\> **Erro:** Permissão negada (Você é apenas um funcionário).
  * `sudo apt update` -\> **Sucesso:** O sistema pede sua senha, verifica se você é confiável na lista de "sudoers" e executa o comando com poderes de Root.

> **Regra de Ouro:** Só use `sudo` quando o comando realmente precisar alterar o sistema. Para criar arquivos na sua própria pasta, não use.

-----

## 4\. Copiando Arquivos: O Comando SCP

Muitas vezes você cria um script ou um arquivo de configuração no seu computador local e precisa enviá-lo para o servidor. Como não temos "Copiar e Colar" (Ctrl+C/Ctrl+V) de arquivos gráficos, usamos o **SCP** (Secure Copy).

Ele funciona sobre o mesmo túnel do SSH.

### A Lógica

```bash
scp [O QUE EU QUERO COPIAR] [PARA ONDE VAI]
```

### Exemplos Práticos

1.  **Do meu PC para o Servidor (Upload):**

    ```bash
    # Copia o arquivo 'index.html' para a pasta home do usuário na nuvem
    scp index.html aluno01@203.0.113.10:/home/aluno01/
    ```

    *Atenção aos dois pontos (`:`) que separam o IP da pasta de destino.*

2.  **Do Servidor para meu PC (Download):**

    ```bash
    # Traz o arquivo de log do servidor para a pasta atual (.) do meu PC
    scp aluno01@203.0.113.10:/var/log/syslog .
    ```

H (na nuvem) e verifique se o arquivo chegou:
        `ls -la` e `cat teste.txt`

-----

Com certeza. Para quem vem do Windows, a estrutura do Linux pode parecer bagunçada no início, mas ela é **extremamente organizada** e segue um padrão lógico (chamado FHS - Filesystem Hierarchy Standard).

Aqui está uma descrição didática das pastas que todo **DevOps** precisa conhecer para não apagar o que não deve.

---

# Principais Diretórios do Linux

### 1. O Início de Tudo
* **`/` (Root / Raiz):**
    * É a entrada do prédio. **Tudo** no Linux começa aqui. Se você apagar a `/`, o sistema operacional deixa de existir.

### 2. Onde moram as pessoas (Usuários)
* **`/home`:**
    * É o setor de **apartamentos dos usuários**.
    * Dentro dela, cada usuário tem sua pasta (ex: `/home/joao`, `/home/maria`).
    * *Analogia Windows:* É a pasta `C:\Users`.
    * **Regra:** Aqui é o único lugar onde o usuário comum manda.
* **`/root`:**
    * É a **cobertura do chefe**. É a pasta pessoal do "Super Usuário" (Administrador).
    * *Atenção:* Não confunda a pasta `/root` com a raiz `/`. A `/root` fica *dentro* da `/`.

### 3. Onde ficam os Programas (Comandos)
No Windows, os programas ficam em "Arquivos de Programas". No Linux, eles são divididos por função.
* **`/bin` (Binaries):**
    * Contém os comandos essenciais que **todos** os usuários podem usar (ex: `ls`, `cp`, `cat`, `mkdir`, `nano`).
* **`/sbin` (System Binaries):**
    * Contém comandos que só o **administrador** costuma usar para manutenção do sistema (ex: `fdisk` para formatar disco, `ifconfig` ou `ip` para rede).

### 4. O Cérebro do Sistema (Configurações)
* **`/etc`:**
    * **Importância Crítica para DevOps.**
    * Aqui ficam os arquivos de configuração de tudo. Se você instalou um servidor web (Nginx), a configuração estará em `/etc/nginx`. Se quer configurar o DNS, estará em `/etc/resolv.conf`.
    * *Analogia:* É o "Painel de Controle" ou o "Registro" do Windows, mas em forma de arquivos de texto.

### 5. Onde as coisas crescem e mudam (Variável)
* **`/var` (Variable):**
    * Aqui ficam arquivos que aumentam de tamanho ou mudam sozinhos com o tempo.
    * **`/var/log`:** Onde ficam os logs do sistema. Se algo der errado, é aqui que você procura.
    * **`/var/www`:** (Geralmente) Onde colocamos os sites/HTML para serem acessados na web.
    * **`/var/lib`:** Onde ficam os bancos de dados (MySQL/Postgres) armazenam seus dados brutos.

### 6. Outros Diretórios Importantes
* **`/tmp` (Temporário):**
    * Uma área de rascunho. Qualquer usuário pode gravar aqui.
    * *Detalhe:* Tudo que está aqui é **apagado automaticamente** quando o computador reinicia.
* **`/opt` (Opcional):**
    * Usado para instalar softwares "externos" que não vêm pelo gerenciador de pacotes oficial (ex: alguns agentes de monitoramento, ferramentas proprietárias).
* **`/mnt` e `/media`:**
    * Onde aparecem pen drives, HDs externos ou pastas compartilhadas de rede quando conectados.
* **`/dev` (Devices):**
    * O Linux trata hardware como se fosse arquivo. Aqui ficam as representações do seu disco rígido, processador, memória, etc. (Não mexa aqui a menos que saiba muito bem o que está fazendo).


---


Com certeza. Como a **Aula 06** é o momento em que eles acessam a nuvem via SSH, é natural que eles se sintam "perdidos" na tela preta.

Este **Complemento da Aula 06** serve como um guia de sobrevivência básica dentro do terminal. O foco aqui é **Navegação, Criação e Entendimento do Ambiente**.

-----

# Sobrevivência no Terminal Linux

Agora que você acessou o servidor remoto via SSH, você não tem mais o mouse para clicar em pastas. Você precisa "falar" com o sistema. Vamos entender a estrutura e os comandos essenciais.

## 1\. A Estrutura de Diretórios (Onde estou?)

Diferente do Windows, o Linux não tem `C:` ou `D:`. Tudo começa na **Raiz** (Root), representada pela barra `/`.

Imagine uma árvore de cabeça para baixo.

### As Pastas Mais Importantes para Agora:

  * **`/` (Root):** O topo da árvore. Só o administrador (root) pode escrever aqui.
  * **`/home/nome_do_usuario`:** A "Sua Casa". É o único lugar onde você tem permissão total para criar e apagar arquivos sem usar `sudo`. (Equivalente ao `C:\Users\Nome` do Windows).
  * **`/bin` e `/usr/bin`:** Onde ficam os programas (comandos) como `ls`, `cp`, `mkdir`.
  * **`/etc`:** Onde ficam as configurações do sistema (ex: configuração de rede).

-----

## 2\. Comandos de Navegação e Criação

Aqui está o "Kit Básico" para se mover e criar coisas.

### `pwd` (Print Working Directory)

  * **Função:** O seu GPS. Diz exatamente onde você está na árvore.
  * **Exemplo:**
    ```bash
    pwd
    # Saída: /home/ubuntu
    ```

### `cd` (Change Directory)

  * **Função:** O teletransporte. Muda você de pasta.
  * **Truques:**
      * `cd /` : Vai para a raiz.
      * `cd ~` (til) : Volta para a sua casa (home), não importa onde você esteja.
      * `cd ..` (dois pontos) : Volta um nível para trás (sai da pasta atual).
      * `cd -` (hífen) : Volta para a última pasta onde você estava (igual botão "voltar" do controle remoto).

### `touch`

  * **Função:** Cria um arquivo vazio instantaneamente. Ótimo para testar se você tem permissão de escrita numa pasta.
  * **Exemplo:** `touch teste.txt`

### `cat` (Concatenate)

  * **Função:** Lê o conteúdo de um arquivo e joga na tela.
  * **Exemplo:** `cat /etc/os-release` (Mostra qual versão do Linux está rodando).

-----

## 3\. O Editor de Texto: `nano`

No servidor, não temos Bloco de Notas ou VS Code visual. Usamos editores de terminal. O mais amigável para iniciantes é o **Nano**.

  * **Abrir/Criar:** `nano meu_arquivo.txt`

**A Tela do Nano:**
Você pode digitar normalmente. A parte difícil para iniciantes é **sair e salvar**. Olhe para o rodapé da tela do nano, ele mostra os atalhos. O acento circunflexo `^` significa a tecla **CTRL**.

**Cheat Sheet do Nano (Passo a Passo para Salvar):**

1.  Escreva seu texto.
2.  Para sair, pressione **`Ctrl + X`**.
3.  Ele vai perguntar: *"Save modified buffer?"* (Salvar alterações?).
4.  Digite **`Y`** (Yes) ou **`S`** (Sim, dependendo da língua).
5.  Ele vai perguntar o nome do arquivo. Apenas aperte **`Enter`**.

-----

## 4\. Variáveis de Ambiente e o `$PATH`

Isso confunde muita gente, mas é essencial para DevOps.

### O que são Variáveis de Ambiente?

São "etiquetas" que o sistema operacional guarda na memória para saber como se comportar. Elas são escritas em LETRA\_MAIUSCULA.

  * **Ver todas:** Digite `env`
  * **Ver uma específica:** Digite `echo $NOME_DA_VARIAVEL` (O `$` avisa que queremos o valor, não o nome).

### A Variável Mais Importante: `$PATH`

Você já se perguntou por que você digita apenas `ls` e o comando funciona? Por que você não precisa digitar o caminho completo `/usr/bin/ls`?

**Resposta:** Por causa do **PATH**.

O **PATH** é uma lista de pastas onde o Linux deve procurar pelos comandos.

**Exemplo prático:**
Quando você digita `nano`, o Linux faz o seguinte:

1.  Olha no `$PATH`.
2.  "O nano está na pasta `/usr/local/sbin`? Não."
3.  "Está na pasta `/usr/local/bin`? Não."
4.  "Está na pasta `/usr/bin`? **Sim\! Achei.** Executando..."

**Como ver seu PATH:**

```bash
echo $PATH
# Saída: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

> **Por que isso importa para o curso?**
> Quando criarmos scripts, se eles não estiverem em uma pasta listada no PATH, o Linux não os achará apenas pelo nome. Por isso, para rodar um script na pasta atual, temos que ser explícitos e usar `./meu_script.sh` ("No diretório atual ponto, rode esse script").

-----

## 5\. Prática Rápida (Desafio para os Alunos)

Peça para executarem essa sequência para fixar o conteúdo:

1.  Descubra onde você está (`pwd`).
2.  Vá para a raiz do sistema (`cd /`) e liste os arquivos (`ls`).
3.  Tente criar um arquivo na raiz (`touch teste_raiz.txt`). **Vai dar erro de permissão\!** (Ótimo para mostrar segurança).
4.  Volte para sua casa (`cd ~`).
5.  Crie um arquivo chamado `lab06.txt` usando o `nano`.
6.  Escreva dentro dele: "Minha primeira edição na nuvem".
7.  Salve e saia (`Ctrl+X`, `Y`, `Enter`).
8.  Leia o arquivo para confirmar (`cat lab06.txt`).
