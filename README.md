# TUTORIAL LINUX + APACHE + PHP + MySQL
Este tutorial está baseado na versão do Linux Ubuntu 20.4 LTS.

Os recursos para a instalação da máquina virtual foram configurados para atender a grande maioria de usuários. Entretanto, podem ocorrer casos em que haverá necessidade de ajustes. Para isso, procure tutoriais no YouTube para resolução de problemas.

Aqui o objetivo é mostrar **apenas a instalação e configuração** do ambiente e dos programas.

Os comandos Linux não serão explicados, ficando como sugestão para estudos e aprendizagem do sistema Linux.

## Instalação do VirtualBox (Oracle)
A instalação está baseada em sistemas Windows. Se você já utiliza Linux, não há a necessidade de instalar a máquina virtual e você já pode pular para "**Instalação do Apache, PHP e MySQL**".

Faça o download do programa VirtualBox no endereço: [https://www.virtualbox.org/](https://www.virtualbox.org/) e siga os seguintes passos:

* Execute a instalação seguindo as orientações apresentadas.
* Faça o *download* da imagem de instalação do Linux Ubuntu 20.4 LTS e salve em um local de sua preferência. O arquivo terá aproximadamente 3GB. Link para *download*: [https://ubuntu.com/download/desktop/thank-you?version=20.04.2.0&architecture=amd64](https://ubuntu.com/download/desktop/thank-you?version=20.04.2.0&architecture=amd64)
* Abra o VirtualBox.
* Siga os procedimentos apresentados no vídeo: [link](link).
    + Caso necessário, faça ajustes de acordo com a disponibilidade dos seus recursos de *hardware* (Memória e Vídeo).
    + Se ocorrer algum erro durante a instalação, procure a solução no [StackOverflow](https://stackoverflow.com/) ou no [YouTube](https://www.youtube.com).

## Instalação do Apache, PHP e MySQL
Todas as etapas a seguir estão disponíveis no vídeo: [link](link)

Para executar comandos no terminal do Linux é necessário pressionar a tecla ```ENTER``` para executar o(s) comandos(s).

1. Acesse o **Terminal do Linux** pressionando as teclas as teclas ```CTRL+ALT+T```. Uma outra forma é pressionar a tecla ```Windows``` e digitar **cmd**
2. Primeiro, precisaremos **atualizar o índice** do repositório do sistema para instalar a versão mais recente do Apache2 (Servidor Web)
    + ```sudo apt-get update```

3. A seguir **atualize os pacotes**. (Pressione ```Y``` quando solicitado).
    + ```sudo apt-get upgrade```

4. Abrindo as portas 22 (SSH), 80 (HTTP) and 443 (HTTPS) e habilitando o Firewall (ufw). **Execute um comando de cada vez**.
    + ```sudo ufw allow ssh```
    + ```sudo ufw allow 80```
    + ```sudo ufw allow 443```
    + ```sudo ufw enable```

## Instalando o servidor Apache
+ ```sudo apt install apache2```

## Testando a instalação do Apache
```sudo systemctl status apache2```
1. Pressione CTRL+C para sair.
2. Em seguida, abra o navegador da web (Firefox) e acesse a página de boas-vindas do apache, digitando: [http://localhost](http://localhost).

## Instalando o PHP7.4 (Linguagem de Programação)
```sudo apt install php7.4 php7.4-mysql php-common php7.4-cli php7.4-json php7.4-common php7.4-opcache libapache2-mod-php7.4```

## Verificando a instalação do PHP 7.4
Retorne para o Terminal do Linux e digite:
+ ```php --version```

O resultado será parecido (ou igual) ao apresentado a seguir para sistemas Windows.

```html
PHP 7.3.26 (cli) (built: Jan 5 2021 15:10:35) ( ZTS MSVC15 (Visual C++ 2017) x64
) Copyright (c) 1997-2018 The PHP Group Zend Engine v3.3.26, Copyright (c)
1998-2018 Zend Technologies
```

## Reinicializando o servidor Apache para se integrar ao PHP
```sudo systemctl restart apache2```

## Testando o funcionamento do servidor com o PHP
Digite no Terminal do Linux o comando a seguir para criar um arquivo que mostrará as configurações atuais do PHP no navegador.

```echo '<?php phpinfo(); ?>' | sudo tee -a /var/www/html/phpinfo.php > /dev/null```

Teste no navegador o funcionamento com a url: [http://localhost/phpinfo.php](http://localhost/phpinfo.php)

Se tudo estiver "OK" (aparecer os dados do Apache), exclua o arquivo criado com o seguinte comando:

```sudo rm /var/www/html/phpinfo.php```

## Instalando o servidor de banco de dados MariaDB (MySQL)
```sudo apt install mariadb-server mariadb-client```

## Verificando o *status* da instalação do MySQL
```sudo systemctl status mariadb```
+ Para sair, pressione ```CTRL+C```.

## Protegendo o banco de dados
```sudo mysql_secure_installation```

Como você não tem uma senha de root definida para o banco de dados, você deve simplesmente pressionar ```Enter``` quando solicitado, pressionando **Y** na próxima pergunta para definir uma senha de ```root``` (**mantenha-a segura e protegida!**).

Para as próximas perguntas, você pode pressionar ```Enter``` para aplicar os padrões para cada um dos itens, que eles ajudarão a proteger sua nova instalação do banco de dados.

## Acessando o MySQL via CLI (*Command Line*)
Digite o seguinte comando
+ ```sudo mysql```

Você receberá um [PROMPT] no Terminal Linux com o seguinte formato: ```MariaDB [(none)]>```.

## Criação de usuário no MySQL
Criando um usuário **admin** padrão no banco de dados diferente de **root**. Para isso, digite uma linha de cada vez e pressione ```ENTER``` para executá-la.

**Não esqueça** de colocar o ponto-e-vírgula ";" no final de cada linha.

1. ```CREATE USER 'admin'@'localhost' IDENTIFIED BY 'admin';```
2. ```GRANT ALL PRIVILEGES ON * . * TO 'admin'@'localhost';```
3. ```FLUSH PRIVILEGES;```
4. ```quit;```

## Acessando o MySQL
Para acessar o MySQL com o novo usuário, digite o comando a seguir e informe a senha definida anteriormente quando solicitado:

```sudo mysql -u admin -p```

## Criando um banco de dados no MySQL
``` CREATE DATABASE teste;```

## Selecionando o banco ```aula_teste```
```USE aula_teste;```

## Criando uma tabela de dados
```CREATE TABLE tb_teste (id int primary key not null auto_increment, nome varchar(50));```

## Inserindo registros na tabela (tb_teste)
1. ```INSERT INTO tb_teste (nome) VALUES ("Primeiro Nome");```
2. ```INSERT INTO tb_teste (nome) VALUES ("Segundo Nome");```

## Verificando as inclusões realizadas
```SELECT * FROM tb_teste;```

## Sair do MySQL
```quit;```

## Testando a conexão do PHP com o banco de dados
Criando um diretório para colocar o arquivo de teste de conexão do PHP com o banco de dados:

```sudo mkdir /var/www/html/teste```

## Acessando o diretório criado
```cd /var/www/html/teste```

Para criar o ```script PHP``` e conectar com o banco de dados criado, utilizando a biblioteca PDO de acesso a dados, digite o seguinte comando para abrir o editor de textos (```Nano```):

```sudo nano index.php```

Digite as instruções a seguir no arquivo aberto:

```php
<?php
try {
    $conn = new PDO('mysql:host=localhost;dbname=aula_teste', 'admin', 'admin');
    
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

Para salvar o conteúdo, pressione as teclas ```CTRL+X``` simultaneamente, depois digite ```Y``` e, por fim, pressione ```ENTER```.

Acesse novamente o navegador e digite: [http://localhost/teste](http://localhost/teste)

Se tudo ocorreu como o esperado, deverá ser mostrado no navegador os dados cadastrados anteriormente no banco de dados.

Agora é só estudar e desenvolver suas aplicações.

# Como citar este conteúdo
```
Souza, Edson Melo de. (2021, August 7). Tutorial Linux-PHP-MySQL no VirtualBox.
Available in: https://github.com/EdsonMSouza/tutoriais
```

Ou BibTeX para LaTeX:

```latex
@misc{souzaem2021LAMP,
  author = {Souza, Edson Melo de},
  title = {Tutorial Linux-PHP-MySQL no VirtualBox},
  url = {https://github.com/EdsonMSouza/tutoriais},
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