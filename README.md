Instalação do Painel WEB de Gerenciamento SSH 3.0
 Debian 8 32x / Debian 8 64x

• Sempre que solicitado [Y/N] escolha a opção Y (Sim para Todos).

1 - Vamos instalar o Apache

 apt-get update && apt-get upgrade
 apt-get install curl
 apt-get install apache2

2 - Vamos instalar PHP

 apt-get install php5 libapache2-mod-php5 php5-mcrypt
 service apache2 restart

3 - Vamos instalar MYSQL

• Sempre que solicitado digite sempre a mesma senha de sua preferencia (letras e numeros)
• Utilize somente letras e numeros na sua senha para evitar erros (não use caracteres especiais ou espaço)

 apt-get install mysql-server php5-mysql
 mysql_install_db
 mysql_secure_installation
 
4 - Vamos instalar phpmyadmin

 apt-get install phpmyadmin
 
• Para a seleção do servidor, escolha apache2.
• Selecione Sim quando perguntado se deseja usar dbconfig-common para configurar o banco de dados.
• Você será solicitado para a senha do administrador de banco de dados.
• Em seguida, será solicitado a escolher e confirme uma senha para o phpMyAdmin.

 php5enmod mcrypt
 service apache2 restart
 ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin
 
5 - Vamos instalar o módulo SSH2

 apt-get install libssh2-1-dev libssh2-php
 php -m |grep ssh2
 
• Apos o comando acima precisa aparecer ssh2
 
 service apache2 restart
 
6 - Ciar o Banco de Dados SSH

• Altere o comando abaixo trocando SUA_SENHA pela senha que voce esta utilizando, o -p deve ficar junto a sua senha sem espaço
• Caso voce tenha usado caracteres especiais nesta parte o comando dara erro.

 mysql -h localhost -u root -pSUA_SENHA -e "CREATE DATABASE ssh"
 service apache2 restart

7 - Instalar o Painel de Gerenciamento

 cd /var/www/html
 wget -O painel.zip https://www.dropbox.com/s/f2yo8u7b42imysv/painelssh.zip?dl=0 && mv painel.zip /var/www/html       
 apt-get install unzip
 unzip painel.zip
 rm painel.zip

8 - Configurar arquivo de acesso ao Banco de Dados

 nano /var/www/html/pages/system/pass.php

• O comando acima cria o arquivo pass.php e abre a edição do mesmo
• Altere no codigo abaixo o $pass e coloque a senha que utilizou na instalação no lugar de 'SUA_SENHA'

 <?php $pass = 'SUA_SENHA';?>

• Copie o codigo acima e cole na edição do arquivo pass.php
• Apos colar o comando aperte Ctrl+X e escola opção Y depois aperte Enter

9 - Configurar Tabelas do Banco de Dados

• Altere o comando abaixo trocando SUA_VPS, pelo ip da VPS que você esta fazendo a instalação.

 curl SUA_VPS/create.php
 rm create.php
 service apache2 restart

10 - Configurarando comando de Agendamento Crontab

• Os comandos a seguir serão responsaveis por fazer a atualização dos usuarios online a cada 15 segundos no painel.
• Tambem por reiniciar o servidor todos os dias as 03:00hs.

 nano /etc/crontab

• Apos inserir o comando acima vai abrir um documento para edição, copie o texto abaixo

* * * * * root /usr/bin/php /var/www/html/pages/system/cron.php 
* * * * * root /usr/bin/php /var/www/html/pages/system/cron.ssh.php 
* * * * * root /usr/bin/php /var/www/html/pages/system/cron.sms.php 
* * * * * root /usr/bin/php /var/www/html/pages/system/cron.online.ssh.php

10 * * * * root /usr/bin/php /var/www/html/pages/system/cron.servidor.php

• As bolinhas e quadrados acima deverão ser substituidos por *

• Cole no documento na ultima linha.

• Apos colar o comando aperte Ctrl+X e escola opção Y depois aperte Enter

11 - Alterando a Data e a Hora

 dpkg-reconfigure tzdata
 
• Escolher opção America e depois São Paulo.

 service apache2 restart

FINAL
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


