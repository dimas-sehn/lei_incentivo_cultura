# Visualização interativa de dados da SALIC WEB

## Este repositório descreve o projeto de visualizaçaõ interativa de dados da lei de incentivo à cultura.

**1. Geração dos dados:** Os dados são gerados pelo fluxo de projetos cadastrados na plataforma VerSalic e acessados via API (Interface de Programação de Aplicação) pública, a documentação é disponível no link <http://api.salic.cultura.gov.br/doc/>. A API é considerada pública quando não há necessidade de chave privada para acessar. Na plataforma estão disponíveis os dados sobre:

**2. Projetos:** Conjunto de ações/atividades culturais que buscam alcançar objetivos específicos, dentro dos limites de um orçamento e tempo determinados. O Projeto recebe um número de registro, Pronac, após aprovação da Proposta junto ao MinC.
Propostas: Requerimento apresentado pelo Proponente, por meio do SALIC, com o objetivo de obter aprovação pelo MinC para captar recursos via incentivo fiscal da Lei Rouanet (Lei nº 8.313/91)

**3. Proponentes:** Pessoa física com atuação na área cultural ou pessoa jurídica de direito público ou privado, com ou sem fins lucrativos, cujo ato constitutivo ou instrumento congênere disponha sobre sua finalidade cultural e com atuação na área. Responsável por apresentar, realizar e responder pelo Projeto cultural.
Incentivadores: Contribuinte do Imposto sobre a Renda e Proventos de qualquer natureza, pessoa física ou jurídica, que efetua doação ou patrocínio em favor dos Projetos aprovados pelo Ministério da Cultura, com vistas a incentivos fiscais, conforme estabelecido na Lei nº 8.313, de 1991.
Fornecedores: Pessoa física ou jurídica que teve bens ou serviços contratados pelo Proponente para a execução do Projeto cultural. (Versalic, [s.d.], online)

**4. Extração dos dados:** A extração dos dados foi feita através da plataforma Google Coolab4 com a linguagem de programação Python5. O código em python é lido linha por linha e funciona executando funções, cada trecho do código define funções que vão ser executadas para atingir o objetivo que é extrair os dados do VerSalic e armazenar em um banco de dados privado. Primeiro são importadas as bibliotecas, que são conjuntos de códigos armazenados em bibliotecas de código que podem ser acionadas a partir de comandos. Depois o código decodifica o texto da fonte de dados em formato JSON no padrão UTF-8, interpretando caracteres especiais como “ç” e “ã”. A API tem uma limitação, só permite que sejam extraídos dados de 100 em 100 linhas, por isso é necessário programar um loop para que o código rode de 100 em 100 linhas, cada vez que o código é executado ele armazena um arquivo offset.txt com a posição da última linha que foi extraída, para que na próxima vez que o código seja executado, a extração parta de onde parou e não do início. Depois é determinada a função de armazenamento no “bucket” do google, que é um banco de dados, como o banco de dados é privado é necessário incluir no código uma chave privada para autorizar o acesso e salvar os dados extraídos da API no banco de dados. Com todas as definições determinadas, o código é programado para concluir a extração apenas quando se esgotarem os dados na fonte e é programado para retornar mensagens de erro pré determinadas para alguns erros previstos e uma mensagem de sucesso caso tudo ocorra como esperado. Assim foi realizada a extração dos dados da API VerSalic e armazenados em banco de dados privado.

** 5. Processamento dos dados:** A linguagem JSON6 foi utilizada para normalizar e padronizar os dados para que possam ser armazenados e posteriormente interpretados.
Armazenamento de dados: Os arquivos JSON foram as armazenados na Google Cloud Platform em buckets7. Através de uma chave privada, o bucket no Google Cloud recebeu os arquivos JSON.
Administração de dados: Os arquivos foram separados pelos nomes e podem ser atualizados conforme novos dados forem gerados.
Análise de dados: A análise de dados é o processo de criar tabelas definindo as colunas e as variáveis. A plataforma utilizada para isso foi a Google Big Query, nela é possível criar e editar tabelas utilizando linguagem SQL (Structured Query Language), uma linguagem de programação para realizar consultas aos dados armazenados e realizar cruzamentos e análises entre eles.

** 6. Visualização de dados:** A visualização dos dados foi realizada no Looker Studio podendo ser visualizada no link <https://lookerstudio.google.com/reporting/1bc9f7d6-c2ac-4b26-9643-9e0c01e3d852/page/2RAXD> Nessa plataforma é possível fazer agregações, incluir textos, imagens e gráficos, painéis, tabelas e cartões de pontuação.

