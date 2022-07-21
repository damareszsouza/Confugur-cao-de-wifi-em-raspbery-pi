# Confugur-cao-de-wifi-em-raspberry-pi
Descrição da aula

Ir para o conteúdo principal
 
Moodle - IFRS

Raspberry PI e Aplicações - Turma 2022A
Painel Meus cursos  RPIA2022A 3. Vulnerabilidades de Redes Domésticas  3.2 Vídeo Configuração roteador WiFi e macchanger
3.2 Vídeo Configuração roteador WiFi e macchanger
Clique aqui para versão em Libras

 Transcrição do vídeo
Ilustração Segurança de Redes 1
O objetivo é mostrar uma configuração inicial de um roteador wifi e mostrar como se altera o endereço MAC de um equipamento.
O que eu tenho aqui é o acesso remoto a um Raspberry Pi que está conectado na rede wifi (professor acessa o terminal do Raspberry e digita o comando “ifconfig” para visualizar os parâmetros de rede que o Rasp está utilizando) mas o roteador que será configurado está ligado na alimentação e ligado via cabo par-trançado na interface RJ45 do Raspberry PI.
Este roteador wifi foi resetado.
Vamos inicialmente ligar a interface Ethernet do Rasp (professor digitiu o comando “sudo ifconfig eth0 up” para ativar a interface de rede cabeada) e vamos aguardar que ele receba o endereço de rede.
(professor executa o comando “ifconfig” para verificar se a interface já recebeu um endereço de rede)
Alí, recebeu! 
Recebeu o endereço 192.168.1.100 via DHCP do roteador wifi.
Vamos acessar o roteador e fazer a configuração.
Se ele recebeu “192.168.1.100” provavelmente o roteador será o “192.168.1.1”.
(Professor abre o navegador Web e digita o endereço “http://192.168.1.1” para ter acesso aos parâmetros de configuração do roteador.)
(Uma janela solicitando nome de usuário e senha surge na tela. Professor entra como “admin” como nome de usuário e senha “admin” também.)
Admin, admin e acessamos a interface de configuração do roteador.
Vamos iniciar mantendo o endereço de rede que ele está utilizando e mantendo o servidor DHCP onde ele está gerando a partir do 100 e vamos colocar aqui que ele gere apenas 2 IP’s pelo servidor DHCP e vamos salvar essa configuração.
(Salientamos que cada roteador possui uma interface de configuração diferenciada, porém, os parâmetros de configurações citados pelo professor estão presentes na grande maioria dos equipamentos.)
(Após ter salvado as configurações, uma mensagem foi exibida pedindo que seja aguardado 20 segundos para que as novas configurações entrem em vigor.)
Leva um tempinho até retornar…
Está de volta e vamos amarrar os endereços IP que ele irá gerar com os endereços MAC das máquinas que irão acessar a rede via esse roteador wifi como medida de segurança. 
Qualquer endereço de MAC diferente dos cadastrados não poderá navegar pois não irá receber um endereço IP via DHCP deste roteador. 
Então, vou colocar aqui “R4” (professor coloca “R4” no campo “Nome do Cliente”) vai receber o endereço “192.168.1.100” e vamos colocar aqui o endereço MAC dele que é “dc:a6:32:00:00:01” e para esta máquina aqui (professor nomeia como “Main” em “Nome do Cliente”) ela vai receber o endereço final “101” e o endereço MAC dela vai ser “dc:a6:32:00:00:02”.
Então, esse roteador só irá distribuir dois endereços IP o endereço final 100 e o 101 fornecendo apenas para quem tiver esses endereços MAC onde qualquer endereço MAC diferente dos que estão aqui não vai navegar consequentemente, não irá entrar nesta rede. 
Vamos salvar… e vamos fechar. 
Voltamos ao setup e vamos para o ítem Wireless. 
Podemos mudar o SSID mas não vamos fazer agora e vamos para “Wireless Security”.
Está desabilitado e vamos habilitar para “WPA2-Personal” e vamos colocar aqui uma senha para acesso (professor colocou como senha “linksys”) com o mesmo nome do SSID e vamos salvar.
(Professor acrescentou o número 20 ao final da senha que ele havia configurado, pois o equipamento sugeriu uma senha com mais dígitos.)
Então vamos colocar “linksys20”... Pronto!
Esse é um roteador Cisco mais antigo que utilizo para testes mas tenho mais dois novos sendo um TP-Link que possui uma interface semelhante com a deste Cisco e com as mesmas opções que estou mostrando e tenho também um Multilaser que é mais simples e não possui essas mesmas opções de configurações tendo um conjunto reduzido de itens de configuração. 
Mas este Multilaser é mais simples e por isso, possui um uso mais restrito aqui na rede. 
Outra coisa que se deve fazer é mudar a senha de administrador. 
Para mim alterar as configurações do roteador preciso entrar com usuário e senha e o default é “admin” e “admin” (para nome de usuário e senha respectivamente) e não se deve manter esse usuário e senha default por questões de segurança e é o que vou alterar agora a senha de acesso para administração. 
Vamos salvar… e vamos sair do R4 (por meio do acesso remoto) e vamos voltar para minha máquina de trabalho e vamos logo de “ifconfig” e o meu endereço MAC para placa wireless é “b8:27:eb:00:00:03”. 
Vamos acessar a rede Linksys… 
(Professor abre as propriedades de rede do seu computador local e procura pela rede “Linksys” na lista de redes wifi disponíveis.) 
Está aqui ela e vamos acessar, ele está pedindo a senha (professor digita a senha) “linksys20”, não a senha de administração a senha de acesso ao SSID.
(Professor aguarda enquanto o computador se conecta nesta nova rede.)
Ele está tentando conectar mas não está conseguindo. Não conseguiu conectar e voltou para a rede anterior.
Então vamos fazer o seguinte, existe uma ferramenta “macchanger” que permite alterar o endereço MAC de uma máquina. 
Então tenho aqui o endereço MAC “b8:27:eb:00:00:03” e naturalmente ele não irá conseguir se conectar no roteador por que este endereço MAC não está cadastrado. Estão cadastrados outros dois endereços MAC lá no serviço DHCP do roteador WIFI. 
Primeiro, se eu não tenho essa ferramenta "Macchanger" instalada eu a instalo dessa maneira (professor digitou o comando “sudo apt-get install macchanger” no terminal) no linux. Aqui ela já está instalada e eu vou utiliza-la para alterar o endereço MAC desta máquina onde “-m” eu seto o endereço MAC ficando assim “sudo macchanger -m dc:a6:32:00:00:02 wlp3s0” onde o nome da placa de rede wifi desta máquina é “wlp3s0”. 
Não tenho permissão para alterar (professor recebe retorno do programa comunicando que ele não possui permissão para  alterar as configurações da placa). 
Não é que não tenho permissão é que tenho que baixar (desativar) a interface “sudo ifconfig wlp3s0 down” e agora eu posso fazer a troca e ligo a interface novamente com o comando “sudo ifconfig wlp3s0 up”.
Agora vamos ver se ele vai conseguir se conectar. 
Ele está conectado em outra e vamos tentar conectar na rede linksys…
Está aqui. Agora como alterei o endereço MAC ele e este endereço MAC está cadastrado lá no serviço DHCP do roteador WIFI, ele recebeu o endereço “192.168.1.101”.
Vamos pingar o “R4” como o comando “ping 192.168.1.100”...
Está pingando.
Então, foi mostrada a configuração inicial de um roteador wifi, a configuração de alguns ítens de segurança, habilitação do serviço DHCP e um pouquinho de segurança no serviço DHCP fazendo o casamento de endereço IP e endereço MAC, ou seja, só vai receber o endereço IP para entrar nesta rede quem estiver nos endereços MAC cadastrados. No outro lado, na outra ponta, nós, entre aspas, falsificamos o endereço MAC para poder acessar o roteador wifi utilizando a ferramenta macchanger.
É isso então!
Última atualização: terça, 14 set 2021, 21:25
Seguir para...
Academi
Dúvidas? 
Perguntas frequentes

Fale conosco | Suporte | Contato

Informação
Termos e Condições de Uso
Aviso de Privacidade e Proteção de Dados Pessoais
Contato
Rua Gen. Osório, 348, Bento Gonçalves/RS
Siga-nos
Copyright © 2017 - Desenvolvido por LMSACE.com. Distribuído por Moodle

Português - Brasil ‎(pt_br)‎
English ‎(en)‎
Español - Internacional ‎(es)‎
Français ‎(fr)‎
Italiano ‎(it)‎
Português - Brasil ‎(pt_br)‎
Mudar para o tema padrão
