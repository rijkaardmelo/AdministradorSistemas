<h1 align="center">Exemplo de Sintaxe de Comandos SCP Linux </h1>

    scp [other options] [source username@IP]:/[directory and file name] [destination username@IP]:/[destination directory]


* [other options] são modificadores que você pode adicionar ao comando SCP. Vamos mostrar os mais populares dele mais abaixo.

* [source username@IP] é o nome do usuário e o IP da máquina que tem o arquivo que você quer. Seria algo como root@123.123.123.12.

* :/ informa o comando SCP que você está prestes a digitar no diretório fonte.

* [directory and file name] é onde o arquivo está localizado e o nome dele. Se parece com algo como /users/Edward/Desktop/SCP.png

* [destination username@IP] é o nome do usuário e do IP da máquina de destino.

* [destination directory] é o diretório onde o arquivo será salvo.

As opções de flags comuns:   

* -P possibilita especificar uma entrada diferente para o servidor (a porta padrão para a porta TCP para o comando é a 22).
* -c dá a possibilidade de especificar a encriptação do algoritmo que o cliente vai usar. Alguns dos valores que você pode usar são ‘aes256-ctr’, ‘aes256-cbc’, ‘blowfish-cbc’, ‘arcfour’, ‘arcfour128’, ‘arcfour256’, ‘cast128-cbc’, aes128-ctr’, ‘aes128-cbc’, ‘aes192-ctr’, ‘aes192-cbc’ e 3des-cbc’. A opção padrão na configuração do shell é ‘AnyStdCipher’
* -q vai executar a operação em modo silencioso, o que significa que apenas os erros críticos é que serão mostrados.
* -r é para cópia recursiva, que vai incluir todos os subdiretórios.
* -4 or -6 pode ser usado se você quiser escolher a versão do protocolo empregada, sendo IPv4 ou IPv6. Você também pode configurar os requerimentos da configuração de IP mais exaustivamente com a palavra-chave da família de endereço.
* -p vai preservar os tempos iniciais de modificação e atributos do arquivo. .
* -u vai apagar a fonte do arquivo logo depois que a transferência for completada.
* -c vai habilitar a compressão de dados enquanto a operação de transferência está sendo executada.

<h3 align="center"> Arquivo Local para um Local Remoto </h3>

Se você não tem uma confirmação automática do cliente SSH, você vai ser solicitado para inserir a senha da máquina local do usuário e versá uma métrica de progresso.

    scp /users/Edward/desktop/scp.zip root@191.162.0.2:/writing/article

root@191.162.0.2’s password:
novel3.zip   100% 0 0.0KB/s 00:00

Mas, vamos dizer que a máquina remota está configurada para responder às conexões SSH e uma porta que não seja a 22.
    
    scp -P 2322 /users/Edward/desktop/scp.zip root@191.162.0.2:/writing/article

Se você quiser mudar o nome do arquivo durante a operação da transferência.
    
    scp /users/Edward/desktop/scp.zip root@191.162.0.2:/writing/article/howtoscp.zip

Se você quer copiar um diretório que tem mais arquivos e/ou mais subdiretórios, use a linha de comando -r.
    
    scp -r /users/Edward/desktop root@191.162.0.2:/writing/article

<h3 align="center"> Arquivo Remoto para uma Máquina Local </h3>

    scp root@191.162.0.2:/writing/articles/SCP.zip Users/Edward/Desktop

<h3 align="center"> Arquivo Remoto para Outro Local Remoto </h3>

    scp root@191.162.0.2:/writing/article/scp.zip edward@11.10.0.1:/publishing