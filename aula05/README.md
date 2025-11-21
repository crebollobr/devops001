# Aula 05: Prática - Instalação do Ubuntu Server no VirtualBox

**Objetivo:** Ao final desta aula, cada aluno terá uma máquina virtual (VM) funcional, conectada à internet e pronta para receber comandos.

-----

## 1\. Preparação (Pré-requisitos)

Antes de começar, certifique-se de que todos têm:

1.  **VirtualBox instalado** (e o *Extension Pack* recomendado).
2.  **ISO do Ubuntu Server** baixada (versão LTS mais recente, ex: 24.04 ou 22.04).
3.  **Virtualização ativada na BIOS** do computador (se alguém tiver erro de VTx/AMD-V, esse é o motivo).

-----

## 2\. Criando a "Máquina" (O Hardware Virtual)

Vamos montar o computador virtual antes de instalar o sistema.

1.  Abra o VirtualBox e clique em **"Novo"** (New).
2.  **Nome:** `Servidor-DevOps-01` (ou o nome do aluno).
3.  **Tipo:** Linux.
4.  **Versão:** Ubuntu (64-bit).
    \*
5.  **Memória RAM:** Mínimo 2048 MB (2GB). Se o aluno tiver um PC potente, 4GB é o ideal.
6.  **Disco Rígido:** Criar um novo disco virtual (VDI) -\> Dinamicamente alocado -\> **20 GB** (10GB é pouco para o curso todo).

**Ajuste Fino (Importante):**

  * Selecione a VM criada e clique em **Configurações (Settings)**.
  * Vá em **Armazenamento (Storage)** -\> Clique no ícone de CD "Vazio".
  * No lado direito, clique no ícone do CDzinho azul -\> **Choose a disk file** -\> Selecione a **ISO do Ubuntu Server** que você baixou.
  * Vá em **Rede (Network)** -\> Certifique-se de que está em **NAT** (mais fácil para garantir internet) ou **Placa em Modo Bridge** (se quiser que o servidor tenha um IP na rede local de casa). *Recomendação: Comece com NAT para evitar problemas de roteador.*

-----

## 3\. Instalando o Sistema Operacional

Inicie a Máquina Virtual (`Iniciar/Start`). O instalador do Ubuntu (texto) irá carregar.

**Passo a Passo da Instalação:**

1.  **Língua:** Selecione **English**.
      * *Explicação:* Em DevOps, logs de erro e documentação são sempre em inglês. É melhor acostumar desde já.
2.  **Teclado:** Aqui é a pegadinha\!
      * Selecione `Identify Keyboard` ou escolha manualmente `Portuguese (Brazil)` se o teclado tiver "Ç". Se não, `US International`. Teste as teclas antes de prosseguir.
3.  **Rede:** O instalador deve pegar um IP via DHCP automaticamente. Apenas dê `Done`.
4.  **Proxy:** Deixe em branco. `Done`.
5.  **Mirror:** Deixe o padrão. `Done`.
6.  **Disco (Storage):**
    \*
      * Selecione **"Use an entire disk"**.
      * Desmarque "Set up this disk as an LVM group" (Para iniciantes, partição simples é menos confusa, mas LVM é o padrão. Pode manter o padrão se preferir).
      * Confirme a destruição dos dados do disco (virtual).
7.  **Perfil (Profile Setup):**
      * **Your name:** Nome do Aluno.
      * **Server name:** `server-01` (Evite espaços).
      * **Username:** `devops` (ou nome do aluno).
      * **Password:** **Escolha uma senha fácil de lembrar agora\!** (ex: 123456 ou linux). Se esquecer, perdemos a VM.
8.  **SSH Setup (CRUCIAL):**
    \*
      * Marque a opção `[x] Install OpenSSH server`.
      * *Explicação:* Sem isso, não conseguiremos acessar o servidor remotamente no futuro.
9.  **Featured Server Snaps:** Não marque nada agora. `Done`.
10. **Instalação:** Aguarde terminar e selecione **Reboot Now**.
      * *Dica:* Se o VirtualBox pedir para remover a mídia, pressione ENTER.

-----

## 4\. Primeiro Login e Verificação de Rede

O sistema reiniciou. Aparecerá uma tela preta pedindo `login:`.

1.  Digite o usuário (ex: `devops`) e a senha.

      * *Aviso:* Ao digitar a senha no Linux, **nada aparece na tela** (nem asteriscos). Isso é segurança. Digite e dê Enter.

2.  **Verificar conectividade (Prática da Aula 04):**

      * Peça para os alunos digitarem: `ip addr`
      * Identifiquem o IP da interface `eth0` ou `enp0s3`.
      * Peça para testarem a internet: `ping -c 4 google.com`
      * Se responder (64 bytes from...), sucesso\! O servidor está vivo.

-----

## 5\. Prática de Gerenciamento de Pacotes

Agora vamos instalar algo útil e visual para celebrar o sucesso da instalação.

**Sugestão de Pacote: `htop` e `neofetch`**

1.  Primeiro, a regra de ouro:

    ```bash
    sudo apt update
    ```

    *(Vai pedir a senha novamente).*

2.  Instalando o monitor de sistema:

    ```bash
    sudo apt install htop -y
    ```

3.  Rodando o programa:

    ```bash
    htop
    ```

      * 
      * *Atividade:* Peça para observarem o uso de Memória e CPU. Para sair, aperte `F10` ou `q`.

4.  **(Bônus Divertido) Instalando o Neofetch:**
    O Neofetch exibe o logo do sistema e informações de hardware de forma bonita (ótimo para postar no LinkedIn/Instagram que começou o curso).

    ```bash
    sudo apt install neofetch -y
    neofetch
    ```

-----

## Encerramento

  * Ensinar como desligar o servidor corretamente via comando:
    ```bash
    sudo poweroff
    ```
    *(Nunca feche a janela do VirtualBox "na marra", isso pode corromper o disco).*
