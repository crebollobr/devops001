# Aula 07: Introdução à Automação com Bash Script

**Objetivo:** Entender como o Linux processa informações, como guardar dados na memória e como transformar uma lista de tarefas chatas em um arquivo executável.

-----

## 1\. Variáveis: As Caixas de Memória

Imagine que você tem uma caixa e escreve "Nome" nela. Dentro, você coloca "Maria". Sempre que alguém perguntar "O que tem na caixa Nome?", a resposta será "Maria".

No Linux, usamos variáveis para não ter que digitar a mesma coisa mil vezes.

### A. Criando uma Variável (Atribuição)

A regra de ouro que reprova muita gente: **NÃO USE ESPAÇOS NO IGUAL\!**

  * **Errado:** `site = google.com` (O Linux acha que você está rodando um comando chamado 'site').
  * **Certo:** `site="google.com"`

### B. Usando a Variável (Expansão)

Para "abrir a caixa" e pegar o valor, usamos o cifrão **`$`**.

```bash
nome="João"
echo "Olá, $nome"
# Saída: Olá, João
```

### C. Boas Práticas

  * Use nomes descritivos: `diretorio_backup` é melhor que `d`.
  * O Linux já tem variáveis prontas (Variáveis de Ambiente). Tente: `echo $USER`, `echo $HOME`, `echo $PWD`.

-----

## 2\. Conectores: O `;` e o `|` (Pipe)

Aqui está a diferença entre fazer "uma coisa de cada vez" e "trabalhar em linha de produção".

### A. O Ponto e Vírgula (`;`) - "E depois..."

Serve para rodar dois ou mais comandos na mesma linha, um após o outro, sem se importar com o resultado do anterior.

  * **Sintaxe:** `comando1 ; comando2`
  * **Exemplo:** `cd /tmp ; ls`
      * *Tradução:* "Vá para a pasta tmp. Quando terminar, liste os arquivos."

### B. O Pipe (`|`) - O Encanamento

Este é o recurso mais poderoso do Unix. Ele pega o **resultado** (saída) do comando da esquerda e joga como **ingrediente** (entrada) para o comando da direita.

  * **Sintaxe:** `comando1 | comando2`

  * **Exemplo:** `cat lista_de_nomes.txt | sort`

      * *Tradução:* "Leia o arquivo (cat). Não jogue na tela\! Jogue o texto direto para o comando `sort`, que vai organizar tudo em ordem alfabética e só então mostrar."

  * **Exemplo DevOps (Filtrando Processos):**
    `ps aux | grep "nginx"`

      * "Liste todos os processos rodando (`ps aux`) E jogue essa lista no filtro (`grep`) para mostrar só o que tem o nome 'nginx'".

-----

## 3\. O Comando `echo`

O `echo` é a voz do seu script. Ele serve para mostrar mensagens na tela ou escrever em arquivos.

  * **Simples:** `echo "Iniciando backup..."`
  * **Com Variável:** `echo "O usuário é $USER"`
  * **Escrevendo em arquivo (Redirecionamento `>`):**
      * `echo "Erro no sistema" > log.txt` (Cria ou sobrescreve o arquivo com essa frase).
      * `echo "Mais um erro" >> log.txt` (O `>>` duplo adiciona ao final, sem apagar o que já tinha).

-----

## 4\. Criando seu Primeiro Script (`.sh`)

Um Script Bash nada mais é do que um arquivo de texto contendo os comandos que você digitaria manualmente, um embaixo do outro.

### A Anatomia de um Script

Todo script precisa começar com a **Shebang**.

1.  **Crie o arquivo:** `nano backup.sh`
2.  **A Primeira Linha (Obrigatória):** `#!/bin/bash`
      * Isso avisa ao Linux: "Use o interpretador BASH para ler este arquivo".
3.  **Comentários:** Linhas que começam com `#` são ignoradas. Use para explicar o código.

### Exemplo Prático: O Script "Organizador"

```bash
#!/bin/bash

# Define o nome da pasta na variável
pasta="Projeto_Novo"

echo "--- Iniciando Automação ---"

# 1. Cria a pasta
echo "Criando diretório: $pasta"
mkdir $pasta

# 2. Entra na pasta
cd $pasta

# 3. Cria arquivos vazios
echo "Criando arquivos de estrutura..."
touch index.html style.css script.js

# 4. Lista o resultado
echo "Tudo pronto! Veja o conteúdo:"
ls -l

echo "--- Fim ---"
```

-----

## 5\. Como Transformar Comandos em Script (Passo a Passo)

Esta é a metodologia que o aluno deve usar no dia a dia.

**Cenário:** Todo dia de manhã, você precisa verificar a rede, ver o espaço em disco e salvar a data num arquivo.

**Fase 1: Teste Manual (No terminal)**
Primeiro, digite os comandos soltos para ver se funcionam.

1.  `date`
2.  `df -h`
3.  `ping -c 3 google.com`

**Fase 2: Consolidação (No arquivo)**
Agora que sabemos que os comandos funcionam, vamos colocá-los no arquivo.

1.  `nano verifica_servidor.sh`
2.  Digite:
    ```bash
    #!/bin/bash
    echo "Relatório do Dia:" > relatorio.txt
    date >> relatorio.txt
    echo "----------------" >> relatorio.txt
    df -h >> relatorio.txt
    echo "Testando Internet..."
    ping -c 3 google.com
    ```
3.  Salve (`Ctrl+O`, `Enter`, `Ctrl+X`).

**Fase 3: A Transformação (Permissão de Execução)**
Um arquivo de texto não roda sozinho. Precisamos torná-lo um **programa**.

  * Comando: `chmod +x verifica_servidor.sh`
      * *`+x` significa "Add eXecutable permission".*

**Fase 4: A Execução**

  * Comando: `./verifica_servidor.sh`

-----

## 6\. Desafio Prático da Aula

Peça para os alunos criarem um script chamado `meu_setup.sh` que faça o seguinte:

1.  Diga "Olá, [Nome do Usuário]".
2.  Crie uma pasta chamada `atividade_aula07`.
3.  Entre nessa pasta.
4.  Crie dois arquivos: `teste1.txt` e `teste2.txt`.
5.  Liste os arquivos criados.
6.  Diga "Setup concluído com sucesso\!".

*Dica: Lembrem-se de dar `chmod +x` antes de rodar\!*
