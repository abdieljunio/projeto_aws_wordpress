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






