Atividade_MYR - Sistema de Cadastro e edição de livros Este projeto consiste em um sistema simples de cadastro e login de usuários, desenvolvido com as seguintes tecnologias:

HTML: Interface do usuário.

PHP: Backend para processar cadastro e login.

MySQL: Banco de dados para armazenar os usuários.

Estrutura do Projeto / ├── cadastro.html # Tela de cadastro de novos usuários ├── processacad.php # Script PHP que processa o cadastro e a lógica de autenticação ├── exemplo-login.php # Página de exemplo para login (autônomo) ├── cadastro.php # Lida com a lógica de registro do usuário, higieniza a entrada, valida o e-mail, faz o hash da senha e armazena os dados do usuário. ├── index.html # Página inicial com links para login e cadastro ├── login.html # Formulário de login de usuários ├── login.php # Lida com a lógica de login, verifica as credenciais do usuário e inicia uma sessão.

Como Executar Para executar este sistema, você precisará de um servidor web com PHP e MySQL instalados (por exemplo, XAMPP, WAMP ou pilha LAMP).

Configurar o Banco de Dados:

Crie um banco de dados chamado sistema_login em seu servidor MySQL.

Crie uma tabela chamada usuarios dentro do banco de dados sistema_login com a seguinte estrutura:

CREATE TABLE usuarios ( id INT AUTO_INCREMENT PRIMARY KEY, nome VARCHAR(255) NOT NULL, email VARCHAR(255) NOT NULL UNIQUE, senha VARCHAR(255) NOT NULL );

Colocar os Arquivos:

Coloque todos os arquivos HTML e PHP fornecidos na raiz do documento do seu servidor web (por exemplo, htdocs para Apache).

Configurar a Conexão com o Banco de Dados:

Abra cadastro.php e login.php.

Certifique-se de que a instanciação da classe Auth (em login.php) e processacad (em cadastro.php) tenha as credenciais corretas do banco de dados: $auth = new processacad("localhost", "root", "&tec77@info!", "sistema_login"); (Assumindo localhost como host, root como usuário, &tec77@info! como senha e sistema_login como nome do banco de dados). Ajuste esses valores se a configuração do seu banco de dados for diferente.

Acessar no Navegador:

Abra seu navegador e navegue até http://localhost/index.html (ou a URL apropriada se você configurou um host virtual).

Funcionalidade index.html: Fornece um ponto de partida para os usuários, permitindo que eles escolham entre fazer login ou se registrar.

cadastro.html: Apresenta um formulário para novos usuários registrarem uma conta. Ele coleta nome completo, e-mail e senha. A senha exige um comprimento mínimo de 6 caracteres.

cadastro.php:

Recebe dados do formulário de cadastro.html.

Usa a classe processacad para higienizar as entradas.

Valida o formato do e-mail.

Verifica se a senha tem pelo menos 6 caracteres.

Tenta registrar o usuário fazendo o hash da senha e inserindo os dados na tabela usuarios.

Impede o registro se o e-mail já existir.

Fornece feedback sobre o registro bem-sucedido ou erros.

login.html: Exibe um formulário para usuários existentes inserirem seu e-mail e senha para fazer login.

login.php:

Recebe dados do formulário de login.html.

Usa a classe Auth (que é processacad renomeada para o contexto de login) para higienizar as entradas.

Valida o formato do e-mail.

Tenta fazer login do usuário verificando o e-mail e a senha fornecidos em relação à senha hash armazenada na tabela usuarios.

Inicia uma sessão PHP após o login bem-sucedido.

Fornece feedback sobre login bem-sucedido ou credenciais incorretas.

processacad.php:

Estabelece uma conexão com o banco de dados usando MySQLi.

sanitizar($dado): Limpa os dados de entrada para evitar ataques de injeção (por exemplo, SQL Injection, XSS).

validarEmail($email): Verifica se um endereço de e-mail está em um formato válido.

login($email, $senha): Verifica as credenciais do usuário consultando o banco de dados para o e-mail e usando password_verify para verificar a senha em relação ao hash armazenado.

emailExiste($email): Verifica se um determinado endereço de e-mail já existe na tabela usuarios.

cadastrar($nome, $email, $senha): Insere novos dados de usuário na tabela usuarios após fazer o hash da senha.

exemplo-login.php: Um exemplo autônomo que demonstra como validar as credenciais de login em um banco de dados de usuários simulado, incluindo hash e verificação de senha. Também mostra uma função sanitizarEntrada.

Considerações de Segurança Hash de Senha: As senhas são hashadas usando password_hash() com PASSWORD_DEFAULT antes de serem armazenadas no banco de dados, o que é crucial para a segurança.

Higienização de Entrada: As entradas do usuário são higienizadas usando htmlspecialchars, strip_tags e trim para mitigar vulnerabilidades comuns da web, como XSS e injeção de SQL.

Prepared Statements: A classe processacad usa prepared statements (mysqli::prepare) para operações de banco de dados, o que ajuda a prevenir ataques de injeção de SQL.

Gerenciamento de Sessão: Uma sessão básica é iniciada após o login bem-sucedido, mas práticas adicionais de gerenciamento de sessão (por exemplo, tempos limite de sessão, cookies seguros) seriam benéficas para um ambiente de produção.

Melhorias (Potencial Trabalho Futuro) Tratamento de Erros: Implementar um tratamento de erros mais robusto e mensagens de erro amigáveis ao usuário.

Feedback do Usuário: Fornecer feedback mais específico aos usuários (por exemplo, "E-mail já cadastrado" no formulário de registro).

Redefinição de Senha: Adicionar funcionalidade para que os usuários redefinam senhas esquecidas.

Painel do Usuário: Criar uma "painel.php" ou página de dashboard para usuários logados.

Estilização e Responsividade: Melhorar a UI/UX com CSS mais avançado e tornar os formulários responsivos.

Validação do Lado do Cliente: Adicionar JavaScript para validação em tempo real do lado do cliente para melhorar a experiência do usuário.

Arquivo de Configuração: Armazenar as credenciais do banco de dados em um arquivo de configuração separado, em vez de diretamente nos scripts PHP.
