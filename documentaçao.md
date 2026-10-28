1. Visão Geral do Projeto
O Sistema de Gerenciamento de Voos e Passagens é uma aplicação desenvolvida na linguagem C que roda em ambiente de linha de comando (console/terminal). O software simula operações básicas de uma companhia aérea, permitindo o cadastro de voos, controle de disponibilidade de assentos, emissão de passagens (reservas) e consulta de dados em tempo de execução.

2. Arquitetura e Estrutura de Dados
O sistema faz uso de vetores estáticos globais para armazenar os registros em memória RAM e utiliza structs (estruturas) para modelar as entidades do domínio.

2.1. Definições e Constantes
MAX_VOOS 100: Número máximo de voos que podem ser cadastrados.

MAX_PASSAGENS 500: Número máximo de passagens/reservas que podem ser emitidas.

2.2. Modelagem de Dados (structs)
Voo: Representa um trajeto aéreo oferecido.
typedef struct {
    int codigo;          // Identificador único do voo (gerado automaticamente)
    char origem[50];     // Cidade de partida
    char destino[50];    // Cidade de chegada
    int assentos;        // Quantidade atual de assentos disponíveis
    float preco;         // Valor da passagem (R$)
} Voo;
Passagem: Representa uma reserva vinculada a um passageiro e a um voo.
typedef struct {
    int idPassagem;      // Identificador único da reserva
    int codigoVoo;       // Código do voo associado
    char nomePassageiro[100]; // Nome completo do passageiro
} Passagem;
3. Funcionalidades e Módulos do Sistema
3.1. Módulo de Cadastro de Voos (cadastrarVoo)
Objetivo: Adicionar novas rotas ao sistema.

Comportamento:

Verifica se o limite máximo de voos (MAX_VOOS) foi atingido.

Atribui um código sequencial automático (totalVoos + 1).

Coleta via teclado: Origem, Destino, Assentos e Preço.

3.2. Módulo de Listagem de Voos (listarVoos)
Objetivo: Exibir todas as rotas ativas.

Comportamento:

Verifica se há voos cadastrados.

Formata e imprime uma tabela legível contendo código, origem, destino, assentos disponíveis e preço formatado em Reais (R$).

3.3. Módulo de Compra/Reserva (comprarPassagem)
Objetivo: Vender um bilhete para um passageiro.

Comportamento:

Lista os voos disponíveis para consulta prévia.

Solicita o código do voo desejado e valida sua existência.

Verifica se há assentos disponíveis (assentos > 0).

Solicita o nome completo do passageiro.

Efeito Colateral: Decrementa em 1 unidade a quantidade de assentos do voo selecionado e registra a nova passagem no vetor global.

3.4. Módulo de Listagem de Passagens (listarPassagens)
Objetivo: Exibir todas as reservas já emitidas.

Comportamento:

Percorre o vetor de passagens e exibe o ID da reserva, o código do voo correspondente e o nome do passageiro.

4. Fluxograma de Execução (Menu Principal)
O programa opera em um loop contínuo (do-while) controlado por um menu interativo baseado em opções numéricas de 1 a 5:
[Início do Programa]
         │
         ▼
 ┌───────────────────────┐
 │   Exibir Menu Principal│
 └──────────┬────────────┘
            │
            ├── [1] Cadastrar Voo ───────► Insere dados no vetor `voos`
            ├── [2] Listar Voos ─────────► Mostra tabela formatada de voos
            ├── [3] Comprar Passagem ────► Valida voo/assentos e gera reserva
            ├── [4] Listar Passagens ────► Exibe todas as reservas emitidas
            └── [5] Sair ────────────────► Encerra a execução do programa
   5. Guia de Compilação e Execução
Para compilar e executar o código-fonte (sistema_voos.c), utilize um compilador compatível com a linguagem C (como o GCC):

Compilação:
gcc sistema_voos.c -o sistema_voos
Execução:

Linux / macOS: ./sistema_voos

Windows: sistema_voos.exe

6. Limitações Conhecidas e Próximos Passos (Melhorias Futuras)
Persistência de Dados: Atualmente os dados são voláteis (salvos apenas em memória RAM). Como melhoria futura, pode-se implementar salvamento e leitura automática em arquivos .txt ou binários.

Tratamento de Entradas: O uso de scanf com  %[^\n]s resolve a leitura de strings com espaços, mas entradas incorretas de tipos de dados (ex: letras em campos numéricos) podem gerar comportamentos inesperados. Recomenda-se a implementação de validações mais robustas.

Cancelamento: Adicionar uma opção para cancelar passagens, o que deveria estornar o assento de volta ao voo correspondente.
