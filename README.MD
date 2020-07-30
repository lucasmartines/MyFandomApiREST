# Aplicativo de fandom
### Objetivo do aplicativo:
O aplicativo de fandom permite gerenciar uma fandom de anime, ou mangá. Nela é possível se obter informações sobre animes, autores, personagens, fazer comentários, administrar usuários etc.

## Objetivo do projeto:
 - Implementar uma api para aprendizado e consolidação das seguintes tecnologias e conceitos: 
 - Spring Boot Core
 - Spring Boot Web Module
 - Spring Boot Data Module
 - Spring Security Module
 - Controle de acesso
 - Controle de permissões
 - Validação de dados
 - Java persistence API (JPA)
 - Rest e RestFul
 - Aplicação dividida em camadas: persistence, service, domain, application.
 - Testes de unidade e integração básico
 - Cobertura de código básico

### Entidades Importantes:
 - Anime
 - Categoria
 - Personagem
 - Comentários sobre anime e personagem.
 - Usuário/Administrador
 - Permissões
 - Roles


# Controllers:
 - ### /usuario
 -  - [post]/usuario/cadastrar
 -  - [post]/usuario/logar
 -  - [post]/usuario/pegar_token
 -  - [get]/usuario/roles
 - ### /anime
 -  - /anime/{123}/registrarComentario 
 -  - /anime/{123}/deletarComentario ( admin, user[limitado] )
 -  - /anime/{123}/verComentarios 
 -  - /anime/{123}/verCategoria 
 -  - [post]/anime/{123}/adicionarCategoria ( admin )
 -  - /anime/{123}/verCategorias 
 -  - /anime/categorias 
 -  - /anime/?pagina={numero} 
 - ### /personagem
 - -  /personagem/{123}/registrarComentario 
 - - /personagem/{123}/deletarComentario
 - - /personagem/{123}/verComentarios 
 -  - /personagem/?pagina={numero}
 -  - /categoria
 -  - /categoria/[crud]/
 -  - /categoria/{123}/inserirAnime
 -  - /categoria/{123}/inserirPersonagem

## Requisitos Funcionais da API:
 - O sistema deve: retornar uma listagem de anime com paginação de 8 animes, incluindo o link de next e preview, e a quantidade de páginas, um link para os personagens.  Na listagem é possível escolher por parâmetro que represente uma página escolhida.
 - O sistema permite que para cada Anime e Personagem, seja possível registrar/ver/deletar comentários.
 - O sistema deve: inserir/pegar uma ou mais categorias relacionadas ao personagem e anime.
 - Regra de Negócio: O usuário pode deletar os próprios comentários, mas não pode deletar os comentários dos outros.
 - Regra de Negócio: O usuário com permissão de administrador ou permissão de moderador pode deletar os comentários de outros usuários desde que ele seja o “criador” do registro do anime. 
 - Regra de Negócio: O usuário cadastrado pode criar animes, e sendo o dono desse anime ele pode delegar responsabilidades para outros usuários, como o direito de poder deletar ou atualizar um anime, e administrar comentários.
 - Regra de Negócio: O sistema deve evitar que um usuário não cadastrado possa inserir um anime e um personagem, mas deve permitir comentários. Uma mensagem de erro com o status bad request deve ser enviada para o cliente.
 - O sistema deve: receber uma requisição REST para poder inserir/atualizar/deletar um anime.
 - O sistema deve: receber uma  requisição REST para poder inserir/atualizar/deletar uma categoria.
 - O sistema deve: receber uma  requisição REST para poder inserir/atualizar/deletar um(a) personagem.
 - O sistema deve: receber uma  requisição REST para poder inserir/atualizar/deletar um(a) comentário.
 - O sistema deve: receber uma  requisição REST para poder inserir/atualizar/deletar um(a) usuário.
 - Definição de Dados: O usuário terá as seguintes informações: id para ser único, nome, senha, idade.
 - Definição de Dados: O comentário terá as seguintes informações: id do dono do comentario, id alvo do comentário para personagem, id alvo para anime, mensagem.
 - Definição de Dados: A categoria terá apenas o nome único e um id.
 - Definição de Dados: O anime terá uma referência para: o usuário dono, nome do anime,  resumo, descricao, uma lista de comentários, lista de personagens, author da obra.
 - Definição de Dados: O personagem tem: id , nome, idade, descrição de aparência,  história, dublador.

###  Definições de permissões
 - Um usuário comum pode: ver anime, personagem, categorías, comentar
 - Um usuário cadastrado pode tudo que o comum pode mais: criar um anime, criar personagens para anime, criar categorías.
 - Um usuário dono do anime pode tudo que um cadastrado pode mais: atualizar o anime, delegar sua permissão de dono para outros usuários, deletar comentários em seu anime, e no anime dos outros que têm permissões de dono.

### Requisitos não funcionais
 - O serviço é uma API rest portanto deve seguir as convenções básicas REST e Restful, recebendo parâmetros de controle e filtro na url, e retornando um arquivo no formato json.
 - Fica a cargo do programador escolher os padrões rest, restful mas o código deverá ter consistência. Exemplo que foi inicialmente determinado que o nome da rota de requisição endpoint é /usuário ou /personagem então não crie /usuários /personagem , ou se o método http delete não retorna nada em usuário, então também não deve retornar nada em personagem.
 - O aplicativo é em português mas o código será em inglês.
Será usado jwt para autenticação.

### Rotas
http://app-route/{versionNumber}:port/{controller}/method/PathParam?QueryParam=x
