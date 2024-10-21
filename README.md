## Descrição do Código Terraform

Este código utiliza o Terraform para provisionar recursos na AWS (Amazon Web Services) de forma programática. Ele cria uma infraestrutura básica que inclui uma VPC, uma sub-rede, um gateway de internet, uma tabela de rotas, um grupo de segurança e uma instância EC2 com a imagem Debian 12.

O provedor AWS é configurado para a região **us-east-1**. Duas variáveis são definidas: `projeto`, que representa o nome do projeto e tem como valor padrão `VExpenses`, e `candidato`, que representa o nome do candidato e tem como valor padrão `SeuNome`. Uma chave privada TLS é gerada com um algoritmo RSA e 2048 bits, que será utilizada para criar um par de chaves EC2. O par de chaves EC2 é criado com um nome que combina o nome do projeto e o nome do candidato, utilizando a chave pública gerada.

Uma VPC é criada com um bloco CIDR de `10.0.0.0/16`, com suporte a DNS e nomes de host habilitados, e é etiquetada com um nome que combina o projeto e o candidato. Em seguida, uma sub-rede é criada dentro dessa VPC com um bloco CIDR de `10.0.1.0/24` na zona de disponibilidade `us-east-1a`, também etiquetada de forma semelhante. Um gateway de internet é provisionado e associado à VPC, permitindo a comunicação com a internet, e uma tabela de rotas é criada para gerenciar o tráfego de rede, permitindo que o tráfego de qualquer lugar (`0.0.0.0/0`) seja roteado através do gateway de internet.

Uma associação de tabela de rotas é criada para a sub-rede, garantindo que o tráfego da sub-rede use a tabela de rotas especificada. Um grupo de segurança é criado para permitir acesso SSH (porta 22) de qualquer lugar, enquanto todas as regras de saída são permitidas. Isso garante que a instância EC2 possa ser acessada via SSH e possa se comunicar livremente com a internet.

A imagem da instância EC2 é obtida utilizando um filtro para a versão mais recente do Debian 12. Uma instância EC2 é então criada utilizando a imagem Debian 12, com tipo de instância `t2.micro`, associada à sub-rede criada, e utilizando o par de chaves gerado anteriormente. A instância é configurada para ter um endereço IP público e um volume de armazenamento de 20 GB que será excluído ao encerrar a instância. O script de inicialização da instância é configurado para atualizar e fazer upgrade dos pacotes do sistema.

Por fim, duas saídas são definidas: uma que exibe a chave privada gerada para acesso à instância EC2 (marcada como sensível) e outra que exibe o endereço IP público da instância EC2, permitindo que o usuário acesse esses valores após a criação da infraestrutura.
