# TUTORIAL LINUX + APACHE + PHP + MySQL
<code><img height="20" src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/terminal/terminal.png"></code>
<code><img height="20" src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/linux/linux.png"></code>
<code><img height="20" src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/php/php.png"></code>
<code><img height="20" src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/mysql/mysql.png"></code>

## __$\color{red}{ATENÇÃO}$__
Este tutorial está baseado na versão do Linux Ubuntu 20.4 LTS.

**Uma versão atualizada para o Linux Ubuntu 22.04.3 LTS** está disponível em: [https://github.com/EdsonMSouza/Apache-PHP-MariaDB](https://github.com/EdsonMSouza/Apache-PHP-MariaDB)

## Introdução

Os recursos para a instalação da máquina virtual foram configurados para atender a grande maioria de usuários. Entretanto, podem ocorrer casos em que haverá a necessidade de ajustes. Para isso, procure tutoriais no YouTube ou Google para resolução de problemas.

Aqui o objetivo é mostrar **apenas a instalação e configuração** do ambiente e dos programas.

Os comandos Linux não serão explicados, ficando como sugestão para estudos e aprendizagem do sistema operacional Linux.

## Instalação do VirtualBox (Oracle)
A instalação está baseada em sistemas Windows. Se você já utiliza o Linux, não há a necessidade de instalar a máquina virtual e você já pode pular para "**Instalação do Apache, PHP e MySQL**".

Faça o *download* do programa VirtualBox no endereço: [https://www.virtualbox.org/](https://www.virtualbox.org/) e siga os seguintes passos:

* Execute a instalação seguindo as orientações apresentadas.
* Faça o *download* da imagem de instalação do Linux Ubuntu 20.4 LTS e salve em um local de sua preferência. O arquivo terá aproximadamente 3GB. Link para *download*: [https://ubuntu.com/download/desktop/thank-you?version=20.04.2.0&architecture=amd64](https://ubuntu.com/download/desktop/thank-you?version=20.04.2.0&architecture=amd64)
* Abra o VirtualBox.
* Crie uma máquina virtual e dê o nome de Linux Ubunut 20.4 LTS.
* Em "Type" (Tipo), selecione Linux.
* Em "Version" (Versão), selecione Ubuntu (64-bit) ou (32bit) - depende a versão que foi baixada.
* Selecione a quantidade RAM. É recomendado no mínimo 1024MB (1GB).
* Selecione a segunda opção para o tipo de "Hard Disk" (Disco Rígido) - "Virtual".
* Ma próxima tela, selecione a primeira opção ```VDI```.
* Na próxima tela, selecione a primeira opção ou "Dinamicamente Alocado".
* Informe o tamanho para o disco a ser criado. É recomendado no mínimo 10GB.
* Clique em criar (Create) e aguarde.
* Dê um duplo clique sobre o nome da máquina criada para inicializá-la.
* Se não for identificada a imagem do Linux, clique no menu Dispositivos (Devices) e adicione um Disco Ótico Virtual, apontando para o local onde a imagem do Linux foi salva.
* Aguarde a inicialização, e prossiga com a instalação do Linux, selecionando "**Install Ubutuntu**" (Instalar o Ubuntu).

Caso necessário, faça ajustes de acordo com a disponibilidade dos seus recursos de *hardware* (Memória e Vídeo).

Se ocorrer algum erro durante a instalação, procure a solução no [StackOverflow](https://stackoverflow.com/) ou no [YouTube](https://www.youtube.com).

Você pode visualizar as telas de instalação (em inglês) em [https://itsfoss.com/install-linux-in-virtualbox/](https://itsfoss.com/install-linux-in-virtualbox/).
## Instalação do Apache, PHP e MySQL
Siga corretamente todas as etapas a seguir para a isntalação dos programas necessários, assim como suas configurações.

Para executar comandos no terminal do Linux é necessário pressionar a tecla ```ENTER``` ao final de cada instrução.

Acesse o **Terminal do Linux** pressionando as teclas ```CTRL+ALT+T```. Uma outra forma é pressionar a tecla ```Windows``` e digitar **cmd**

Primeiro, precisaremos **atualizar o índice** do repositório do sistema para instalar a versão mais recente do Apache2 (Servidor Web)

```sudo apt-get update```

A seguir **atualize os pacotes**. (Pressione ```Y``` quando solicitado).

```sudo apt-get upgrade```

Abrindo as portas 22 (SSH), 80 (HTTP) and 443 (HTTPS) e habilitando o Firewall (ufw). **Execute um comando de cada vez**.
+ ```sudo ufw allow ssh```
+ ```sudo ufw allow 80```
+ ```sudo ufw allow 443```
+ ```sudo ufw enable```

## Instalando o servidor Apache
```sudo apt install apache2```

## Testando a instalação do Apache

```sudo systemctl status apache2```

1. Pressione CTRL+C para sair.
2. Em seguida, abra o navegador da web (Firefox) e acesse a página de boas-vindas do apache, digitando: [http://localhost](http://localhost).

## Instalando o PHP7.4 (Linguagem de Programação)
```sudo apt install php7.4 php7.4-mysql php-common php7.4-cli php7.4-json php7.4-common php7.4-opcache libapache2-mod-php7.4```

## Verificando a instalação do PHP 7.4
Retorne para o Terminal do Linux e digite:

```php --version```

O resultado será semelhante ao apresentado a seguir.

```html
PHP 7.3.26 (cli) (built: Jan 5 2021 15:10:35) ( ZTS MSVC15 (Visual C++ 2017) x64
) Copyright (c) 1997-2018 The PHP Group Zend Engine v3.3.26, Copyright (c)
1998-2018 Zend Technologies
```
## Reinicializando o servidor Apache para integrar o PHP
```sudo systemctl restart apache2```

## Testando o funcionamento do servidor com o PHP
Digite no Terminal do Linux o comando a seguir para criar um arquivo que mostrará as configurações atuais do PHP no navegador.

```echo '<?php phpinfo(); ?>' | sudo tee -a /var/www/html/phpinfo.php > /dev/null```

Teste no navegador o funcionamento com a url: [http://localhost/phpinfo.php](http://localhost/phpinfo.php)

Se tudo estiver "OK", será mostrada uma página com as informações do PHP.

Exclua o arquivo criado com o seguinte comando:

```sudo rm /var/www/html/phpinfo.php```

## Instalando o servidor de banco de dados MariaDB (MySQL)
```sudo apt install mariadb-server mariadb-client```

## Verificando o *status* da instalação do MariaDB
```sudo systemctl status mariadb```
+ Se o comando não finalizar, pressione ```CTRL+C``` para sair.

## Protegendo o MariaDB
```sudo mysql_secure_installation```

Como não existe uma senha de  **root** definida para o banco de dados, você deve simplesmente pressionar ```Enter``` quando receber a seguinte mensagem: ```Enter current password for root (enter for none):```

Na próxima pergunta, pressione **Y** para definir uma senha de **root** (***mantenha-a segura e protegida!***) e siga as orientações.

Para as próximas perguntas, você pode pressionar ```Enter``` para cada um dos itens.

## Acessando o MySQL via CLI (*Command Line*)
Digite o seguinte comando:

```sudo mysql```

Você terá na tela algo semelhante a:

```MariaDB [(none)]>```

## Criação de usuário no MariaDB
Criando um usuário **admin** padrão no banco de dados diferente de **root**.

Para isso, digite as linhas abaixo (**uma linha por vez**) e pressione ```ENTER``` para executá-la.

**Não esqueça** de colocar o ponto-e-vírgula "**```;```**" no final de cada linha.

1. ```CREATE USER 'admin'@'localhost' IDENTIFIED BY 'admin';```
2. ```GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost';```
3. ```FLUSH PRIVILEGES;```
4. ```quit;```

## Acessando o MariaDB
Para acessar o MariaDB com o novo usuário criado, digite o comando a seguir e informe a senha definida anteriormente (**admin**) quando solicitado:

```sudo mysql -u admin -p```

## Criando um banco de dados no MariaDB
```CREATE DATABASE bd_teste;```

## Selecionando o banco ```bd_teste```
```USE bd_teste;```

## Criando uma tabela de dados
```CREATE TABLE tb_teste (id int primary key not null auto_increment, nome varchar(50));```

## Inserindo registros na tabela (tb_teste)
1. ```INSERT INTO tb_teste (nome) VALUES ("Primeiro Nome");```
2. ```INSERT INTO tb_teste (nome) VALUES ("Segundo Nome");```

## Verificando as inclusões realizadas
```SELECT * FROM tb_teste;```

O resultado deverá ser igual ao mostrado abaixo.

```sql
+----+---------------+
| id | nome          |
+----+---------------+
|  1 | Primeiro Nome |
|  2 | Segundo Nome  |
+----+---------------+
2 rows in set (0.000 sec)

```
## Sair do MariaDB
```quit;```

## Testando a conexão do PHP com o banco de dados MariaDB
Criando um diretório para colocar um arquivo de teste de conexão do PHP com o banco de dados criado anteriormente **bd_teste**:

```sudo mkdir /var/www/html/teste```

## Acessando o diretório criado
```cd /var/www/html/teste```

Execute o comando ```ls -la``` para realizar a listagem do diretório e verificar se ele está vazio. O resultado deste comando pode ser visualizado abaixo.

```bash
drwxr-xr-x 2 root root 4096 ago  8 21:22 .
drwxr-xr-x 3 root root 4096 ago  8 21:22 ..
```

Para criar o ```script PHP``` (programa) e fazer a conexão com o banco de dados **bd_teste**, vamos utilizar a biblioteca PDO de acesso a dados. Para isso, digite o seguinte comando para abrir o editor de textos (```Nano```):

```sudo nano index.php```

Digite as instruções a seguir no arquivo aberto:

```php
<?php
try {
    $conn = new PDO('mysql:host=localhost;dbname=bd_teste', 'admin', 'admin');
    
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

    $data = $conn->query('SELECT * FROM tb_teste');

    foreach($data as $key => $value) {
        print("Id: " . $value[0] . "</br>");
        print("Nome: " . $value[1] . "</br>");
        print("</br></br>");
    }
} catch(PDOException $e) {
    echo 'ERROR: ' . $e->getMessage();
}
```

Para salvar o arquivo, pressione as teclas ```CTRL+X``` simultaneamente, depois digite ```Y``` e, por fim, pressione ```ENTER``` para fechar o editor de textos.

Execute novament o comando ```ls -la``` para realizar a listagem do diretório e verificar se o arquivo foi criado corretamente. O resultado deste comando pode ser visualizado abaixo, mostrando o arquivo ```index.php```.

```bash
drwxr-xr-x 2 root root 4096 ago  8 21:27 .
drwxr-xr-x 3 root root 4096 ago  8 21:22 ..
-rw-r--r-- 1 root root  469 ago  8 21:27 index.php
```

# Testando o funcionamento do programa
Acesse novamente o navegador e digite: [http://localhost/teste](http://localhost/teste)

Se tudo ocorreu como o esperado, deverá ser mostrado no navegador os dados cadastrados anteriormente no banco de dados.

Agora é só estudar e desenvolver suas aplicações.

# Como citar este conteúdo
```
Souza, Edson Melo de. (2021, August 7). Tutorial Linux-PHP-MySQL no VirtualBox.
Available in: https://github.com/EdsonMSouza/tutorial_lamp_virtualbox
```

Ou BibTeX para LaTeX:

```latex
@misc{Souzaem2021LAMP,
  author = {Souza, Edson Melo de},
  title = {Tutorial Linux-PHP-MySQL no VirtualBox},
  url = {https://github.com/EdsonMSouza/tutorial_lamp_virtualbox},
  year = {2021},
  month = {August}
}
```
 
# License

[![CC BY-SA 4.0][cc-by-sa-shield]][cc-by-sa]

This work is licensed under a
[Creative Commons Attribution-ShareAlike 4.0 International License][cc-by-sa].

[![CC BY-SA 4.0][cc-by-sa-image]][cc-by-sa]

[cc-by-sa]: http://creativecommons.org/licenses/by-sa/4.0/
[cc-by-sa-image]: https://licensebuttons.net/l/by-sa/4.0/88x31.png
[cc-by-sa-shield]: https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg
