# Material Extra: GitHub e a Arte do README.md

## 1\. Git vs. GitHub: Qual a diferença?

Antes de escrever, precisamos limpar uma confusão comum:

  * **Git:** É a **ferramenta** de linha de comando instalada no seu computador. É a "Máquina do Tempo" que salva versões do seu código. (Funciona offline).
  * **GitHub:** É o **site** (a Nuvem). É onde hospedamos os repositórios Git para compartilhar com o mundo e trabalhar em equipe. Pense no GitHub como a "Rede Social dos Programadores".

> **Analogia:** O Git é o *Microsoft Word* (onde você escreve). O GitHub é o *Google Drive* (onde você guarda e compartilha).

-----

## 2\. O Arquivo `README.md`

Todo projeto no GitHub deve ter um arquivo chamado `README.md` na raiz.

  * **README:** "Leia-me". É a primeira coisa que aparece quando alguém abre seu repositório.
  * **.md:** Significa **Markdown**. É uma linguagem de marcação super simples que converte texto puro em HTML bonito.

### Por que usar Markdown?

Diferente do Word (.docx), o Markdown é texto puro. Ele é leve, pode ser lido no terminal e versionado facilmente pelo Git.

-----

## 3\. Guia de Sintaxe Markdown (Cheat Sheet)

Aqui estão os códigos que você usará 99% do tempo para deixar sua documentação profissional.

### A. Títulos e Cabeçalhos

Use `#` para criar títulos. Quanto mais cerquilhas, menor o título.

```markdown
# Título Principal (H1)
## Subtítulo (H2)
### Seção menor (H3)
```

### B. Ênfase (Negrito e Itálico)

```markdown
Este texto é *itálico* ou _itálico_.
Este texto é **negrito** ou __negrito__.
Este é ***negrito e itálico***.
```

### C. Listas

Organize os passos de instalação ou requisitos.

```markdown
**Lista não ordenada (Bullets):**
* Item 1
* Item 2
  * Sub-item (use tab para indentar)

**Lista ordenada (Números):**
1. Primeiro passo
2. Segundo passo
3. Terceiro passo
```

### D. Links e Imagens

A sintaxe é quase igual, só muda a exclamação `!` na frente da imagem.

```markdown
[Texto do Link](https://google.com)

![Texto alternativo da imagem](https://link-da-imagem.png)
```

### E. Blocos de Código (Essencial para DevOps\!)

Nunca cole código ou comandos soltos no texto. Use as crases triplas (\`\`\`).

**Para comandos de uma linha (inline):**
Para instalar, use o comando `apt install docker`. (Use uma crase \` no início e fim).

**Para blocos de código (scripts/configs):**
Use três crases \`\`\` no início e fim. Você pode especificar a linguagem (bash, python, yaml) para ter cores.

```bash
#!/bin/bash
echo "Instalando sistema..."
sudo apt update
```

-----

## 4\. Modelo de README para seus Projetos do Curso

Copie e cole este modelo nos seus exercícios. Ele segue o padrão de mercado.

````markdown
# Nome do Projeto (ex: Servidor Web Nginx)

Uma breve descrição do que este projeto faz. Ex: "Configuração automatizada de um servidor web utilizando scripts Bash e Docker."

## 🚀 Começando

Essas instruções permitirão que você obtenha uma cópia do projeto em operação na sua máquina local para fins de desenvolvimento e teste.

### 📋 Pré-requisitos

De que coisas você precisa para instalar o software e como instalá-las?

* Linux (Ubuntu 20.04+)
* Docker instalado
* Git

### 🔧 Instalação

Um passo a passo de como rodar o ambiente:

1. Clone o repositório:
   ```bash
   git clone [https://github.com/seu-usuario/seu-projeto.git](https://github.com/seu-usuario/seu-projeto.git)
````

2.  Entre na pasta:

    ```bash
    cd seu-projeto
    ```

3.  Execute o script de instalação:

    ```bash
    chmod +x install.sh
    ./install.sh
    ```

## 🛠️ Ferramentas Utilizadas

  * [Ubuntu Server](https://ubuntu.com/) - O Sistema Operacional
  * [Docker](https://www.docker.com/) - Containerização
  * [Bash](https://www.gnu.org/software/bash/) - Scripting

## ✒️ Autores

  * **Seu Nome** - *Trabalho Inicial* - [SeuGitHub](https://github.com/link)

-----

⌨️ com ❤️ por [Seu Nome] 😊

```

---

## 5. Dica de Ouro: Visualizando antes de postar

Você não precisa enviar para o GitHub para ver se ficou bonito.

* **No VS Code:** Abra seu arquivo `.md` e pressione `Ctrl + Shift + V` (ou clique no ícone de lupa/livro no canto superior direito). Ele abre um preview lado a lado.
* **Editor Online:** Se não estiver no VS Code, use sites como o [Dillinger.io](https://dillinger.io/) ou [StackEdit](https://stackedit.io/) para testar sua formatação.
```
