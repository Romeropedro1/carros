Sistema de Cadastro de Carros
Descrição
Este é um sistema de cadastro de carros, desenvolvido em PHP com integração a um banco de dados MySQL. O sistema permite o cadastro, a edição e a exclusão de marcas e modelos de carros. Ele possui uma interface simples para o gerenciamento das marcas e modelos, sendo ideal para um sistema de estoque de veículos.

Funcionalidades
Cadastro de Marcas: Permite adicionar uma nova marca de carro.
Edição de Marcas : Permite editar o nome de uma marca existente.
Exclusão de Marcas: Permite excluir uma marca de carro.
Listagem de Marcas: Exibe todas as marcas cadastradas no banco de dados.
Cadastro de Modelos: Permite adicionar um modelo de carro associado a uma marca.
Edição de Modelos : Permite editar os detalhes de um modelo de carro, incluindo marca, nome, cor, ano e placa.
Exclusão de Modelos: Permite excluir um modelo de carro.
Tecnologias Utilizadas
PHP: A linguagem de programação usada para desenvolver a lógica do sistema.
MySQL: O banco de dados utilizado para armazenar informações sobre marcas e modelos de carros.
HTML: Para a estruturação dos formulários e interfaces.
Bootstrap: Para estilização e layout da interface (opcional).
Estrutura do Sistema
O sistema é composto por várias páginas e operações para o gerenciamento das marcas e modelos de carros.

Páginas principais
Cadastrar Marca: Página para cadastrar uma nova marca de carro.

URL :?page=marca-cadastrar
Formulário com um campo de entrada para o nome da marca.
HTML->

Copiar código
<form action="?page=marca-salvar" method="POST">
    <input type="hidden" name="acao" value="cadastrar">
    <label>Nome da Marca</label>
    <input type="text" name="nome_marca" class="form-control">
    <button type="submit" class="btn btn-success">Enviar</button>
</form>
Listar Marcas: Página que exibe todas as marcas cadastradas.

URL :?page=marca-listar
Exibe uma tabela com as marcas, com opções para editar ou excluir cada uma.
php

Copiar código
$sql = "SELECT * FROM marca";
$res = $conn->query($sql);
$qtd = $res->num_rows;

if($qtd > 0){
    echo "<table class='table'>";
    echo "<tr><th>#</th><th>Nome da Marca</th><th>Ações</th></tr>";
    while($row = $res->fetch_object()){
        echo "<tr>";
        echo "<td>".$row->id_marca."</td>";
        echo "<td>".$row->nome_marca."</td>";
        echo "<td>
                <button onclick=\"location.href='?page=marca-editar&id_marca=".$row->id_marca."';\" class='btn btn-primary'>Editar</button>
                <button onclick=\"if(confirm('Tem certeza que deseja excluir?')){location.href='?page=marca-salvar&acao=excluir&id_marca=".$row->id_marca."';}else{false;}\"  class='btn btn-danger'>Excluir</button>
              </td>";
        echo "</tr>";
    }
    echo "</table>";
} else {
    echo "Não encontrou resultados.";
}
Editar Marca: Página para editar o nome de uma marca existente.

URL :?page=marca-editar&id_marca={id}
Formulário com o nome da marca pré-preenchido para edição.
php

Copiar código
<form action="?page=marca-salvar" method="POST">
    <input type="hidden" name="acao" value="editar">
    <input type="hidden" name="id_marca" value="<?php echo $row->id_marca; ?>">
    <label>Nome da Marca</label>
    <input type=
    <label>Nome da Marca</label>
  
"text" name="nome_marca" value="<?php echo $row->nome_marca; ?>" class="form-control">
    <button type="submit" class="btn btn-success">Enviar</button>
</form>
Cadastrar Modelo: Página para cadastrar um modelo de carro.

URL :?page=modelo-cadastrar
Formulário para preencher os dados do modelo, incluindo a marca, nome, cor, ano e placa.
php

Copiar código
<form action="?page=modelo-salvar" method="POST">
    <input type="hidden" name="acao" value="cadastrar">
    <label>Marca</label>
    <select name="marca_id_marca" class="form-control">
        <!-- Opções de marcas -->
    </select>
    <label>Modelo</label>
    <input type="text" name="nome_modelo" class="form-control">
    <label>Cor</label>
    <input type="text" name="cor_modelo" class="form-control">
    <label>Ano</label>
    <input type="text" name="ano_modelo" class="form-control">
    <label>Placa</label>
    <input type="text" name="placa_modelo" class="form-control">
    <button type="submit" class="btn btn-success">Enviar</button>
</form>
Editar Modelo: Página para editar os detalhes de um modelo de carro existente.

URL :?page=modelo-editar&id_modelo={id}
Formulário pré-preenchido com os dados do modelo.
php

Copiar código
<form action="?page=modelo-salvar" method="POST">
    <input type="hidden" name="acao" value="editar">
    <input type="hidden" name="id_modelo" value="<?php echo $row_1->id_modelo; ?>">
    <label>Marca</label>
    <select name="marca_id_marca" class="form-control">
        <!-- Opções de marcas -->
    </select>
    <label>Modelo</label>
    <input type="text" name="nome_modelo" value="<?php echo $row_1->nome_modelo; ?>" class="form-control">
    <label>Cor</label>
    <input type="text" name="cor_modelo" value="<?php echo $row_1->cor_modelo; ?>" class="form-control">
    <label>Ano</label>
    <input type="text" name="ano_modelo" value="<?php echo $row_1->ano_modelo; ?>" class="form-control">
    <label>Placa</label>
    <input type="text" name="placa_modelo" value="<?php echo $row_1->placa_modelo; ?>" class="form-control">
    <button type="submit" class="btn btn-success">Enviar</button>
</form>
Operações
Cadastrar: A operação de cadastro insere os dados no banco de dados.
Editar: A operação de edição atualiza os dados no banco de dados.
Excluir: A operação de exclusão remove o item do banco de dados.
Exemplo de SQL para criação das tabelas
Para que o sistema funcione corretamente, você precisa criar duas tabelas no banco de dados MySQL:

SQL->

Copiar código
CREATE TABLE marca (
    id_marca INT AUTO_INCREMENT PRIMARY KEY,
    nome_marca VARCHAR(255) NOT NULL
);

CREATE TABLE modelo (
    id_modelo INT AUTO_INCREMENT PRIMARY KEY,
    marca_id_marca 
    marca_id_marca
INT,
    nome_modelo VARCHAR(255) NOT NULL,
    cor_modelo VARCHAR(50),
    ano_modelo INT,
    placa_modelo VARCHAR(20),
    FOREIGN KEY (marca_id_marca) REFERENCES marca(id_marca)
);
Como Executar o Projeto
Pré-requisitos
Servidor Local: Para rodar este projeto, você precisa de um servidor com PHP e MySQL, como o XAMPP ou WAMP.

Banco de Dados: Certifique-se de que o banco de dados esteja configurado e as tabelas sejam criadas conforme o exemplo SQL acima.

Passos
Clone o Repositório: Clone este repositório para o seu servidor local.

bater

Copiar código
git clone https://github.com/seu-usuario/cadastro-carros.git
Configuração do Banco de Dados: No seu servidor MySQL, crie o banco de dados e as tabelas, como mostrado acima.

Configuração do Banco de Dados no PHP: No código PHP, configure a conexão com o banco de dados no arquivo config.php.

Acesse o Sistema: Abra o navegador e acesse http://localhost/seu-projeto/.

Contribuir
Se você deseja contribuir para o projeto, sinta-se à vontade para abrir um pull request




