# DP100-Estudos
## deploy_target 
`AKS Compute`:
- O que é?: Um destino de computação para **implantação de modelos**.
- Uso principal: É usado para inferência em **tempo real** que requer **alta escalabilidade e disponibilidade**. É a opção ideal para um "cluster de inferência" em ambiente de produção.

`AmlCompute`:
- É o recurso de computação gerenciado pelo próprio Azure Machine Learning. É utilizado principalmente para **treinamento de modelos e processamento de dados**, permitindo escalabilidade automática de nós de computação.

`RemoteCompute`: É uma forma de **anexar um ambiente de computação já existente** (como uma máquina virtual ou um cluster de terceiros) que **não é gerenciado pelo Azure ML**. É tipicamente usado para **treinamento**.

`BatchCompute`: É usado para **inferência em lote (batch)**, ou seja, para jobs que processam grandes volumes de dados de uma só vez, sem a necessidade de uma resposta imediata. É ideal para tarefas assíncronas.

## deployment_config 

`AksWebservice` : Uso: Usada para implantar um serviço web em um cluster do Azure Kubernetes Service (AKS). É ideal para ambientes de produção, oferecendo escalabilidade, alta disponibilidade e monitoramento.
`AciWebservice`: Uso: Usada para implantar um serviço web em uma Instância de Contêiner do Azure (ACI). É uma opção mais rápida e simples para testes ou para cargas de trabalho de pequena escala que não exigem um cluster completo.
`LocalWebservice`: Uso: Usada para implantar e testar o serviço web localmente na sua máquina. É uma forma de depuração e validação antes de implantar na nuvem.

## Configuração de Autenticação
`auth_enabled=True/False` : autenticação por key
`token_auth_enabled=True/False`: token active directory

## Resumo das Importações
`Webservice`: Esta é a classe base para qualquer serviço web implantado no Azure Machine Learning. Você a usa para criar um objeto que representa o serviço implantado na nuvem.
`requests`: Este não é um módulo do Azure ML, mas sim a popular biblioteca Python para fazer requisições HTTP. No contexto do Azure ML, você a usaria para chamar a API de um modelo diretamente, sem usar o SDK nativo.
`LocalWebservice`: Esta é uma classe específica para testar e depurar um modelo localmente, antes de implantá-lo na nuvem. Ela cria um serviço web temporário na sua própria máquina.

## Resumo da Invocação do Modelo (API)

`service.run()`: Método nativo do SDK para chamar a API de um modelo implantado. É a forma programática e recomendada.
`requests.post()`: Método para fazer uma chamada HTTP/REST API direta para o endpoint do modelo. Funciona, mas não é o método nativo do SDK.
`deserialize`: converte dados de uma api para objeto python

## Bias e Variança de modelos de árvore

- Viés (Bias): Erro causado por um modelo ser muito simples (subajustado). Ele não consegue capturar a complexidade dos dados.
  - Exemplo: Uma árvore de decisão com baixa profundidade (como 5) tem alto viés.
  - Baixa profundidade = alto vies, alta profundidade = baixo viés

- Variância (Variance): Erro causado por um modelo ser muito complexo (superajustado). Ele aprende o ruído dos dados de treino em vez de se generalizar bem.
  - Exemplo: Uma árvore de decisão com alta profundidade (como 15) tem alta variância.
  - Alta profundidade:alta variança, baixa profundidade:baixa variança

## Tipos de Computação para ML

- Computação sem servidor: É a opção mais moderna e gerenciada para treinamento de ML automatizado. Ela abstrai a infraestrutura e dimensiona automaticamente, o que a torna ideal para escalabilidade em trabalhos de larga escala.
- Instância de computação: É uma máquina virtual gerenciada por você. É mais adequada para um ambiente de desenvolvimento e exploração de dados, ou para executar tarefas que não exigem um cluster, pois geralmente é um único nó.
- Cluster do Kubernetes: É um cluster de vários nós, ideal para implantações de produção que requerem alta escalabilidade para inferência em tempo real. Embora possa ser usado para treinamento, a computação sem servidor é a opção preferida para ML automatizado.
- Extremidade: Este termo se refere à computação de borda (edge computing), que é o processamento de dados mais perto de onde eles são coletados, como em dispositivos IoT. É usada para implantar modelos em dispositivos de borda, não para o treinamento centralizado.

## Política de segurança:
- `TruncationSelectionPolicy`: Funciona por truncação. Ela "corta" (para) uma porcentagem dos treinamentos com o pior desempenho a cada intervalo de avaliação. É uma abordagem mais simples e direta.
- `BanditPolicy`: Funciona com um fator de folga. Ela interrompe um treinamento se o seu desempenho cair abaixo do melhor desempenho até o momento por uma "margem de folga". É uma abordagem mais dinâmica, que compara os resultados continuamente.
