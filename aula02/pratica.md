# Arquivo de Apoio: Escolhendo as Ferramentas (Aula 02)

## 1. "Sabores" de Linux: O que são Distribuições?

Muitas vezes você ouvirá a pergunta: *"Qual Linux você usa?"*. Essa pergunta, tecnicamente, refere-se à **Distribuição** (ou Distro).

Como vimos, o **Linux** é apenas o **Kernel** (o motor do carro). Mas ninguém dirige apenas um motor. Você precisa do chassi, das rodas, do volante e do painel. No mundo dos Sistemas Operacionais, as distribuições pegam o Kernel Linux e adicionam:
* Ferramentas de sistema (GNU tools).
* Um gerenciador de pacotes (a "loja de aplicativos").
* Uma interface (se for desktop).
* Configurações padrão.



### As Principais Famílias ("Sabores")

Embora existam centenas, no mundo corporativo e DevOps, focamos em três grandes famílias:

1.  **Família Debian:**
    * **Exemplos:** Debian, Ubuntu, Linux Mint.
    * **Características:** Focada em usabilidade e uma comunidade gigantesca. Usa o gerenciador de pacotes `.deb` e o comando `apt`. É a porta de entrada mais comum para iniciantes.

2.  **Família Red Hat:**
    * **Exemplos:** RHEL (Red Hat Enterprise Linux), Fedora, CentOS, Rocky Linux, AlmaLinux.
    * **Características:** O padrão "Enterprise" (corporativo). Focada em estabilidade extrema e certificação de hardware. Usa pacotes `.rpm` e os comandos `dnf` ou `yum`. Muito comum em bancos e grandes indústrias.

3.  **Alpine Linux (Menção Honrosa para DevOps):**
    * Uma distribuição minúscula (cerca de 5MB).
    * **Por que importa?** É a base da maioria dos containers Docker que veremos no futuro, devido ao seu tamanho reduzido e segurança.

---

## 2. Nossa Escolha: Ubuntu Server

Para este curso, escolhemos utilizar o **Ubuntu Server**.

### Por que Ubuntu?
A resposta é pragmática: **Comunidade e Documentação.**
O Ubuntu é a distribuição mais utilizada no mundo em ambientes de nuvem pública (AWS, Azure, Google Cloud). Isso significa que, se você tiver um erro ou dúvida, é 99% provável que alguém já tenha tido esse problema, postado em um fórum e resolvido. Para quem está aprendendo, essa facilidade de encontrar respostas é vital.

### O que significa "Server"?
Você notará que não baixaremos a versão "Desktop".
* **Ubuntu Desktop:** Vem com interface gráfica, navegador, reprodutor de vídeo, papéis de parede. É pesado e consome muita memória RAM.
* **Ubuntu Server:** Vem apenas com o essencial para o sistema funcionar. **Não tem interface gráfica (janelas)**. Interagiremos apenas por texto (terminal).
    * *Vantagem:* É extremamente leve, rápido e simula exatamente o ambiente real que você encontrará trabalhando profissionalmente em servidores remotos.

---

## 3. O Laboratório: VirtualBox

Para praticar sem medo de errar, não instalaremos o Linux diretamente no hardware do seu computador pessoal (formatando o disco). Usaremos a **Virtualização**.

### O que é o VirtualBox?
O Oracle VM VirtualBox é um software de virtualização (Hypervisor Tipo 2). Ele permite criar um "computador dentro do computador".

### Por que vamos usá-lo?
1.  **Segurança:** Se você deletar um arquivo crítico do Linux na máquina virtual e o sistema quebrar, seu computador real (Windows/Mac) continua intacto. Basta apagar a VM e criar outra.
2.  **Snapshots (O "Save Game"):** O VirtualBox permite salvar o estado da máquina. Antes de fazer uma configuração arriscada na aula, você pode tirar um "Snapshot". Se der errado, você restaura o estado anterior em segundos.
3.  **Rede Isolada:** Podemos criar uma rede virtual para simular servidores conversando entre si, sem interferir na rede Wi-Fi da sua casa.

---

> **Próximo Passo:** Agora que entendemos o *que* vamos instalar e *onde*, vamos iniciar o procedimento prático de criação da Máquina Virtual e instalação do Sistema Operacional.
