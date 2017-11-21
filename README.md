# xampp
Configurações para Virtual Host do Xampp para Windows.

1. Inclua a instrução do novo diretório de arquivos no arquivo /xampp/apache/conf/httpd.conf
<Directory "D:/projetos">
    AllowOverride none
    Require all granted
</Directory>

-- Modificar o caminho "D:/projetos" para o que você definiu como seu diretório de projetos.

2. Faça as seguintes modificações e instruções no arquvivo de Virtual Host /xamp/apache/conf/extra/httpd-vhosts.conf
2.1 Descomente a linha com a instrução: NameVirtualHost *:80.
2.2 Inlua a instrução de diretório default
<VirtualHost *:80>
	DocumentRoot C:/xampp/htdocs/   Lembrando de modificar esta linha se não for a mesma da sua instalação.
	ServerName localhost
</VirtualHost>
2.3 Inclua a instruções do novo diretório
<VirtualHost *:80>
    DocumentRoot "D:/projetos"
    ServerName projetos.dev
    ErrorLog "logs/projetos-error.log"
    CustomLog "logs/projetos-access.log" common
    <Directory "D:/projetos">
		Options Indexes FollowSymLinks Includes ExecCGI
        AllowOverride All
        Order allow,deny
        Allow from all
    </Directory>
</VirtualHost>

3. Feito estas configurações abra o arquivo hosts em C:\Windows\System32\drivers\etc
3.1 Inclua a instrução:
127.0.0.1		projetos.dev  # Mesmo nome que foi definido em ServerName
3.2 Salve as modificações * Para salvar os dados é necessário que o bloco de notas tenha sido aberto como "Executar como Administrador".

4. Reinicie o Apache.
