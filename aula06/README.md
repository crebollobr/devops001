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

## 9\. Prática da Aula: "Hello Cloud"

1.  Conecte-se à sua VM na nuvem via SSH.
2.  Use `pwd` para confirmar que está na sua `/home`.
3.  Vá até a raiz (`cd /`) e tente criar um arquivo (`touch teste.txt`). **Observe o erro de permissão.**
4.  Volte para casa (`cd ~`).
5.  Crie um arquivo chamado `lab06.txt` usando o `nano`. Escreva seu nome dentro.
6.  Instale o pacote `neofetch` usando `sudo apt install neofetch`.
7.  **(Desafio)**: No terminal do seu computador local, crie um arquivo e envie para a nuvem via `scp`.
