# Draft Artigo #0001: Lab local de Kubernetes easy easy

Cara, seguinte, já pensou em uma forma facil e sem custo para ter seu laboratorios de estudos k8s? tem ai um oldbook para voce transformar ele em um home server? Então acho que da para começar a brincadeira.

Bom, uma boa justificativa de por qual motivo fazer isso, seria, sei lá, ter um home server rodando coisas uteis na sua casa via kubertetes e ter a experiencia de por um cluster em produção on-premises e manter ele? Não sei o quanto conta, mas para mim, é meu hobby fazer essas coisas, então, vamos que vamos....

O que vamos precisar?

- Oldbook
- PenDrive
- Ventoy
- Proxmox
- Warp Terminal
- TalosCtl
- Talos.ISO

# OldBook + Proxmox

Então, tens ai um notebook antigo? um desktop encostado? Precisamos de uma maquina para subir o remedio Proxmox, não lembro onde eu ouvi isso mas faz sentido, parece maior nome de remedio, lol. Mas, fuciona bem! stick with me and you'll shine!

O Proxmox é um Hypervisor tipo 1, e te falar, curto bastante fazer meus labs com ele, já tentei migrar para outros, mas ele é leve e funcional e o melhor, 0800, freezão! Ah, quase esqueço, para funcionar, seu notebook antigo precisa ter suporte a virtualização, acho que um computador com X anos de uso, dependendo de alguns fatores, pode ser que já tenha, mas, vale a tentativa, se não tiver um oldbook ou computador, vou pensar depois em uma forma diferente de fazer isso, e te falar que ja to com uma ideia doida de fazer um cluster com oldphones, será que rola?

Continuando, Baixa a ISO do Proxmox, e tambem baixa o Ventoy, roda o executavel do ventoy com seu pendrive conectado e olha bem antes de clicar em formatar, vai apagar tudo hein! Ventoy aplicado, só copiar e colar a ISO do Proxmox no seu pendrive e vamos para o OldBook.

Boot nele, de note para note para bootar pelo USB costuma ser diferente, mas se não souber, só procurar o modelo do seu notebook + tecla boot menu, deve ser o f11, f2, esc, alguma dessas ou outras, qualquer duvida, deixa ai o note e o modelo que a gente tenta ajudar.

Para instalar o Proxmox não tem misterio, tipo next next finish, só se atente ao endereço de IP tem que ser fixo na sua rede, maioria vai ser 192.168.0.algumacoisa, então, se não tiver como reservar seu ip, joga um ip alto, 192.168.0.200, por exemplo, mas da um confere se ele não ta em uso na sua rede. Se isso não for sua praia, depois posso falar mais sobre, comenta ai.

Ah, sugestão de Video, tem esses aqui, do Diolinux para dar um start, mas cara, treina ai seu ingles, da uma olhada nos videos do Techno Tim e do Christian Lempa, mesmo com legenda, ir ouvindo vai te ajudar no futuro caso não tenha ainda ingles.

Proxmox instalado vai aparecer isso na tela, se estiver num notebook, faz sentido seguir a ideia do Diolinux e desativar a tela, tambem faço a questão de unificar as particções, deixar os comandos resumidos aqui.

Ai para testar a função de container do Proxmox, o LXC, vamos subir um Ubuntu Server para colocar o TalosCTL e seja la mais o que precisar, passo X Y e Z para fazer isso e pronto.

Warp Terminal para que? Só indicando, terminal top d+, e se usar meu link ai, eu posso ganhar alguns brindes, ajuda nois, vai?

Usando o Warp, vamos de SSH conectar nesse cara para ficar local e instalar o TalosCTL para criar nosso cluster.

Além disso, vou subir 3 VMs aqui para brincar, a configuração minima do Talos é a seguinte, mas isso vai depender do seu Hardware.

Todas as VMs estão up and running, agora, vamos de TalosCTL

SEGUIR o passo a passo da instalação. ## Draft, pendente:

Criar o ambiente:

- Subir uma VM para lidar como Gerenciador.
- curl -sL https://talos.dev/install | sh
- talosctl gen config pick https://192.168.15.79:6443
- talosctl disks --nodes 192.168.15.79 --insecure
- nano controlplane.yaml e adicione o disco correto em Install.
- talosctl apply-config --nodes 192.168.15.79 --insecure --file controlplane.yaml
- talosctl bootstrap -n 192.168.15.79 -e 192.168.15.79 --talosconfig ./talosconfig
- talosctl dashboard -n 192.168.15.79 -e 192.168.15.79 --talosconfig ./talosconfig
- talosctl services -n 192.168.15.79 -e 192.168.15.79 --talosconfig ./talosconfig
- talosctl -n 192.168.15.79 -e 192.168.15.79 --talosconfig ./talosconfig kubeconfig ./kubeconfig
- talosctl apply-config --insecure \
    --nodes 192.168.15.129,192.168.15.34,192.168.15.90 \
    --file worker.yaml

Kubectl get nodes, e ta ai, Cluster Kubernetes rodando num oldbook, ele deve ta fritando, deve, mas ta ai, lab de estudos no ar, e pensa em aplicar algumas soluções para o uso no seu dia a dia, tenho algumas aqui na minha lista, como o piHole ou ADGuard, Jellyfin, Minecraft Server? sei lá, o que tiverem de ideia ai compartilham.

Bom, primeiro artigo, tentando compartilhar um pouco do que estou aprendendo, muita coisa ai com o Jef da Linuxtips, valeu ai o incentivo para começar a pensar assim, compartilhar conhecimento não só ajuda os outros, ajuda a voce mesmo aprender ainda mais! pensa nisso, valeu Jef e Linuxtips, voces são fantasitcos e quem não conhece, tem muito material free top d+ lá, aprendendo muita coisa com voces e vou compartilhar mais. Esse lab deveria fazer parte do Projeto PICK2024, mas, não consegui fazer em tempo, mas vou entregar, atrasado mas vou!

Só Vaiii.

Por hoje, termiando por aqui, shutdown -s -t 00
---





