# Projeto de Integração de Sistemas de Informação (ETL)

## Visão Geral

Este projeto foi desenvolvido no âmbito da Unidade Curricular de **Integração de Sistemas de Informação (ISI)** da Licenciatura em Engenharia de Sistemas Informáticos do Instituto Politécnico do Cávado e do Ave (IPCA).

O objetivo principal é demonstrar a aplicação de um processo de **ETL (Extract, Transform, Load)** para integrar, limpar, validar e analisar dados de múltiplas fontes heterogéneas. A solução utiliza o **Apache Hop** para a orquestração e transformação dos dados e o **Node-RED** para a visualização dos resultados num dashboard.

O cenário de negócio fictício é a empresa "CarExpress", que necessita de consolidar dados de inventário de veículos (em formato CSV) com os seus registos de vendas (em formato XML) para gerar métricas de negócio.

---

## Tecnologias Utilizadas

* **ETL Tool:** [Apache Hop](https://hop.apache.org/)
* **Dashboard e Visualização:** [Node-RED](https://nodered.org/) com `node-red-dashboard`
* **Formatos de Dados:** CSV, XML, JSON

---

## Funcionalidades Principais

O processo de ETL implementado inclui as seguintes funcionalidades:

* **Extração de Múltiplas Fontes:** Leitura e *parsing* de ficheiros `.csv` e `.xml`.
* **Limpeza e Padronização de Dados:**
    * Remoção de espaços e conversão de texto (maiúsculas/minúsculas).
    * Normalização de dados através de mapeamento de valores (ex: "vw" -> "volkswagen").
* **Validação de Dados:**
    * Filtragem de registos com campos essenciais nulos.
    * Validação de formato de matrículas utilizando **Expressões Regulares**.
* **Enriquecimento e Transformação:**
    * Conversão de unidades (milhas para quilómetros).
    * *Parsing* de múltiplos formatos de data com recurso a scripts **JavaScript**.
* **Integração e Junção de Dados:**
    * Combinação dos dados de inventário e vendas através de um `Merge Join` com base na matrícula do veículo.
* **Agregação de Dados:**
    * Cálculo de métricas de negócio (nº de vendas, médias de CO2 e de valor) por marca, utilizando a operação `Group By`.
* **Orquestração e Gestão de Erros:**
    * Um **Workflow** (`.hwf`) que verifica a existência dos ficheiros de entrada antes de executar o pipeline.
    * Registo de erros centralizado e geração de ficheiros de saída para dados inválidos ou inconsistentes (ex: `matriculas_invalidas.xml`, `carros_nao_vendidos.xml`).
* **Carregamento e Visualização (Load):**
    * Envio dos dados agregados em formato JSON para um *endpoint* REST em Node-RED.
    * Apresentação dos resultados em gráficos de barras num dashboard dinâmico.

---

## Como Executar o Projeto

Para executar este projeto, são necessários os seguintes pré-requisitos:

### Pré-requisitos

1.  **Apache Hop:** [Instalar o Apache Hop](https://hop.apache.org/download/).
2.  **Node-RED:** [Instalar o Node.js e o Node-RED](https://nodered.org/docs/getting-started/local).
3.  **Node-RED Dashboard:** Instalar o módulo `node-red-dashboard` no Node-RED através do *Manage Palette*.

### Passos de Execução

1.  **Clonar o Repositório:**
    ```bash
    git clone [https://github.com/fabiocosta191/Projeto_ISI_Tb1.git](https://github.com/fabiocosta191/Projeto_ISI_Tb1.git)
    cd Projeto_ISI_Tb1
    ```

2.  **Configurar o Node-RED:**
    * Inicie o Node-RED no seu terminal com o comando `node-red`.
    * Aceda a `http://127.0.0.1:1880/` no seu navegador.
    * No menu, vá a `Import` e importe o ficheiro `flows.json` deste repositório.
    * Clique em **Deploy** para ativar o fluxo. O dashboard estará disponível em `http://127.0.0.1:1880/ui`.

3.  **Executar o Processo ETL:**
    * Abra a GUI do Apache Hop.
    * Abra o ficheiro do workflow `filename.hwf`.
    * As variáveis de projeto (`PROJECT_HOME`) devem ser configuradas para o caminho do diretório do projeto.
    * Clique no botão **Run** para iniciar a execução do workflow.

4.  **Verificar os Resultados:**
    * Após a execução, os ficheiros de resultado serão gerados na pasta `/result`.
    * O dashboard no Node-RED (`http://127.0.0.1:1880/ui`) será automaticamente atualizado com os gráficos. O pipeline inclui um passo que tenta abrir o navegador neste URL.

---

## Vídeo de Demonstração

Um vídeo completo a demonstrar a execução do projeto está disponível no seguinte link:

[**Vídeo de Demonstração do Projeto**](https://alunosipca-my.sharepoint.com/:v:/g/personal/a22997_alunos_ipca_pt/Ea7394t0NudHl4-Iw3NyTqoBsLsvC0VknLMu7l6fM6mfwA?e=FJNZGh)

---

## Autor

* **Fábio Costa** - [fabiocosta191](https://github.com/fabiocosta191)
