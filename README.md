# Atividade MVC

## Arquitetura MVC
- **Nome do Projeto:** DIVE - Dell Interactive Virtual Environment
- **Descrição:** O projeto visa o desenvolvimento de uma solução web que hospede manuais de instrução que irão servir para o treinamennto dos colaboradores que trabalham na linha de mintagem de computadores.
- **Arquitetura:** M.V.C (Model-View-Controller) <img src="../assets/MVCponderada.png"><br>
- **Ferramenta de Diagramação:** draw.io

### Modelos (Models):
#### Manuais
- **Id:** Identificador do manual;
- **Título:** Título que o manual recebe;
- **Descrição:** Descrição do conteúdo contido no manual;
- **Conteúdo:** Conteúdo do manual com todos os passos de montagem e informações.

####Users
- **Id:** Identificador do usuário;
- **Nome:** Nome do usuário;
- **E-mail:** E-mail do usuário;
- **Senha:** Senha do usuário;
- **Função:** Função na empresa, nesse caso, funciomário ou administrador;

#### Relações
##### Usuário X Log de atividade:
- Os usuários conseguem se associar a nenhum ou a vários logs;
- Chave estrangeira referenciando a tabela "Usuário" na tabela "Log de Atividade"

##### Usuário X Manual
- Os usuários podem ter manuais relacionados a cada um deles em uma escala de zero a vários;
- Os manuais podem ser associados aos montadores em uma escala de zero a vários;
- Relação de equivalencia de escala de quantidade entre os usuários e os manuais.

### Controladores (Controllers):
#### Funcionários:
##### Responsabilidades:
- Autenticação;
- Gerenciar contas;
- Autorizar acesso.

###### Ações:
######Autenticação (nome de usuário, senha);
- **Entrada:** nome de usuário, senha;
- **Saída:** usuário ou null
- Interage com usuário e senha para autenticar e retorna autenticado ou null caso sejam inválidos.

###### Interação com modelos e views:
- Eles interagem realizando CRUD nos dados do usuário, então retornam os resultados para as views para só assim serem renderizadas para o usuário.

#### Manual:
##### Responsabilidades:
- Visualização;
- Gerenciamento de manuais;

#### Ações:
##### Visualização:
- **Entrada:** Id do manual selecionado para visualização;
- **Saída:** Manual;
- Interage com o manual, assim, com o id do manual fornecido, ele recupera as informações e retorna com o manual correspondente.

##### Gerenciamento de manuais:
- **Entrada**: palavra-chave de busca, id do manual e informações a serem atualizadas;
-  **Saída:** Manual ou resultados;
-  Interage com o manual para atualizar e buscar manuais com base em Id e palavra-chave, retornando, assim a lista de manuais ou o manual já atualizado.

###### Interação com modelos e views:
- Os métodos interagem com os modelos para recuperar informações dos manuais, buscá-los e atualizá-los, passando por fim os resultados para o usuário.

#### Administrador:
##### Responsabilidades:
- Gerenciamento de usuários;
- Gerenciamento de manuais.

#### Ações:
##### Gerenciamento de usuários:
-  **Entrada**: Não se aplica;
-  **Saída:** Os usuários;
-  Interage com usuário para listar todos que estão presentes no sistema, retornando uma lista dos funcionários.

##### Gerenciamento de manuais:
- **Entrada**: Não se aplica;
- **Saída:** Os manuais;
- Interage com os manuais exibindo toda a lista dos disponíveis.

###### Interação com modelos e views:
- Os métodos interagem com os modelos para gerar uma lista de usuários e manuais e ao fim são exibidos para os usuários.

### Views (Views):
- **Login:** Permite que os usuários acessem ao sistema;

- **Tela do Funcionário:** Fornece a visão do sistema de manuais e funcionalidades da página assim que realizam o login.

- **Tela do Administrador:** Fornece ao administrador uma página que o permite gerenciar usuários, adicionar novos manuais e visualizar relatórios, entre outros.


### Infraestrutura:
### Banco de Dados:

- **Escolha:** PostgreSQL. Por ser um banco de dados relacional ele se torna mais adequado para armazenar as informações necessárias sobre usuários, manuais e atividade.

- **Integração com MVC:** Os modelos Usuário e Manual interagem com o banco de dados através do MVC. Os controllers interagem com esses modelos e agem nas operações de escrita, exclusão de dados, atualização e leitura.

- **Impacto:** É consistente e promove a integridade dos dados, garantindo estruturação e segurança ao armazenar informações, o que facilita o acesso aos dados.

### Servidor Web:

- **Escolha:** Node.js, Express.js

- **Integração com MVC:** O Express.js trabalha para nos permitir organizar o código em Controllers, estes que lidam com as requisições realizadas, interagem com Models para acessar o banco de dados para assim retornar as respostas.

- **Impacto:**  O uso do Node.js com Express.js é o responsável pela escalabilidade e desempenho, gerando eficiência ao lidar requisições volumosas.

### Autenticação e Autorização:

- **Escolha:** SSO. Usado para lidar com a autenticação de usuários.

- **Integração com MVC:** Os controllers de usuário agem integrando-se com o serviço SSO e verificam a autenticação do usuário dando a ele as permissões e funcionalidades a depender das credenciais.

- **Impacto:** Uma autenticação e autorização robusta serve para proteger os dados sensíveis da aplicação, garantindo segurança, ou seja, apenas pessoal autorizado possui permissão de acesso.

## Implicações da Arquitetura:
### Escalabilidade:

- **Impacto:** A arquitetura MVC proporciona que haja escalabilidade tanto horizontal quanto vertical, dessa forma, facilitando o aumento de carga.
- **Considerações:** É importante usar técnicas e métodos como balanceamento de carga ou cache buscando estabilidade.

### Manutenção:

- **Impacto:** A distinção dos "pedaços" modelos, viewa e controlers torna a manutenção do código mais prática, praticamente exterminando o impacto de mudanças de um em outros.
- **Considerações:** Boas práticas de desenvolvimento, testes de código e processos de controle são extremamente importantes para estabilidade com o decorrer do tempo.

### Testabilidade:

- **Impacto:** A arquitetura MVC facilita a testabilidade da aplicação devido à separação clara de responsabilidades entre os componentes.
- **Considerações:** Sem os testes unitários não é possível assegurar um bom e correto funcionamento da aplicação.

### Segurança:
- **Impacto:** Fornece apenas uma estrutura para colocar em ação as medidas necessárias de segurança em camadas variadas da aplicação.
- **Considerações:** É muito importante que haja  validação de autenticação, entrada, autorização e prevenção de vulnerabilidades conhecidas na solução web.
