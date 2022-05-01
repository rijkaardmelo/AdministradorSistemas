O Que é Comando SCP?
Baseado em Berkeley Software Distribution (BSD) Remote Copy Protocol, o SCP (Secure Copy) é um protocolo de rede para transferências de arquivos.

Com ele, você pode transferir arquivos de forma fácil e segura entre um local remoto e um host ou entre dois locais remotos.

Desenvolvedores full-stack frequentemente usam um comando SCP para funções de autenticação e encriptação sem precisar usar softwares externos, como o Github.

É uma maneira bem acessível de prevenir que seus dados fiquem expostos para outros usuários ao mesmo tempo em que preserva a confidencialidade.

Na essência, o SCP é uma mistura de RCP e SSH (Secure Shell). Ele se baseia no primeiro para realizar ações de cópia. Enquanto que, no segundo, ele usa toda a parte de encriptação de informação para autenticar sistemas remotos.

Diferentemente do Rsync, tudo o que você precisa para usar um comando SCP com sucesso é um nome de usuário e senha. Ou, ainda, uma frase que serve como senha para os sistemas envolvidos na transferência. Ele agiliza o processo, pois você não precisa fazer login em nenhum deles.

Exemplo de Sintaxe de Comandos SCP Linux
Um comando SCP básico se parece com isso:

scp [other options] [source username@IP]:/[directory and file name] [destination username@IP]:/[destination directory]
Pode parecer complicado num primeiro momento. Mas vamos explicar cada trecho dele para você.

Neste exemplo de comando acima, estamos fazendo uma transferência entre dois servidores de VPS.

[other options] são modificadores que você pode adicionar ao comando SCP. Vamos mostrar os mais populares dele mais abaixo.
[source username@IP] é o nome do usuário e o IP da máquina que tem o arquivo que você quer. Seria algo como root@123.123.123.12.
:/ informa o comando SCP que você está prestes a digitar no diretório fonte.
[directory and file name] é onde o arquivo está localizado e o nome dele. Se parece com algo como /users/Edward/Desktop/SCP.png
[destination username@IP] é o nome do usuário e do IP da máquina de destino.
[destination directory] é o diretório onde o arquivo será salvo.
Em um cenário mais claro, a situação se pareceria com algo como:

scp -p root@162.168.1.1:/media/scp.png edward@162.168.1.2:/desktop/destination
Viu como é simples? Se você está copiando para ou de uma máquina local, você não precisa do endereço de IP, do destino ou do caminho da fonte como /desktop/nome_da_pasta.  

Vamos falar sobre outras opções que você pode usar para modificar o comando SCP. Existem 20 comuns deles que você pode usar tanto na forma de caractere único (-o) quanto no equivalente descritivo (-option).

As opções comuns mais usadas são:   

-P possibilita especificar uma entrada diferente para o servidor (a porta padrão para a porta TCP para o comando é a 22).
-c dá a possibilidade de especificar a encriptação do algoritmo que o cliente vai usar. Alguns dos valores que você pode usar são ‘aes256-ctr’, ‘aes256-cbc’, ‘blowfish-cbc’, ‘arcfour’, ‘arcfour128’, ‘arcfour256’, ‘cast128-cbc’, aes128-ctr’, ‘aes128-cbc’, ‘aes192-ctr’, ‘aes192-cbc’ e 3des-cbc’. A opção padrão na configuração do shell é ‘AnyStdCipher’
-q vai executar a operação em modo silencioso, o que significa que apenas os erros críticos é que serão mostrados.
-r é para cópia recursiva, que vai incluir todos os subdiretórios.
-4 or -6 pode ser usado se você quiser escolher a versão do protocolo empregada, sendo IPv4 ou IPv6. Você também pode configurar os requerimentos da configuração de IP mais exaustivamente com a palavra-chave da família de endereço.
–p vai preservar os tempos iniciais de modificação e atributos do arquivo. .
–u vai apagar a fonte do arquivo logo depois que a transferência for completada.
–c vai habilitar a compressão de dados enquanto a operação de transferência está sendo executada.
Detalhes para Ficar Atento
Como o SCP usa encriptação SSH, você vai precisar de uma senha SSH para a transferência do arquivo acontecer.

Além disso, é necessário que você tenha permissão de leitura na máquina da qual você está prestes a copiar e garantir privilégios para a máquina que vai receber o arquivo transferido.

Para a autenticação e configuração da conexão, você vai ter que gerar um par de chaves SSH no terminal usando o seguinte comando:

ssh-keygen -t rsa
Você copia essa chave para o sistema remoto usando:

ssh-copy-id user@remote_machine
Assim que tiver autenticado a chave na (s) máquina (s) remota (s), a chave pública será copiada e você estará pronto para começar as transferências.

Se você não se lembrar da (s) senha (s) raiz (es) de qualquer sistema, poderá fazer com que o cliente SSH selecione o arquivo a partir do qual a chave de identidade privada para a confirmação RSA é lida automaticamente.

Para a versão 2 do protocolo, o caminho de identidade padrão da chave do host é ~/.ssh/id_dsa, enquanto para a versão 1 do protocolo é ~/.ssh/id_rsa.

Então, você deve encontrar onde o backup das chaves públicas e privadas estão armazenadas, para que você possa usar o comando SSH para usá-las automaticamente.

Para o caminho /back-up/home/jack/.ssh, o comando a usar é este:

ssh -i /back-up/home/user/.ssh/id_dsa user@yourserver.servername.domain
DICA PRO: Essa opção tem o valor padrão –overwrite [yes]. Então, a menos que você especifique a opção –overwrite no ou –overwrite ask no seu comando SCP, a operação vai sobrescrever os arquivos que têm nomes e locais idênticos sem qualquer aviso.

Se você está transferir arquivos gigantes, recomendamos que use uma sessão tmux o execute o comando dentro de uma tela diferente.

Além disso, você também deve usar a opção -v para transferências maiores. Ela vai forçar o SCP a mostrar e depurar as conexões, as autenticações ou os problemas de configuração.    

Como Copiar Arquivos com um Comando SCP
A melhor parte do SCP é que ele dá a você a possibilidade de transferir arquivos entre dois hosts. Ou entre um host e uma máquina local. Vamos ver como o comando deve ser usado para cada tipo de transferência.

Arquivo Local para um Local Remoto
Vamos copiar um arquivo local scp.zip para o usuário de uma máquina remota chamada root. O nome do usuário é seguido pelo endereço de IP do servidor.

Exemplo:

scp /users/Edward/desktop/scp.zip root@191.162.0.2:/writing/article
Se você não tem uma confirmação automática do cliente SSH, você vai ser solicitado para inserir a senha da máquina local do usuário e versá uma métrica de progresso. Seria algo como isso:

root@191.162.0.2’s password:
novel3.zip   100% 0 0.0KB/s 00:00
Mas, vamos dizer que a máquina remota está configurada para responder às conexões SSH e uma porta que não seja a 22. Nesse caso, você deve especificar a porta usando uma opção.

scp -P 2322 /users/Edward/desktop/scp.zip root@191.162.0.2:/writing/article
Se você quiser mudar o nome do arquivo durante a operação da transferência, então o seu comando vai se parecer com isso (se a sua porta não for a padrão, apenas adicione -P e o número da porta):  

scp /users/Edward/desktop/scp.zip root@191.162.0.2:/writing/article/howtoscp.zip
Se você quer copiar um diretório que tem mais arquivos e/ou mais subdiretórios, use a linha de comando -r que mostramos mais cedo no artigo.

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