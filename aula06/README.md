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

-----

## 5\. Atividade Prática: "Hello Cloud"

*O instrutor deve fornecer a lista de IPs e Usuários/Senhas para cada aluno neste momento.*

**Passo a Passo:**

1.  **Conexão:** Abra o terminal do seu computador e conecte na sua VM:
    `ssh usuario@SEU_IP_DA_NUVEM`
2.  **Aceite a chave:** Digite `yes` na pergunta do fingerprint.
3.  **Teste o Sudo:**
      * Tente rodar: `apt update` (Deve falhar).
      * Tente rodar: `sudo apt update` (Deve funcionar).
4.  **Transferência de Arquivo (Desafio):**
      * No seu computador **local** (abra outro terminal, não feche o SSH), crie um arquivo:
        `echo "Estou na nuvem" > teste.txt`
      * Envie para o servidor usando SCP:
        `scp teste.txt usuario@SEU_IP_DA_NUVEM:/home/usuario/`
      * Volte para o terminal do SSH (na nuvem) e verifique se o arquivo chegou:
        `ls -la` e `cat teste.txt`

-----

### Dica para o Instrutor (Sobre a Nuvem):

Como você ainda não definiu a nuvem, aqui vão sugestões rápidas para "1 VM por aluno":

  * **AWS (EC2):** Crie uma conta, suba as instâncias t2.micro (Free Tier) ou t3.nano. Vai precisar gerenciar as chaves `.pem` (o que complica um pouco o comando SSH para `ssh -i chave.pem user@ip`).
  * **DigitalOcean / Linode / Hetzner:** Mais simples. Cria com senha de root ou usuário padrão, e o acesso é direto com senha, facilitando a didática para iniciantes que podem se atrapalhar com chaves RSA agora.
  * **Laboratório Local:** Se a nuvem falhar, você pode usar as VMs do VirtualBox em modo "Bridge" (se todos estiverem na mesma rede Wi-Fi) para simular acesso remoto entre colegas.
