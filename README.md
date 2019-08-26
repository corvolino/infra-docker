# docker with docker-compose
creation of work development in docker

* Serviços Disponíveis
  * Apache - with PHP
  * Nginx
  * Postgresql
  * MySql
  * PhpMyadmin
  * PhpPgadmin
  * PHP - with composer
  * Angular
  * React
  * Mongodb
  * Mongo Express

<strong>Para usuários do docker toolbox, o projeto deve ser clonado dentro da pasta pessoal do usuário</strong><br>

<strong>Todos os projetos web devem ficar na pasta <strong>sites</strong> do projeto</strong>

* Configurando Dominio Local

  * <s>Windows</s><br>
    0 - É realmente necessário usar Windows em sua máquina? Sério?
    1 - Ir até a pasta <code>C:\Windows\System32\drivers\etc</code>.<br>
    2 - Dar permissão total ao arquivo <code>hosts</code> para o usuário logado.<br>
    3 - Adicionar a seguinte linha no final do arquivo: <code>127.0.0.1	projeto.local</code> (O nome do projeto fica a seu critério)<br>
    Para usuários do docker toolbox, o IP será o resultado do comando <code>$ docker-machine ip default</code><br>
    4 - Criar um atalho na área de trabalho para projetos futuros (Opcional facilitador).<br>
  * Linux/Mac<br>
    1 - Editar o arquivo <code>/etc/hosts</code><br> e adicione no final do arquivo <code>127.0.0.1	projeto.local</code> (O nome do projeto fica a seu critério)<br>
  
 *  Baixar VSCode: https://code.visualstudio.com/<br>
 *  Instalar plugin do docker: https://marketplace.visualstudio.com/items?itemName=PeterJausovec.vscode-docker&ssr=true<br>

* Criando containers

  * Criando volumes para postgres e mysql (Obs.: Comandos apenas se tiver erro de criação de volumes para bases de dados)<br>
    <code>$ docker create volume data-postgres</code><br>
    <code>$ docker create volume data-mysql</code><br>
  * Editar o arquivo <code>.env</code> de acordo as suas necessidades.<br>
  * Instanciar container com o serguinte comando:
    <code>$ docker-compose up -d serviço1 serviço2 ...</code><br><br>

* Configuração de VirtualHost nos containers Apache e Nginx

  * Apache<br>
  
    1 - Ir até a pasta <code> apache/sites-avaliable</code> e Editar as diretivas do arquivo sites.conf:<br>
        <code>ServerName projeto.local</code> (Colocar o dominio local criado).<br>
        <code>DocumentRoot /var/www/html/teste</code> e <code>Directory "/var/www/html/teste"</code>, Alterar O final "teste" pelo nome da pasta do seu projeto.<br>
    2 - Acessar o container do apache pelo vscode e digitar o seguinte comando: <code># a2ensite sites.conf</code>.<br>
    3 - Reiniciar o container pelo vscode.<br>
    4 - Caso queira criar mais VirtualHost, crie uma copia do arquivo <code>sites.conf</code> na mesma pasta, renomeie-o de acordo a sua escolha (ex.: projeto.conf) e repita o processo adaptando-se ao novo arquivo criado.<br>
  
  * Nginx <br>
  
    1 - Ir até a pasta <code>nginx</code> e Editar as diretivas do arquivo sites.conf:<br>
      <code>root /var/www/html/teste;</code> Alterar O final "teste" pelo nome da pasta do seu projeto.<br>
      <code>server_name site.dev;</code> (Colocar o dominio local criado).<br>
    1.1 - Edite localmente seu <code>/etc/hosts</code> e adicione o mesmo nome no qual adicionou em <code>server_name</code><br>
    2 - Reiniciar o container pelo vscode.<br>
    3 - Caso queira criar mais VirtualHost, crie uma copia do arquivo <code>sites.conf</code> na mesma pasta, renomeie-o de acordo a sua escolha (ex.: projeto.conf) e repita o processo adaptando-se ao novo arquivo criado.<br>
    4 - Abra o container do PHP e digite <code>composer install</code> para instalar o composer<br>
    5 - Abra o container do PHP e de permissão na pasta <code>html/teste</code><br>
    6 - Reinicie o containter do Nginx após modificações nele.<br>
    
 A partir de agora a gerência dos containers será através do VScode (iniciar e parar).
  
  
