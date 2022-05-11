
<h1> Instalar Dig no Linux </h1>

Dig é uma parte do pacote utilitário DNS que é frequentemente instalado com nomes de servidores BIND.

Você também pode instalar o pacote de utilitários que contém o dig separadamente, acessando seu VPS através de SSH e usando os seguintes comandos na linha de comando:

Debian e Ubuntu:

    apt-get install dnsutils

CentOS 7:

    yum install bind-utils

Ao instalar, verifique a versão para garantir que a configuração foi concluída com sucesso:

    dig -v

<h3>Sintaxe Dig</h3>

De uma forma simples, a sintaxe do dig será como esta:

    dig [server] [name] [type]

* [server] – o endereço do IP ou hostname do servidor a ser consultado.

<p>Se o argumento do servidor for o hostname, então o dig resolverá o hostname antes de proceder com a consulta ao nome do servidor.
Isto é opcional e se você não fornecer um argumento de servidor, então o dig usará o nome do servidor listado em /etc/resolv.conf.</p>

* [name] – o nome do registro de recurso que deve ser pesquisado.

* [type] – o tipo de pesquisa solicitada pelo dig. Por exemplo, pode ser um registro A, registro MX, registro SOA ou qualquer outro tipo. Por padrão, o dig executa uma pesquisa por registro A se nenhum tipo de argumento for especificado.

<h3> Como usar o comando DIG </h3>

Vamos conhecer as utilidades básicas deste comando.

<h4> Dig no Nome de Domínio</h4>

Para executar uma pesquisa de DNS para um nome de domínio, apenas informe o nome com o comando dig:

    dig hostinger.com

Por padrão, o comando dig vai exibir o registro A quando não houver outras opções especificadas.

A saída também terá outras informações como a versão dig instalada, detalhes técnicos sobre respostas, estatísticas sobre a pesquisa, seção de perguntas e outras mais.

<h4> Respostas Curtas </h4>

O comando dig acima inclui muitas informações úteis em seções diferentes, mas em alguns momentos você só deseja o resultado da consulta.

Você pode fazer isso usando a opção +short, que vai exibir o endereço do IP (registro A) somente do nome do domínio:

    dig hostinger.com +short

<h4> Respostas Detalhadas</h4>

Talvez você queira ver a seção de respostas em detalhes. Portanto, para ter informações detalhadas sobre a seção de respostas, você pode parar de exibir toda a seção usando a opção +noall e consultar a seção de respostas usando apenas a opção +answer com o comando dig.

    dig hostinger.com +noall +answer

<h4> Especificando Nameservers </h4>

Por padrão, os comandos dig irão consultar os nomes de servidores listados em /etc/resolv.conf para pesquisar DNS para você. Você pode alterar esse comportamento padrão usando o símbolo @ seguido de um nome de host ou endereço IP do nome do servidor.

O seguinte comando dig envia a consulta DNS para o nome do servidor do Google (8.8.8.8) usando a opção @8.8.8.8.

    dig @8.8.8.8 hostinger.com

<h4> Consultar Todos os Tipos de Registro DNS </h4>

Para consultar todos os tipos de registro DNS disponíveis associados a um domínio, use a opção ANY. A opção ANY vai incluir todos os tipos de registro disponíveis na saída:

    dig hostinger.com ANY

<h4> Pesquisar por Tipos de Registro </h4>

Se você quer pesquisar um registro específico, apenas adicione o tipo ao final do comando.

Por exemplo, para consultar apenas a seção de resposta de troca de mensagens – MX – associada a um domínio, você pode usar o seguinte comando dig:

Por exemplo, para consulta obter apenas a troca de mensagens MX – seção de resposta associada a um domínio, você pode usar o seguinte comando dig.

    dig hostinger.in MX

De forma similar, para visualizar os outros registros associados com o domínio, especifique os outros tipos de registro no final do comando dig:

    dig hostinger.com txt (Query TXT record)

    dig hostinger.com cname (Query CNAME record)

    dig hostinger.com ns (Query NS record)

    dig hostinger.com A (Query A record)

<h4> Rastrear Caminho DNS </h4>

Dig permite rastrear o caminho de pesquisa de DNS usando a opção +trace. A opção faz consultas repetidas para resolver a pesquisa por nomes.

Ele consultará os servidores de nomes a partir da raiz e, em seguida, percorrerá a namespaces tree usando consultas iterativas de referências ao longo do caminho:

    dig hostinger.com +trace

<h4> Reverter DNS Lookup </h4>

A pesquisa reversa de DNS permite pesquisar o domínio e o nome do host associados a um endereço de IP.

Para executar uma pesquisa reversa de DNS usando o comando dig, use a opção –x seguida do endereço de IP escolhido.

No exemplo a seguir, a o dig realizará uma pesquisa de DNS inversa para o endereço IP associado ao google.com:

    dig +answer -x 172.217.166.46

Lembre-se de que se um registro PTR não estiver definido para um endereço IP, não será possível fazer uma pesquisa reversa de DNS, pois o registro PTR aponta para o domínio ou nome do host.

Consultas por Lotes
Com o utilitário dig, você pode realizar uma pesquisa de DNS para uma lista de domínios em vez de fazer o mesmo para cada um individualmente.

Para fazer isso, você precisa fornecer uma lista de nomes de domínio – um por linha em um arquivo. Quando o arquivo estiver pronto, especifique o nome dele com a opção -f:

vi domain_name.txt

hostinger.com

google.com

ubuntu.com
dig -f domain_name.txt +short
Controlar Comportamento Dig
A saída do comando pode ser personalizada permanentemente configurando opções no arquivo ~/.digrc que serão executadas automaticamente com o comando.

Suponha que você queira visualizar apenas a seção de respostas – especifique as opções necessárias no arquivo ~/.digrc, para que você não precise digitá-las durante a execução da consulta.

echo "+noall +answer" > ~/.digrc
Agora, faça uma pesquisa no servidor DNS para um domínio. A saída confirma que o dig é executada com as opções definidas no arquivo ~/.digrc.