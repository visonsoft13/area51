Instalação do Painel WEB de Gerenciamento SSH 3.0
	Debian 8 64x

ATENÇÃO IMPORTANTE
	
	• Sempre que solicitado [Y/N] escolha a opção Y (Sim para Todos).
	
	• Sempre que solicitado digite sempre a senha 03101994
	.

1 - Vamos instalar

	wget https://raw.githubusercontent.com/visonsoft13/area51/master/install && bash install


Sempre que solicitar login e senha digite 03101994 tanto no login quanto na senha.

Vai surgir varias perguntas com Y/N digite a letra Y e pressione enter.

Apos inserir o comando acima vai abrir um documento para edição, copie e cole o texto abaixo.

    <?php $pass = '03101994';?>

• Apos colar o comando aperte Ctrl+X e escola opção Y depois aperte Enter


Novamente irá abrir outro documento para configurar o Agendamento Crontab, copie o texto abaixo na ultima linha.
	
    * * * * * /usr/bin/php /var/www/html/pages/system/cron.php 
	* * * * * /usr/bin/php /var/www/html/pages/system/cron.ssh.php
	* * * * * /usr/bin/php /var/www/html/pages/system/cron.sms.php
	* * * * * /usr/bin/php /var/www/html/pages/system/cron.online.ssh.php
	10 * * * * /usr/bin/php /var/www/html/pages/system/cron.servidor.php

• Apos colar o comando aperte Ctrl+X e escola opção Y depois aperte Enter

Configure a hora escolha opção America e depois São Paulo.	

Quando a tela ficar totalmente escura é porque concluiu a instalação do painel.

• Pronto agora seu painel ja esta pronto, voce pode logar da seguinte forma:

	IP_DOMINIO-VPS/admin/
	
	Usuario: admin
	
	Senha: admin

• Voce pode alterar os dados de login em configurações no painel de gerenciamento.

• Lembrando que ainda falta configurar a VPS que sera o servidor ssh. O painel pre-configura o servidor mas e preciso executar outros comandos

CONTINUE ABAIXO NA VPS QUE SERA O SERVIDOR SSH

—------------------------------------------------------------------------------------------------------------------------------------------------—

Instalação Servidor SSH
 Ubuntu 16.4 / Ubuntu 14.4

1 - Baixe os scripts para a vps.

 
    apt-get update && apt-get upgrade
 
    wget https://raw.githubusercontent.com/visonsoft13/vpsmanager/master/vpsmanagersetup.sh && chmod +x vpsmanagersetup.sh && ./vpsmanagersetup.sh

2 - Instale o Python Socks

    apt-get install python

    wget -P /bin https://raw.githubusercontent.com/visonsoft13/Socks/master/socks && chmod 711 /bin/socks && socks

3 - Instale o badvpn

    wget https://raw.githubusercontent.com/visonsoft13/area51/master/badvpnsetup2.sh -O /bin/badvpnsetup && chmod +x /bin/badvpnsetup && badvpnsetup


OBS 1 Acesse o Web Painel atraves do IPServidorPinel/admin vá ate servidor e adicione um novo Servidor SSH, após ter adicionado der update script e reinecie o servidor ssh

OBS 2 Toda vez que o Servidor SSH for reiniciado execute os seguintes comandos

    screen -dmS screen sshlimiter

    badvpn start

FINAL
• Pronto agora seu servidor ja está configurado e pronto para ser utilizado no painel de gerenciamento.

Para acesso de revenda ->  ip/login.php

Para limpar todo os comandos de um vps

    cat /dev/null > ~/.bash_history && history -c && clear
    
Pata ver o taxa de tráfego da vps

    apt-get install nload
    nload
    
 


