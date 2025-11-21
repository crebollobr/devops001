# Aula: Navegando e Gerenciando o Linux via Terminal

## 1\. O Conceito da Árvore de Diretórios

Antes de digitar, precisamos entender onde estamos. O Linux não usa letras de unidade (`C:`, `D:`). Ele usa uma estrutura de **Árvore Invertida**.

  * **`/` (Root/Raiz):** É o início de tudo. Todas as pastas estão dentro da raiz.
  * **Caminho (Path):** É o endereço de um arquivo (ex: `/home/usuario/projeto/arquivo.txt`).

-----

## 2\. Navegação: "Onde estou e para onde vou?"

Estes comandos são o seu GPS dentro do terminal.

| Comando | Significado | Explicação Didática |
| :--- | :--- | :--- |
| **`pwd`** | *Print Working Directory* | **"Onde estou?"** Mostra o caminho completo da pasta atual. Essencial para não se perder. |
| **`ls`** | *List* | **"O que tem aqui?"** Lista os arquivos e pastas. <br> *Dica:* Use `ls -la` para ver detalhes ocultos e permissões. |
| **`cd`** | *Change Directory* | **"Me leve para..."** Entra em uma pasta.<br> `cd pasta` (entra)<br> `cd ..` (volta uma pasta para trás)<br> `cd ~` (vai para a casa do usuário). |

-----

## 3\. Manipulação: "Criar, Copiar, Mover e Apagar"

Agora que sabemos andar, vamos mexer nas coisas.

### Criando

  * **`mkdir nome_da_pasta`** *(Make Directory)*: Cria uma nova pasta.
  * **`touch nome_do_arquivo`**: Cria um arquivo vazio (ou atualiza o horário de um existente). *Sugestão de adição.*

### Movimentando e Copiando

  * **`cp origem destino`** *(Copy)*: Faz uma cópia do arquivo.
      * *Ex:* `cp relatorio.txt relatorio_bkp.txt`
      * *Dica:* Para copiar pastas inteiras, use `cp -r`.
  * **`mv origem destino`** *(Move)*: Serve para duas coisas:
    1.  **Mover:** Tirar de um lugar e por em outro.
    2.  **Renomear:** Se você mover `arquivo.txt` para `novo_nome.txt` na mesma pasta, você o renomeou.

### Destruindo (Cuidado\!)

  * **`rm nome_do_arquivo`** *(Remove)*: Apaga arquivos.
      * *Atenção:* No terminal **não existe lixeira**. Apagou, já era.
      * *Dica:* Para apagar pastas use `rm -rf` (Recursive/Force). *Sugestão de adição indispensável.*

-----

## 4\. Leitura: "Olhando o conteúdo"

Como ler arquivos de texto (logs, configurações, códigos) sem abrir um editor gráfico.

  * **`cat arquivo`** *(Concatenate)*: Joga o conteúdo **inteiro** na tela de uma vez. Bom para arquivos pequenos.
  * **`less arquivo`**: O visualizador inteligente. Permite navegar com as setas, buscar palavras. Não carrega o arquivo todo na memória (bom para arquivos gigantes). "Less is more".
  * **`more arquivo`**: O avô do `less`. Só permite ir para frente, não volta. (Hoje em dia, usamos quase sempre o `less`).
  * **`head` e `tail`** (*Sugestão de adição*):
      * `head`: Mostra as primeiras 10 linhas.
      * `tail`: Mostra as últimas 10 linhas.
      * `tail -f`: **Vital para DevOps**. Fica monitorando o arquivo em tempo real (ex: ver um log de erro acontecendo agora).

-----

## 5\. Permissões e Segurança (O Modelo UGO)

Esta é a parte técnica mais crítica. No Linux, tudo tem dono e regras.

### O Conceito: Quem é quem? (UGO)

  * **U**ser (u): O dono do arquivo (quem criou).
  * **G**roup (g): O grupo que tem acesso (ex: grupo 'devs').
  * **O**thers (o): O resto do mundo (qualquer um que não seja o dono nem do grupo).

### O Conceito: O que podem fazer? (rwx)

  * **r** (Read - 4): Pode ler/abrir o arquivo.
  * **w** (Write - 2): Pode alterar/salvar/apagar o arquivo.
  * **x** (Execute - 1): Pode rodar o arquivo como um programa (script).

### O Comando: `chmod`

*Change Mode*: Altera as permissões. Pode ser usado de dois jeitos:

1.  **Modo Simbólico (Mais fácil):**

      * `chmod +x script.sh`: Adiciona permissão de e**x**ecução para todos.
      * `chmod u+w arquivo.txt`: Adiciona permissão de escrita (**w**) apenas para o dono (**u**).

2.  **Modo Octal (Numérico - Padrão DevOps):**

      * Soma-se os valores: r=4, w=2, x=1.
      * **7** (4+2+1) = Leitura, Escrita e Execução (Tudo).
      * **5** (4+0+1) = Leitura e Execução.
      * **6** (4+2+0) = Leitura e Escrita.
      * *Exemplo Clássico:* `chmod 755 arquivo` (Dono faz tudo, o resto só lê e executa).

### Outros comandos de permissão sugeridos:

  * **`chown`** *(Change Owner)*: Muda quem é o dono do arquivo. (Ex: `chown usuario arquivo`).
  * **`sudo`** *(SuperUser DO)*: O comando mais poderoso. Executa qualquer comando anterior como "Administrador" (Root). Ex: `sudo apt update`.

-----

## 6\. Resumo da Aula (Cheat Sheet)

| Categoria | Comandos |
| :--- | :--- |
| **Navegar** | `pwd`, `ls`, `cd` |
| **Criar** | `mkdir`, `touch` |
| **Manipular** | `cp`, `mv`, `rm` |
| **Ler** | `cat`, `less`, `tail` |
| **Permissões** | `chmod`, `chown`, `sudo` |
| **Ajuda** | `man` (manual do comando), `clear` (limpa a tela) |
