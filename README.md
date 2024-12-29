pip install django
django-admin startproject loja_ebook
cd loja_ebook
python manage.py startapp produtos
Registro da Aplicação no Django
Abrir settings.py:
1.
No VS Code, use o explorador de arquivos para localizar o arquivo settings.py no diretório raiz do projeto.
Esse arquivo contém todas as configurações globais do projeto, incluindo as aplicações instaladas.
Adicionar a Aplicação:2.
No arquivo settings.py, encontre a lista INSTALLED_APPS.
Adicione a aplicação "produtos" à lista para que o Django a reconheça:
INSTALLED_APPS = [
# outras aplicações
"produtos",
]
Verificação da Aplicação no Django
Migração:1.
Para garantir que a aplicação esteja integrada ao projeto, execute o comando de migração no terminal:python
manage.py migrate
Esse comando aplica as alterações dos modelos ao banco de dados, criando as tabelas e os relacionamentos
necessários.
Iniciar Servidor:2.
Verifique se o servidor de desenvolvimento reconhece a nova aplicação sem erros:python manage.py runserver
O servidor exibe mensagens de log indicando o status da execução. Se tudo estiver correto, a aplicação estará
disponível para testes no ambiente lo
