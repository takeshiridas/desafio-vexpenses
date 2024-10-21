# Instruções para Inicializar e Aplicar a Configuração Terraform

Este documento fornece um guia detalhado sobre como inicializar e aplicar uma configuração do Terraform para provisionar recursos na AWS.

## Pré-requisitos

1. **Conta na AWS**:
   - Você precisará de uma conta ativa na AWS. Certifique-se de que você tenha as credenciais de acesso (Access Key e Secret Key) configuradas.

2. **Instalação do Terraform**:
   - Baixe e instale o Terraform a partir do [site oficial do Terraform](https://www.terraform.io/downloads.html).
   - Verifique a instalação executando o seguinte comando no terminal:
     ```bash
     terraform -version
     ```

3. **Configuração das Credenciais da AWS**:
   - Você pode configurar suas credenciais da AWS usando o AWS CLI ou criando um arquivo `~/.aws/credentials`.
   - Para configurar via AWS CLI, execute:
     ```bash
     aws configure
     ```
   - Insira sua **Access Key**, **Secret Key**, região padrão (por exemplo, `us-east-1`), e formato de saída (opcional).

4. **Editor de Texto**:
   - Utilize um editor de texto de sua escolha para editar arquivos Terraform (`.tf`), como Visual Studio Code, Atom ou qualquer outro.

## Passos para Inicializar e Aplicar a Configuração Terraform

1. **Criar um Diretório para o Projeto**:
   - No terminal, crie um diretório para o seu projeto Terraform e navegue até ele:
     ```bash
     mkdir meu-projeto-terraform
     cd meu-projeto-terraform
     ```

2. **Criar o Arquivo de Configuração Terraform**:
   - No diretório criado, crie um arquivo chamado `main.tf` e cole o código Terraform modificado.

3. **Inicializar o Terraform**:
   - No terminal, execute o seguinte comando para inicializar o Terraform. Isso irá baixar os plugins necessários para a AWS e preparar o ambiente:
     ```bash
     terraform init
     ```

4. **Verificar a Configuração**:
   - Antes de aplicar, você pode verificar a configuração para garantir que não há erros:
     ```bash
     terraform validate
     ```

5. **Visualizar o Plano de Execução**:
   - Gere um plano de execução para ver quais recursos serão criados:
     ```bash
     terraform plan
     ```

6. **Aplicar a Configuração**:
   - Para aplicar a configuração e criar os recursos na AWS, execute:
     ```bash
     terraform apply
     ```
   - O Terraform mostrará o plano de execução novamente e pedirá sua confirmação. Digite `yes` para prosseguir.

7. **Acessar a Instância EC2**:
   - Após a aplicação bem-sucedida, você verá a saída com o endereço IP público da instância EC2 e a chave privada. Use a chave privada gerada para se conectar à instância:
     ```bash
     ssh -i "caminho/para/sua/chave.pem" ubuntu@<ec2_public_ip>
     ```
   - Substitua `caminho/para/sua/chave.pem` pelo caminho da chave privada e `<ec2_public_ip>` pelo endereço IP público que foi exibido na saída.

## Limpar Recursos (Opcional)

- Quando você não precisar mais dos recursos criados, você pode removê-los utilizando o seguinte comando:
  ```bash
  terraform destroy
