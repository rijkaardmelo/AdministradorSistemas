Exemplo de Sintaxe de Comandos SCP Linux

Um comando SCP básico:

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

Arquivo Local para um Local Remoto

Exemplo:

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


Arquivo Remoto para uma Máquina Local
Neste processo, a fonte e o alvo do comando ficam reservados. Então, isso deve refletir na sua sintaxe. Desta vez, estamos tentando copiar scp.zip do mesmo host remoto para a nossa máquina local.

scp root@191.162.0.2:/writing/articles/SCP.zip Users/Edward/Desktop
Novamente, isso deve pedir um login SSH, onde você precisa colocar sua senha de acesso. A menos que a autenticação tenha sido desabilitada por privilégios sudo. Ou que você forçou o cliente SSH a usar uma chave privada na sua máquina.

Arquivo Remoto para Outro Local Remoto
Para copiar arquivos de um host remoto para outro, você vai ter que inserir senhas para ambas as contas depois de executar este comando no seu terminal.

Exemplo:

scp root@191.162.0.2:/writing/article/scp.zip edward@11.10.0.1:/publishing
O comando acima copia a fonte do arquivo /writing/article/scp.zip do primeiro host para o segundo. Para copiar pastas, apenas adicione a opção -r e especifique o caminho da pasta ao invés do arquivo dentro dela, como fizemos antes.

Em circunstâncias normais, o arquivo vai direto do primeiro host remoto para o segundo. Porém, se você quiser redirecionar a operação através da sua máquina, é só adicionar a opção -3:

scp -3 root@191.162.0.2:/writing/article/scp.zip edward@11.10.0.1:/publishing
E é isso!

Resumo
Neste artigo, você aprendeu a como transferir arquivos facilmente entre hosts locais e remotos usando um comando SCP. Isso é extremamente útil quando você está trabalhando com múltiplos servidores.

O protocolo da cópia de segurança faz com que seja mais fácil copiar informações com sucesso de um host remoto para outro sem precisar fazer login.

Além disso, esse método de transferência remota de arquivos encripta seus dados com um shell seguro, o que garante a confiabilidade da informação que está sendo transmitida.