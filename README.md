# AWS_Wordpress

## 📖 Descrição
Projeto feito durante o estágio na CompassUol com o intuido de instalar e configurar um container Docker_Wordpress em uma máquina virtual EC2, utilizando o banco de dados RDS e o EFS para armazenamento de arquivos estáticos, todos esses serviços disponíveis  na AWS.

## 🚀 Tecnologias Utilizadas
-    ![AWS](https://img.shields.io/badge/AWS-232F3E?logo=amazonaws&logoColor=white&style=for-the-badge)
-    ![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white&style=for-the-badge)
-    ![Linux](https://img.shields.io/badge/Linux-FCC624?logo=linux&logoColor=black&style=for-the-badge)
-    ![Git](https://img.shields.io/badge/Git-F05032?logo=git&logoColor=white&style=for-the-badge)
-    ![MySQL](https://img.shields.io/badge/MySQL-4479A1?logo=mysql&logoColor=white&style=for-the-badge)


  Agora vamos ao passo-a-passo para executar o projeto.

  ## Passo 1: Criar VPC.
  #### 1.1. Digite "VPC" na barra de pesquisa da aws e clique em: vpc -> suas vpc's -> criar vpc.
  ![vpc_pt1](https://github.com/user-attachments/assets/173b4e87-f3cf-4339-9e5a-188cbd80bd07)
  #### Certifique-se das seguintes configurações:
 ![vpc_pt](https://github.com/user-attachments/assets/87a8b959-98cb-4ccd-8ed9-8e0ddc4f1ebc)
![vpc_pt3](https://github.com/user-attachments/assets/f2c74ce2-0da3-49a1-9c40-306f88474789)

  
  #### Após essas configurações clique em "Criar VPC"`



## Passo 2: Security Groups.
#### 2.1.Na console da AWS pesquise "EC2", quando abrir vá até a barra lateral e clique em "Security Groups".
#### 2.2.Clique em "Criar Security Group" no canto superior direito e crie um SG sem regras (por enquanto) para ser o web server.
#### 2.3.Crie um SG para o EFS (Elastic File System) com as seguintes regras:
![efs_pt'](https://github.com/user-attachments/assets/cc5f6760-20e3-4604-9fd1-d6f177872c5c)
![efs_pt2](https://github.com/user-attachments/assets/dbcda4fd-ae4e-4ed3-9eef-c77ec4f79a83)

#### 2.4.Crie um SG para o RDS (banco de dados) com as seguintes regras:
![rds_pt1](https://github.com/user-attachments/assets/f08c489b-7b86-4e3e-ac50-f3e2b413385d)
![rds_pt2](https://github.com/user-attachments/assets/778e6c63-0bcc-4ba1-838e-de98b1adf5b0)

#### 2.5.Crie um SG para o Classic Load Balance com as regras: 
![clb_pt1](https://github.com/user-attachments/assets/d0b9dd2f-18ce-4c23-ba71-182f000e2270)
![clb_pt2](https://github.com/user-attachments/assets/2a455a7b-e271-4756-8630-37909a234446)

#### 2.6.Selecione o grupo do web server, clique em "ações" no canto superior direito e edite as regras de entrada e de saida:
![ws_pt1](https://github.com/user-attachments/assets/0106880f-e925-4434-8550-8c37b6fed910)
![ws_pt2](https://github.com/user-attachments/assets/723719d3-4d2e-4363-8872-191d05ed7832)


## Passo 3: Criar o RDS.
#### 3.1. Na barra de pesquisa do console da AWS pesquise "RDS" e clique na opção "Aurora and RDS".
#### 3.2. Clique em "Criar banco de dados" e siga as seguintes configurações:
![rds_pt1](https://github.com/user-attachments/assets/61c12fc6-fa14-43d3-8036-94abeda4d0e3)
![rds_pt2](https://github.com/user-attachments/assets/2997f5e3-7899-49d6-b8cc-05d30696abfe)
#### OBS:se necessário anote o usuario e a senha que você colocar pois precisará deles no docker-compose  daqui a pouco.
![rds_pt3](https://github.com/user-attachments/assets/ae5daad8-6d87-43fb-82a5-33c76eb4eec5)
![rds_pt4](https://github.com/user-attachments/assets/4873e3ab-5ee6-4d42-ac2e-7dacde1fb2e5)
![rds_pt5](https://github.com/user-attachments/assets/fbf4586f-c68d-4506-9963-47685d2e71ea)
![rds_pt6](https://github.com/user-attachments/assets/6ea56624-dc76-4cbb-a50c-0a2729513758)
#### OBS: Na ultima aba de "Configurações avançadas" guarde bem o nome que você der ao banco de dados pois ele será usado no docker0compose.
![rds_pt10](https://github.com/user-attachments/assets/885ccf19-1c43-46de-a5b9-a84ed3ce0cb1)
#### É só clicar em "criar banco de dados" e esperar a mensagem de confirmação ou o statud de "Disponível"
#### 3.2.Clique no nome do banco de dados e salve o endereço do endpoint para usar no docker-compose.
![rds_pt11](https://github.com/user-attachments/assets/b7ba56ab-2a67-4bb1-b759-a3472ef9da8e)

## Passo 4: Criar o EFS (Elastic File Sistem)
#### 4.1 Na barra de pesquisa do console da AWS digite "EFS", selecione e depois clique em "Criar sistema de arquivos" no canto superir direito, na seguinte tela coloque o nome do seu sistema de arquivos e depois clique em "Personalizar".
![efs_pt1](https://github.com/user-attachments/assets/9714faee-e622-4a20-b6af-6a5b6e7f6ecc)
#### 4.2. Siga as seguintes configurações:
![efs_pt2](https://github.com/user-attachments/assets/8d3c9962-3c43-4cf0-b5d9-06274b37f5ef)
#### OBS: Selecione subnets privadas e soloque o SG do EFS.
![efs_pt3](https://github.com/user-attachments/assets/d65e6d9a-4461-4954-b971-7c4fbb8338b8)
#### 4.3. É só clicar em "próximo" até aparecer o botão "criar"
#### 4.4. Salve o id sistema de arquivos para usar no user-data posteriormente.
![efs_pt4](https://github.com/user-attachments/assets/088d2011-de71-4074-bb02-e4002e7fd83c)

## Passo 5: Cirar o Modelo de Execução (Launch template).
#### 5.1. Dentro do menu da EC2 ao lado esquerdo clique em "modelo de execução" -> "Criar novo modelo", e copie as seguintes configurações:
![lt_pt1](https://github.com/user-attachments/assets/12431538-963c-440f-8941-263cabeeade0)
![lt_pt2](https://github.com/user-attachments/assets/1e0acfa0-3bf8-4a78-a9f6-9478c963692b)
#### vá até o final da página e clique em "detalhes avançados" desça até o final novamente e coloque o seguinte userdata no campo de text0:
![lt_pt3](https://github.com/user-attachments/assets/d76168aa-0dd3-41f1-94e2-5f66e7d8307a)
```bash
#!/bin/bash

# Atualiza pacotes do sistema
sudo yum update -y

# Instala pacotes necessários
sudo yum install -y git curl wget unzip amazon-efs-utils nfs-utils

# Instala Docker via amazon-linux-extras
sudo amazon-linux-extras enable docker
sudo yum install -y docker

# Adiciona o ec2-user ao grupo Docker
sudo usermod -aG docker ec2-user

# Habilita e inicia o serviço Docker
sudo systemctl enable docker
sudo systemctl start docker

# Baixa e instala Docker Compose manualmente
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# Verifica se o Docker Compose foi instalado corretamente
docker-compose --version
if [ $? -ne 0 ]; then
  echo "Erro: Docker Compose não foi instalado corretamente."
  exit 1
fi

# Criar diretório para montagem do EFS
sudo mkdir -p /mnt/efs-wordpress

# Adiciona a montagem do EFS no /etc/fstab para persistência
echo "<COLOQUE AQUI O FS ID DO SEU EFS>:/ /mnt/efs-wordpress efs _netdev,tls 0 0" | sudo tee -a /etc/fstab

# Monta o EFS
sudo mount -a

# Confirma se o EFS foi montado corretamente
df -h | grep efs

# Define a URL do repositório onde está o arquivo docker-compose.yml
GIT_REPO_URL="COLOQUE AQUI O LINK RAW DO SEU DOCKER COMPOSE QUE PARA MIM SÓ FUNCIONOU BAIXANDO ELE DO GITHUB"

# Criar diretório para armazenar o docker-compose.yml
mkdir -p /home/ec2-user/app
cd /home/ec2-user/app

# Baixa o arquivo docker-compose.yml do GitHub
curl -sS -o docker-compose.yml $GIT_REPO_URL

# Verifica se o arquivo foi baixado corretamente
if [ ! -s docker-compose.yml ]; then
  echo "Erro: Falha ao baixar o arquivo docker-compose.yml com curl. Tentando com wget..."
  wget -q $GIT_REPO_URL -O docker-compose.yml
fi

if [ -s docker-compose.yml ]; then
  echo "Arquivo docker-compose.yml baixado com sucesso."
else
  echo "Erro crítico: Não foi possível baixar o arquivo docker-compose.yml."
  exit 1
fi

# Aguarda o Docker inicializar
sleep 10

# Inicia o Docker Compose como root
sudo docker-compose up -d

```
#### Modelo de docker-compose.yml 
```yaml
version: '3.8'
services:
  web:
    image: wordpress
    restart: always
    ports:
      - "80:80"
    environment:
      WORDPRESS_DB_HOST: <COLOQUE AQUI O ENDPOINT DO RDS>
      WORDPRESS_DB_USER: <COLOQUE AQUI O NOME DE USUARIO DO RDS>
      WORDPRESS_DB_PASSWORD: <COLOQUE AQUI A SENHA DO RDS>
      WORDPRESS_DB_NAME: <COLOQUE AQUI O NOME QUE VOCÊ PÔS LA NO FINAL DA CRIAÇÃ DO RDS>
    volumes:
      - /mnt/efs/wp-content:/var/www/html/wp-content
    networks:
      - tunel
networks:
  tunel:
    driver: bridge
```
#### 5.2. É só criar em "criar modelo de execução"
## Passo 6: Criar Classic Load Balance.
#### 6.1. No menu da  EC2 ao lado esquerdo clique em "Load Balancers" -> "Criar Load Balancer"(botaão amarelo no canto superior esquerdo) e copie as seguintes configurações:
![clb_pt2](https://github.com/user-attachments/assets/6ddeb880-fafb-48f4-943a-8c269ecac819)

![clb_pt3](https://github.com/user-attachments/assets/65639f70-f699-436e-9045-6d0b39fe9acc)
![clb_pt4](https://github.com/user-attachments/assets/7fdf8198-ff84-4682-892a-95d490f8e072)
#### no final basta clicar em "criar load balancer"
## Passo 6: Criar Auto Scaling Group.
#### 6.1. No menu da EC2 ao lado esquerdo clique em "criar auto scaling group" no canto superior esquerdo e siga as configurações:
![asg_pt1](https://github.com/user-attachments/assets/dc3f4322-9bfe-434f-84da-d5977bd5cf10)
![asg_pt2](https://github.com/user-attachments/assets/56e39bea-0d6c-4a91-8bab-10a21d8b669a)
![asg_pt3](https://github.com/user-attachments/assets/90d8096b-f94c-4f6f-8b2b-f40b084eadf6)
![asg_pt4](https://github.com/user-attachments/assets/cad069d8-4568-4476-90fc-a899f83beac5)
![asg_pt5](https://github.com/user-attachments/assets/48b49334-18d0-4845-b83c-626a7afa2bfe)
![asg_pt6](https://github.com/user-attachments/assets/a13397cf-384a-4e13-956e-99cb5bba7f98)
#### 6.2. Após essa configurações você não meche em nada na ultima tela e clica em "criar auto scaling group" no final da pagina.

## Passo 7: Ver se o wordpress está rodando:
 #### 7.1. No menu da  EC2 ao lado esquerdo clique em "Load Balancers" e copie o dns do CLB:
 ![testendo](https://github.com/user-attachments/assets/a080a2cd-4696-4b8d-bdbe-40c2e3fbdc44)
#### Cole o dns no barra do link do navegador se estiver assim está correto:
![Screenshot from 2025-04-03 19-05-40](https://github.com/user-attachments/assets/142a58d5-9e38-490c-8ea7-f0d91148cb5a)

