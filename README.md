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
  
  ![vpc _pt1](https://github.com/user-attachments/assets/839d1a43-4d85-45bc-aee3-5a26612799f7)
  #### Após essas configurações clique em "Criar VPC"`

#### 1.2.Selecione a VPC -> clique em Mapa de Recursos -> clique exatamente naquele canto da subnet publica.

![vpc_pt2](https://github.com/user-attachments/assets/c89b4ff5-00aa-479e-8bf8-0183d453cdf6)

#### Na Próxima tela que abrir, no canto superior direito clique em "Ações" -> "Editar Configuração de sub-rede". E marque a seguinte opção:
![vpc_pt3](https://github.com/user-attachments/assets/6319307e-0374-4d24-9fad-f9869635df4c)

## Passo 2: Security Groups.
#### 2.1.Na console da AWS pesquise "EC2", quando abrir vá até a barra lateral e clique em "Security Groups".
#### 2.2.Clique em "Criar Security Group" no canto superior direito e crie um SG sem regras (por enquanto) para ser o web server.
#### 2.3.Crie um SG para o EFS (Elastic File System) com as seguintes regras:
![efs_pt'](https://github.com/user-attachments/assets/cc5f6760-20e3-4604-9fd1-d6f177872c5c)
![efs_pt2](https://github.com/user-attachments/assets/4161b5b5-8699-4141-86f3-e816118c440e)
#### 2.4.Crie um SG para o RDS (banco de dados) com as seguintes regras:
![rds_pt1](https://github.com/user-attachments/assets/f08c489b-7b86-4e3e-ac50-f3e2b413385d)
![rds_pt2](https://github.com/user-attachments/assets/523ba6f9-b144-42c1-849f-5a6243b8bb0b)
#### 2.5.Crie um SG para o Classic Load Balance com as regras: 
![clb_pt1](https://github.com/user-attachments/assets/9648a2d1-33db-450d-b635-7da39f1dc4fb)
![clb_pt2](https://github.com/user-attachments/assets/ad04ee99-1051-4fd9-94b4-c24ee60edff3)
#### 2.6.Selecione o grupo do web server, clique em "ações" no canto superior direito e edite as regras de entrada e de saida:
![ws_pt1](https://github.com/user-attachments/assets/ab5f19bd-1900-4288-961d-4c16955b5998)
![ws_pt2](https://github.com/user-attachments/assets/f797dc20-5c62-4e3d-8d51-8189bfdfe03c)

## Passo 3: Criar o RDS.
#### 3.1. Na barra de pesquisa do console da AWS pesquise "RDS" e clique na opção "Aurora and RDS".
#### 3.2. Clique em "Criar banco de dados" e siga as seguintes configurações:
