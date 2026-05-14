# EFBT-AUTODEBIAN
Automated Debian Bare-Metal Provisioning using Preseed (Hybrid Boot: BIOS/UEFI).

Este repositório contém a estrutura de arquivos necessária para transformar uma ISO oficial do Debian em uma mídia de instalação 100% automatizada, 
corrigindo desafios comuns de boot híbrido (Legacy/UEFI) e padronizando o ambiente para utilização do SO.

Provisionamento de Infraestrutura Automatizado

Processos manuais de instalação de SO são o inimigo número 1 da escalabilidade. 
Geram inconsistências de particionamento, erros de rede e um alto custo de tempo operacional. 


- Para eliminar o "trabalho braçal", utilizei o *Debian Preseed* (`preseed.cfg`). 
Este arquivo de configuração atua como uma resposta automatizada ao instalador do Debian, garantindo:

* Particionamento Padronizado: Configuração automática de volumes (Root, Swap) sem intervenção manual.
* Gestão de Identidade: Criação automatizada de usuários, grupos e definição de privilégios de `sudo`.
* Networking: Configuração de hostname e parâmetros de rede via DHCP/Static.
* Bootstrap de Dependências: Instalação nativa de pacotes essenciais (`openssh-server`, `curl`, `vim`, `net-tools`) já no primeiro boot.


Benefícios e Melhoria Esperada:

* Consistência (Reprodutibilidade de Ambiente): Garantia de que todos os servidores do laboratório terão a mesma base.
* Escalabilidade: Redução do tempo de deploy do SO de ~20 minutos para o tempo de escrita no disco.
* Observabilidade facilitada: Com o ambiente padronizado, o troubleshooting e a manutenção tornam-se previsíveis.


Etapas:

1 - Configuração do arquivo de configurações para instalação automática
[preseed.cfg]

2 - Extração e modificação da estrutura da ISO do Debian

3 - Inclusão do preseed.cfg criado anteriormente em seu diretório raiz

4 - Editar .CFG´s nos seguintes diretórios:
	- \boot\grub\grub.cfg
	- \boot\grub\x86_64-efi\grub.cfg
	- \EFI\debian\grub.cfg
	- \isolinux\isolinux.cfg
	- \isolinux\adtxt.cfg
     para que estes deem boot diretamente apontados ao preseed.cfg.
a edição desses diretórios foi feita para garantir compatibilidade híbrida (BIOS/Legacy e UEFI)

5 - Remontagem da imagem .ISO, já com preseed.cfg em seu diretório raiz, utilizando AnyBurn

6 - Instalação automática pronta


Estrutura de arquivos na ISO:
/
├── preseed.cfg
├── boot/grub/grub.cfg
├── boot\grub\x86_64-efi\grub.cfg
├── EFI/debian/grub.cfg
└── isolinux/isolinux.cfg
