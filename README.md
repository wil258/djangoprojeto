Linux Ubuntu 

Este conjunto de comandos é usado para configurar e iniciar um projeto Django em um ambiente de desenvolvimento no Linux, usando Python 3. Vou explicar cada parte do código de forma detalhada:

sudo apt update

Atualiza a lista de pacotes disponíveis nos repositórios configurados do sistema.
A opção sudo é usada para executar o comando com privilégios de administrador.
Isso garante que você tenha as versões mais recentes dos pacotes.
sudo apt install python3 python3-venv python3-pip

Instala os pacotes necessários para trabalhar com Python 3 e Django:
python3: Instala o Python 3.
python3-venv: Instala o módulo que permite criar ambientes virtuais em Python.
python3-pip: Instala o pip, o gerenciador de pacotes Python.
python3 --version

Exibe a versão do Python 3 instalada no sistema.
python3 -m venv venv

Cria um ambiente virtual chamado venv.
O ambiente virtual é isolado, permitindo que você instale pacotes sem afetar o sistema global.
source venv/bin/activate

Ativa o ambiente virtual que foi criado. Após a ativação, todos os pacotes Python serão instalados e utilizados dentro desse ambiente, sem afetar o sistema global.
pip install django

Instala o Django, um framework para desenvolvimento de aplicações web em Python.
django-admin startproject nome_do_projeto

Cria um novo projeto Django com o nome especificado (substitua nome_do_projeto pelo nome desejado).
O comando cria a estrutura de diretórios e arquivos iniciais para o projeto Django.
cd nome_do_projeto

Navega para o diretório do projeto que você acabou de criar, onde os arquivos do projeto Django estão localizados.
http://127.0.0.1:8000/

Este é o endereço local onde o servidor Django será acessível. A URL 127.0.0.1 é o IP de loopback (localhost), e a porta 8000 é a porta padrão para servidores Django.
python manage.py runserver

Inicia o servidor de desenvolvimento do Django. O projeto pode ser acessado em http://127.0.0.1:8000/.
python manage.py startapp produtos

Cria um novo aplicativo Django chamado produtos.
Aplicativos são componentes modulares dentro de um projeto Django, onde você pode definir modelos, visualizações, URLs, etc.
INSTALLED_APPS = [ ... 'produtos' ]

No arquivo settings.py do seu projeto Django, você deve adicionar o aplicativo produtos à lista INSTALLED_APPS. Isso faz o Django reconhecer e incluir o aplicativo no seu projeto.
python manage.py migrate

Aplica todas as migrações do banco de dados. O Django usa migrações para manter o banco de dados sincronizado com o modelo de dados da aplicação.
python manage.py makemigrations

Cria novas migrações com base nas alterações feitas nos modelos (exemplo: criação ou alteração de tabelas no banco de dados).
Este comando gera arquivos de migração que podem ser aplicados posteriormente com migrate.
sudo apt install sqlite3

Instala o SQLite, um banco de dados leve e embutido, que é o banco de dados padrão usado no Django para o desenvolvimento local.
O comando sudo garante que você tenha permissão de administrador para instalar o pacote.
Com isso, você terá um projeto Django básico rodando, com um aplicativo produtos e o banco de dados SQLite configurado. Para desenvolver, basta seguir criando e migrando seus modelos, views e URLs!

Passo 1: Criando um Modelo
Os modelos são definidos em arquivos Python dentro de cada aplicativo Django, geralmente em um arquivo chamado models.py. Abaixo, vou mostrar um exemplo de como criar um modelo para um aplicativo de "produtos", como mencionado no seu comando anterior.

Exemplo de modelo Produto:
No arquivo produtos/models.py:

from django.db import models

class Produto(models.Model):
    nome = models.CharField(max_length=100)  # Nome do produto (string com limite de 100 caracteres)
    descricao = models.TextField()  # Descrição do produto (texto longo)
    preco = models.DecimalField(max_digits=10, decimal_places=2)  # Preço do produto (número com 2 casas decimais)
    estoque = models.PositiveIntegerField()  # Quantidade em estoque (somente números positivos)
    data_criacao = models.DateTimeField(auto_now_add=True)  # Data de criação do produto (automática)

    def __str__(self):
        return self.nome  # Retorna o nome do produto quando o modelo for convertido para string

Passo 2: Realizando Migrações
Após criar ou modificar os modelos, é necessário criar as migrações, que são arquivos que informam ao Django como o banco de dados deve ser alterado para refletir as mudanças nos modelos.

1. Criar migrações:
No terminal, execute o seguinte comando

python manage.py migrate
O comando migrate aplica todas as migrações pendentes ao banco de dados, criando as tabelas e os campos necessários para os modelos.

Passo 3: Interação com o Banco de Dados
Agora que o modelo foi criado e a migração foi aplicada, você pode interagir com o banco de dados usando o Django ORM. O Django fornece uma API de alto nível para consultar e manipular os dados.

Exemplos de Interação com o Banco de Dados:
1. Criar um novo produto:
Você pode criar instâncias de modelos e salvá-las no banco de dados:
from produtos.models import Produto

from produtos.models import Produto

# Criando um novo produto
novo_produto = Produto(
    nome="Camiseta Python",
    descricao="Uma camiseta confortável com estampa de Python.",
    preco=39.90,
    estoque=50
)
novo_produto.save()  # Salva o produto no banco de dados
2. Consultar produtos:
Você pode consultar os produtos do banco de dados usando o ORM:
# Buscar todos os produtos
produtos = Produto.objects.all()

# Buscar um produto específico
produto = Produto.objects.get(id=1)

# Buscar produtos com preço maior que 30
produtos_caros = Produto.objects.filter(preco__gt=30)
 Atualizar um produto:
Para atualizar um produto, basta pegar o objeto e alterar os campos desejados:
produto = Produto.objects.get(id=1)
produto.preco = 29.90  # Atualiza o preço
produto.save()  # Salva as alterações no banco de dados
4. Deletar um produto:
Você pode excluir um produto usando o método delete():
produto = Produto.objects.get(id=1)
produto.delete()  # Deleta o produto do banco de dados
Passo 4: Acessando e Visualizando os Dados na Interface Administrativa do Django
O Django vem com uma interface administrativa pronta para ser utilizada. Para acessar a interface administrativa, siga os passos abaixo:

1. Registrar o modelo no admin:
No arquivo produtos/admin.py, registre o modelo Produto para que ele apareça na interface administrativa do Django:
from django.contrib import admin
from .models import Produto

admin.site.register(Produto)  # Registra o modelo Produto
2. Criar um superusuário:
Se ainda não tiver um superusuário (um administrador), crie um para acessar o painel administrativo:
python manage.py createsuperuser
Siga as instruções para definir um nome de usuário, e-mail e senha.

3. Acessar o admin:
Agora, inicie o servidor Django:

python manage.py runserver

Acesse o painel administrativo através do navegador em http://127.0.0.1:8000/admin/, faça login com o superusuário criado, e você poderá gerenciar os produtos diretamente pela interface web.

Passo 5: Conclusão
Agora você tem um modelo Produto integrado com o banco de dados, pode criar, ler, atualizar e excluir dados facilmente, e também tem a interface administrativa do Django para gerenciar tudo de forma simples e rápida.

Observações Finais:

O Django ORM facilita muito a interação com o banco de dados, sem precisar escrever SQL manualmente.
Após a criação dos modelos, é importante sempre rodar makemigrations e migrate quando você fizer alterações nos modelos, para garantir que o banco de dados esteja sempre atualizado.
Embora o Django use o SQLite por padrão para desenvolvimento, você pode configurar outros bancos de dados como PostgreSQL, MySQL ou MariaDB no arquivo settings.py.

