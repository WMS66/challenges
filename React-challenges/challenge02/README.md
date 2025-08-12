# React challenge #02

## Instruções:

- Você tem um formulário de login INCOMPLETO
- Não é permitido adicionar novos elementos HTML
- Não é permitido usar refs

## Tarefas:

- **todo** - O botão de login deve disparar a função login(), importada no topo deste arquivo, e passar os dados necessários.
- **todo** - Desabilite o botão de Login caso o e-mail esteja em branco ou a senha for menor que 6 dígitos.
- **todo** - Desabilite o botão de Login enquanto você está executando o login.
- **todo** - Mostre uma mensagem de erro de login() caso o Login falhe. A mensagem deve ser limpa a cada nova tentativa de Login.
- **todo** - Mostre um alerta caso o login seja efetuado com sucesso (javascript alert). Investigue a função login() para entender como ter sucesso na requisição.

<hr>

# Análise de Codigo desafio 02

## Estado e Funções

O componente utiliza o useState para gerenciar quatro estados principais:

    - email: Armazena o valor do campo de e-mail.

    - password: Armazena o valor do campo de senha.

    - error: Armazena a mensagem de erro, caso o login falhe. Inicialmente, ele é definido com um valor de "Deu erro !", mas na prática, é melhor iniciá-lo como null para evitar que a mensagem de erro seja exibida antes da primeira tentativa.

    - isRequesting: Um booleano que indica se uma requisição de login está em andamento.

As funções handleEmail e handlePassword são chamadas a cada mudança nos campos de input e atualizam os estados de email e password, respectivamente.

**Função** handleSubmit

Esta é a função central que orquestra o processo de login.

    - Limpeza de Estado: Primeiro, ela reseta o estado de error para null e define isRequesting como true. Isso limpa qualquer mensagem de erro anterior e desabilita o botão para evitar múltiplos cliques.

    - Chamada da API: Em seguida, ela chama a função login() (importada de outro arquivo), passando um objeto com o e-mail e a senha.

    - Tratamento da Promessa: A função login() retorna uma Promise, que é tratada com .then(), .catch() e .finally():

.then(): Se a requisição for bem-sucedida, ele limpa o campo de e-mail e exibe um alerta de sucesso.

.catch(): Se houver um erro, a mensagem de erro é capturada e salva no estado error.

.finally(): Esta parte é executada independentemente do sucesso ou falha da requisição. Ela define isRequesting como false, reabilitando o botão de login.

**_Renderização (JSX)_**

O JSX define a estrutura do formulário:

- **_Mensagem de Erro:_** A linha {error && <div className="errorMessage">{error.message}</div>} exibe a div de erro somente se a variável error não for nula, garantindo que a mensagem seja mostrada apenas quando necessário.

- **_Inputs:_** Os campos de e-mail e senha têm seus valores controlados pelos estados email e password e seus eventos onChange chamam as funções handleEmail e handlePassword.

- **_Botão de Login:_** O botão de login chama a função handleSubmit no evento onClick. A propriedade disabled é crucial aqui: o botão fica desabilitado se o email estiver vazio, se a password tiver menos de 6 dígitos, ou se isRequesting for true. Essa lógica atende a duas das tarefas principais do problema, garantindo a validação dos campos e a desabilitação durante a requisição.
