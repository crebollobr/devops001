# Aula 06: Ambiente Cloud, Acesso Remoto e Sobrevivência Linux

## 1\. O Novo Cenário: Infraestrutura na Nuvem

Até agora, simulamos um servidor dentro do seu computador (VirtualBox). Mas no mundo real, os servidores ficam em Data Centers (Nuvem).

  * **O que muda hoje:**
      * Cada aluno recebe um **IP Público**.
      * O servidor não tem monitor nem teclado físico.
      * O acesso é 100% remoto via terminal.

-----

## 2\. Acesso Remoto: O Protocolo SSH

Para controlar um computador à distância com segurança, usamos o **SSH (Secure Shell)**. Ele cria um túnel criptografado entre seu PC e o servidor.

### Como Conectar

No terminal do seu computador (PowerShell, CMD ou Bash), o comando é universal:

```bash
ssh usuario@endereco_ip
```

  * **Exemplo:** `ssh aluno@203.0.113.10`
  * **O "Fingerprint" (Aperto de mão):** Na primeira conexão, digite `yes` para confirmar que confia no servidor.
  * **Senha:** Digite a senha (ela não aparecerá na tela) e dê Enter.

-----

## 3\. Sobrevivência no Terminal: Navegação

Ao logar, você verá apenas uma tela preta. Não há mouse. Você precisa "falar" com o sistema.

### Onde estou?

  * **`pwd`** (Print Working Directory): O seu GPS. Mostra em qual pasta você está agora.

### Como me movo?

  * **`cd nome_da_pasta`** (Change Directory): Entra em uma pasta.
  * **`cd ..`**: Volta um nível (sai da pasta atual).
  * **`cd ~`**: Volta para a sua casa (/home/usuario), não importa onde esteja.
  * **`ls`**: Lista os arquivos da pasta atual.

-----

## 4\. O Mapa da Mina: Estrutura de Diretórios do Linux

O Linux organiza tudo em uma árvore invertida, começando na Raiz (`/`).

[Image of Linux file system hierarchy chart with description]

| Diretório | Função / Analogia | O que o DevOps faz aqui? |
| :--- | :--- | :--- |
| **`/` (Raiz)** | O topo do prédio. Tudo começa aqui. | Nunca apague nada aqui\! |
| **`/home`** | Apartamentos dos usuários (Meus Documentos). | Onde você guarda seus projetos e scripts. |
| **`/etc`** | Painel de Controle e Configurações. | Edita configurações de rede, servidores web, etc. |
| **`/var/log`** | Registros e Diários. | Lê logs para descobrir por que algo quebrou. |
| **`/bin`** | Caixa de Ferramentas. | Onde ficam os comandos (ls, cp, cat). |
| **`/tmp`** | Lixeira temporária. | Arquivos que somem ao reiniciar. |

-----

## 5\. Criando e Editando Arquivos

### Criar arquivos vazios

  * **`touch arquivo.txt`**: Cria um arquivo vazio instantaneamente. Útil para testar permissões.

### O Editor de Texto: Nano

Não temos Bloco de Notas visual. Usamos o **Nano**.

  * **Abrir:** `nano arquivo.txt`

**Como Salvar e Sair do Nano:**

1.  Escreva seu texto.
2.  Pressione `Ctrl + X` (Sair).
3.  Pressione `Y` ou `S` (Sim, quero salvar).
4.  Pressione `Enter` (Confirmar o nome).

### Ler sem abrir

  * **`cat arquivo.txt`**: Mostra o conteúdo na tela.

-----

## 6\. Poderes Administrativos: O `sudo`

Por segurança, seu usuário comum não pode instalar programas ou mexer na raiz (`/`).

  * **`sudo` (SuperUser DO):** É o crachá de gerente.
  * **Exemplo:**
      * `apt update` -\> **Erro** (Permissão negada).
      * `sudo apt update` -\> **Sucesso** (Executa como Administrador).

> **Regra:** Use `sudo` apenas para configurar o sistema. Não use para criar arquivos na sua própria pasta `/home`.

-----

## 7\. Variáveis de Ambiente e o `$PATH`

O Linux usa "etiquetas" na memória para configurar o ambiente.

  * **`env`**: Lista todas as variáveis.
  * **`echo $USER`**: Mostra qual usuário está logado.

**O `$PATH` (Caminho):**
É uma lista de pastas onde o Linux procura os comandos. Se você digitar `ls`, o Linux procura esse programa nas pastas do `$PATH`.

  * *Por que importa?* Se você criar um script, ele não rodará apenas pelo nome. Você deve indicar o caminho: `./meu_script.sh`.

-----

## 8\. Transferindo Arquivos: SCP

Como levar um arquivo do seu PC para o servidor? Usamos o **SCP (Secure Copy)**. Execute este comando **no seu computador**, não no servidor.

**Do PC para o Servidor (Upload):**

```bash
scp meu_arquivo.txt usuario@ip_do_servidor:/home/usuario/
```

*(Note os dois pontos `:` separando o IP do destino).*

-----


Você tem total razão. Na tentativa de unificar o conteúdo, a explicação detalhada do "bê-a-bá" dos comandos acabou ficando superficial. Para um aluno que está entrando no terminal pela primeira vez, esses comandos precisam ser explicados com calma e exemplos.

Vou reescrever a seção de **"Sobrevivência no Terminal"** da Aula 06, focando especificamente nessa lista essencial (`pwd`, `ls`, `cd`, `cp`, `mv`, `rm`, `mkdir`, `touch`).

Aqui está o módulo detalhado para inserir na aula:

-----

#  Guia de Sobrevivência: Os Comandos Essenciais

Agora que você está na "tela preta", o mouse não funciona para abrir pastas. Você precisa digitar ordens. Vamos aprender os 7 comandos que você usará 90% do tempo.

### A. Localização e Navegação ("Onde estou?")

**1. `pwd` (Print Working Directory)**

  * **O que faz:** É o seu **GPS**. Mostra o caminho completo da pasta onde você está pisando agora.
  * **Exemplo:**
    ```bash
    pwd
    # Saída: /home/aluno
    ```

**2. `ls` (List)**

  * **O que faz:** São seus **olhos**. Mostra o que tem dentro da pasta atual.
  * **Variações importantes:**
      * `ls`: Lista simples.
      * `ls -l`: Lista com **detalhes** (mostra quem é o dono, tamanho e data).
      * `ls -a`: Mostra arquivos **ocultos** (no Linux, arquivos que começam com ponto `.` são invisíveis).
      * `ls -la`: Combina tudo (detalhes + ocultos).

**3. `cd` (Change Directory)**

  * **O que faz:** É o **teletransporte**. Move você de uma pasta para outra.
  * **Comandos Mágicos:**
      * `cd Downloads`: Entra na pasta Downloads.
      * `cd ..`: **Volta** um nível (sai da pasta atual).
      * `cd ~`: Vai direto para sua **Casa** (/home/usuario), não importa onde você esteja.
      * `cd /`: Vai para a **Raiz** do sistema (o início de tudo).

-----

### B. Manipulação de Arquivos ("Criar e Destruir")

**4. `mkdir` (Make Directory)**

  * **O que faz:** Cria uma nova pasta (diretório).
  * **Exemplo:**
    ```bash
    mkdir Projetos
    ```

**5. `touch`**

  * **O que faz:** Originalmente serve para mudar a data de um arquivo, mas usamos para **criar arquivos vazios** instantaneamente.
  * **Exemplo:**
    ```bash
    touch teste.txt
    # Agora existe um arquivo vazio chamado teste.txt
    ```

**6. `cp` (Copy)**

  * **O que faz:** O famoso CTRL+C / CTRL+V. Clona um arquivo.
  * **Sintaxe:** `cp [ORIGEM] [DESTINO]`
  * **Exemplos:**
      * `cp arquivo.txt copia.txt` (Cria uma cópia com outro nome).
      * `cp arquivo.txt /tmp/` (Copia o arquivo para a pasta /tmp).
      * **Atenção:** Para copiar pastas inteiras, use `cp -r` (recursivo).

**7. `mv` (Move)**

  * **O que faz:** Serve para duas coisas: **Mover** (Recortar) ou **Renomear**.
  * **Exemplos:**
      * **Mover:** `mv arquivo.txt Documentos/` (Joga o arquivo dentro da pasta Documentos).
      * **Renomear:** `mv arquivo_velho.txt arquivo_novo.txt` (Muda o nome do arquivo, pois você "moveu" ele para o mesmo lugar com outro nome).

**8. `rm` (Remove) - CUIDADO\!**

  * **O que faz:** Apaga arquivos.
  * **Aviso:** **Não existe lixeira no terminal.** Apagou, já era.
  * **Exemplos:**
      * `rm arquivo.txt`: Apaga um arquivo.
      * `rm -r pasta`: Apaga uma pasta e tudo que tem dentro dela.

-----

### Resumo Visual (Tabela Rápida)

| Ação | Comando | Exemplo |
| :--- | :--- | :--- |
| **Onde estou?** | `pwd` | `pwd` |
| **O que tem aqui?** | `ls` | `ls -la` |
| **Entrar na pasta** | `cd` | `cd Documentos` |
| **Voltar uma pasta** | `cd ..` | `cd ..` |
| **Criar pasta** | `mkdir` | `mkdir Site` |
| **Criar arquivo** | `touch` | `touch index.html` |
| **Copiar** | `cp` | `cp index.html backup.html` |
| **Mover/Renomear** | `mv` | `mv index.html /var/www/` |
| **Apagar** | `rm` | `rm lixo.txt` |



# O Editor de Texto `nano`

No mundo gráfico, usamos VS Code ou Bloco de Notas. No servidor (tela preta), precisamos de editores de texto baseados em terminal. Existem vários (Vim, Emacs), mas o **Nano** é o mais amigável para começar.

### 1\. A Interface do Nano

Diferente do Vim (que é modal e complexo), o Nano funciona como um editor comum: você abre e já pode sair digitando.

A tela é dividida em 3 partes:

1.  **Topo:** Mostra a versão do nano e o nome do arquivo que você está editando.
2.  **Centro:** A área de texto onde você escreve.
3.  **Rodapé (Muito Importante):** A "cola" dos comandos. Ele mostra os atalhos para salvar, sair, buscar, etc.

### 2\. O Segredo do "Chapeuzinho" (`^`)

Olhando para o rodapé do nano, você verá símbolos como `^G` ou `^X`.

  * O símbolo **`^`** representa a tecla **CTRL** (Control).
  * Portanto, **`^X`** significa: Pressione **CTRL** e **X** ao mesmo tempo.

-----

### 3\. Ciclo de Vida: Abrir, Editar, Salvar e Sair

Este é o procedimento padrão que você fará 1000 vezes na carreira.

#### Passo 1: Abrir ou Criar

```bash
nano meuarquivo.txt
```

*Se o arquivo existir, ele abre. Se não existir, ele cria um novo na memória.*

#### Passo 2: Editar

Apenas digite. As setas do teclado movem o cursor. O mouse não funciona para clicar no texto (em terminais puros).

#### Passo 3: Salvar (Write Out)

O comando técnico é "Write Out" (Escrever para fora).

1.  Pressione **`Ctrl + O`**.
2.  O nano perguntará: *"File Name to Write: meuarquivo.txt"* (Confirmar nome?).
3.  Pressione **`Enter`**.
      * *Note que apareceu "Wrote X lines" no centro da tela.*

#### Passo 4: Sair (Exit)

1.  Pressione **`Ctrl + X`**.
      * *Se você salvou antes:* Ele fecha e volta pro terminal.
      * *Se você NÃO salvou:* Ele perguntará *"Save modified buffer?"*. Digite **`Y`** (Yes/Sim) e depois **`Enter`** para confirmar o nome.

-----

### 4\. Atalhos Úteis (Cheat Sheet)

Além de salvar e sair, o nano tem ferramentas poderosas:

| Atalho | Nome | O que faz? |
| :--- | :--- | :--- |
| **`Ctrl + W`** | **W**here Is | **Pesquisar.** Digite a palavra e dê Enter. (Use `Alt + W` para buscar a próxima ocorrência). |
| **`Ctrl + K`** | Cu**t** Text | **Recortar.** Apaga a linha inteira onde o cursor está. (Muito usado para deletar linhas rápidas). |
| **`Ctrl + U`** | **U**ncut Text | **Colar.** Cola a linha que você acabou de recortar com o `Ctrl + K`. |
| **`Ctrl + _`** | Go To Line | **Ir para linha.** Digite o número da linha (útil quando o log de erro diz "Erro na linha 54"). |
| **`Ctrl + C`** | Cur Pos | Mostra em qual linha e coluna o cursor está agora. |

-----

### 5\. Nano vs. Vim (Curiosidade para o aluno)

Provavelmente alguém vai perguntar: *"E o tal do Vim? É melhor?"*

  * **Nano:** É como uma bicicleta com rodinhas. Fácil de pegar e sair andando. É o ideal para edições rápidas de configuração.
  * **Vim:** É como um jato de caça. Extremamente poderoso, faz coisas incríveis com poucos toques, mas se você não souber pilotar, nem consegue sair do chão (ou sair do editor\!).
      * *Veredito:* Começamos com Nano. Quando você se sentir um "Jedi" do Linux, aprenda o básico de Vim.

-----

### Exercício Prático Sugerido

1.  Crie um arquivo: `nano lab_nano.txt`
2.  Escreva 3 linhas com nomes de frutas.
3.  Salve o arquivo (`Ctrl+O`, `Enter`).
4.  Saia do arquivo (`Ctrl+X`).
5.  Abra novamente.
6.  Use o `Ctrl+K` para apagar a segunda fruta.
7.  Saia e Salve usando o atalho rápido: `Ctrl+X`, `Y`, `Enter`.
