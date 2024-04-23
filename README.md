<div align="center">
  
  <h1>Tutorial-Azure-ML</h1>
  
</div>

<div align="center">

  ![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/9e8b97cf-93ac-4daf-b9e3-f0fc656ec883)
  
<hr>
  
  ![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/d8156e05-3945-4f0c-ba4d-3796e24466e4)
  
</div>

<br>

## 1° Passo: Criar um recurso de Azure Machine Learning.

1. Faça login no portal do Azure em [https://portal.azure.com](https://portal.azure.com) usando suas credenciais da Microsoft.

2. Selecione **+ Criar um recurso**, pesquise por **Machine Learning**, e crie um novo recurso de Azure Machine Learning com as seguintes configurações:

- **Assinatura:** Sua assinatura do Azure.
- **Grupo de recursos:** Crie ou selecione um grupo de recursos.
- **Nome:** Insira um nome único para o seu espaço de trabalho.
- **Região:** Selecione a região geográfica mais próxima.
- **Conta de armazenamento:** Observe a nova conta de armazenamento padrão que será criada para o seu espaço de trabalho.
- **Cofre de chaves:** Observe o novo cofre de chaves padrão que será criado para o seu espaço de trabalho.
- **Aplicação Insights:** Observe o novo recurso de Application Insights padrão que será criado para o seu espaço de trabalho.
- **Registro de contêiner:** Nenhum (um será criado automaticamente na primeira vez que você implantar um modelo em um contêiner).

3. Selecione **Revisar + criar**, e então selecione **Criar**. Aguarde a criação do seu espaço de trabalho (isso pode levar alguns minutos) e depois vá para o recurso implantado.

4. Selecione **Iniciar studio** (ou abra uma nova aba do navegador e acesse [https://ml.azure.com](https://ml.azure.com), e faça login no Azure Machine Learning studio usando sua conta da Microsoft). Feche quaisquer mensagens que aparecerem.

5. No Azure Machine Learning studio, você deverá ver seu espaço de trabalho recém-criado. Caso contrário, selecione **Todos os espaços de trabalho** no menu à esquerda e depois selecione o espaço de trabalho que você acabou de criar.

<hr>

## 2° Passo: Use aprendizado de máquina automatizado para treinar um modelo.

### Treinar um modelo usando Aprendizado de Máquina Automatizado (Automated ML)

No Azure Machine Learning studio, acesse a página Automated ML (em Authoring).

Crie um novo trabalho de Automated ML com as seguintes configurações, avançando pela interface do usuário conforme necessário:

### Configurações básicas:

- **Nome do trabalho:** mslearn-bike-automl
- **Nome do experimento:** mslearn-bike-rental
- **Descrição:** Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
- **Tags:** Nenhuma

### Tipo de tarefa e dados:

- **Selecione o tipo de tarefa:** Regressão
- **Selecione o conjunto de dados:** Crie um novo conjunto de dados com as seguintes configurações:
  - **Tipo de dados:**
    - **Nome:** bike-rentals
    - **Descrição:** Dados históricos de aluguel de bicicletas
    - **Tipo:** Tabular
  - **Fonte de dados:**
    - **Selecionar de arquivos da web**
    - **URL da web:** https://aka.ms/bike-rentals
  - **Configurações:**
    - **Formato do arquivo:** Delimitado
    - **Delimitador:** Vírgula
    - **Codificação:** UTF-8
    - **Cabeçalhos de coluna:** Somente o primeiro arquivo possui cabeçalhos
    - **Pular linhas:** Nenhuma
    - **O conjunto de dados contém dados de várias linhas:** Não
  - **Esquema:**
    - Inclua todas as colunas, exceto Path
    - Revise os tipos detectados automaticamente
  - **Selecionar Criar.** Depois que o conjunto de dados for criado, selecione o conjunto de dados bike-rentals para continuar a submissão do trabalho Automated ML.

### Configurações da tarefa:

- **Tipo de tarefa:** Regressão
- **Conjunto de dados:** bike-rentals
- **Coluna alvo:** Rentals (inteiro)
- **Configurações adicionais:**
  - **Métrica primária:** Erro quadrático médio de raiz normalizado
  - **Explicar o melhor modelo:** Não selecionado
  - **Usar todos os modelos suportados:** Não selecionado. Você restringirá o trabalho a tentar apenas alguns algoritmos específicos.
  - **Modelos permitidos:** Selecione apenas RandomForest e LightGBM.
  - **Limites:**
    - **Número máximo de tentativas:** 3
    - **Tentativas simultâneas máximas:** 3
    - **Máximo de nós:** 3
    - **Limite de pontuação da métrica:** 0.085 (para que, se um modelo alcançar uma pontuação de métrica de erro quadrático médio de raiz normalizado de 0.085 ou menos, o trabalho termine.)
    - **Tempo limite:** 15
    - **Tempo limite de iteração:** 15
    - **Ativar término antecipado:** Selecionado
- **Validação e teste:**
  - **Tipo de validação:** Divisão de treinamento-validação
  - **Percentual de dados de validação:** 10
  - **Conjunto de dados de teste:** Nenhum

### Computação:

- **Selecionar tipo de computação:** Serverless
- **Tipo de máquina virtual:** CPU
- **Nível da máquina virtual:** Dedicado
- **Tamanho da máquina virtual:** Standard_DS3_V2*
- **Número de instâncias:** 1
* Se sua assinatura restringir os tamanhos de VM disponíveis para você, escolha qualquer tamanho disponível.

Envie o trabalho de treinamento. Ele inicia automaticamente.

Aguarde o término do trabalho. Pode levar um tempo - agora pode ser um bom momento para uma pausa para o café!

### Passo a passo representado em imagens:

![ml1](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/95a4f85f-6514-4679-befe-a20aa529370e)

![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/5ed698f7-11af-437f-a41f-6bd135c984d4)

![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/a8ffeb0c-09de-4001-a916-9c11848a8d89)

![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/d7f08bd6-755d-4da6-909d-1774c6c95036)

![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/0b7fb677-41f7-461e-a974-e56e3cf375d0)

![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/2752b632-47fb-46ce-9a6a-615cf4383a90)

![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/deeee924-09d3-42fd-b060-2fbe87680aac)

![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/7df83046-d035-4076-8918-748016006ab1)

![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/81f1d668-8643-4a98-8e0b-0c2c8246c8ae)

![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/a3f07d1f-77e9-44ff-afb3-f4776803aa82)

![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/b7800835-81d8-450e-a16a-56887f7b9cca)

![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/b44c197a-cade-40c3-891a-3569bbe98799)

![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/6cd7b42c-eb68-41fc-a7e8-0209988e8030)

![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/679adcee-4427-4af6-b3c5-c83875b7a35a)

<hr>

## 3° Passo: Revisão do Melhor Modelo.

Quando o trabalho de aprendizado de máquina automatizado for concluído, você poderá revisar o melhor modelo treinado.

1. Na guia Visão geral do trabalho de aprendizado de máquina automatizado, observe o resumo do melhor modelo. Captura de tela do resumo do melhor modelo do trabalho de aprendizado de máquina automatizado com um destaque em torno do nome do algoritmo.

![image](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/7e0c4ad5-b815-4120-b747-47a47b3751a9)

> **Observação:** Você pode ver uma mensagem sob o status "Aviso: Pontuação de saída especificada pelo usuário atingida...". Esta é uma mensagem esperada. Por favor, continue para a próxima etapa.

2. Selecione o texto sob o nome do algoritmo para o melhor modelo para visualizar seus detalhes.

3. Selecione a guia Métricas e selecione os gráficos de resíduos e previsto_verdadeiro se eles ainda não estiverem selecionados.

Revise os gráficos que mostram o desempenho do modelo. O gráfico de resíduos mostra os resíduos (as diferenças entre os valores previstos e reais) como um histograma. O gráfico previsto_verdadeiro compara os valores previstos com os valores reais.

<hr>

## 4° Passo: Implante e teste o modelo.

Na guia Modelo para o melhor modelo treinado pelo seu trabalho de aprendizado de máquina automatizado, selecione **Implantar** e use a opção **Serviço da Web** para implantar o modelo com as seguintes configurações:

- **Nome:** predict-rentals
- **Descrição:** Prever aluguéis de bicicletas
- **Tipo de computação:** Instância de Contêiner do Azure
- **Habilitar autenticação:** Selecionado

Aguarde o início do processo de implantação - isso pode levar alguns segundos. O status de Implantação para o endpoint predict-rentals será indicado na parte principal da página como **Executando**.

Aguarde o status de Implantação mudar para **Concluído**. Isso pode levar de 5 a 10 minutos.

<hr>

## 5° Passo: Teste o serviço implantado.

Agora você pode testar o serviço implantado.

1. No Azure Machine Learning studio, no menu à esquerda, selecione **Endpoints** e abra o endpoint em tempo real predict-rentals.

2. Na página do endpoint em tempo real predict-rentals, visualize a guia **Teste**.

3. Na seção de Dados de entrada para testar o endpoint, substitua o JSON modelo pelos seguintes dados de entrada:

````
{
  "Inputs": { 
    "data": [
      {
        "day": 1,
        "mnth": 1,   
        "year": 2022,
        "season": 2,
        "holiday": 0,
        "weekday": 1,
        "workingday": 1,
        "weathersit": 2, 
        "temp": 0.3, 
        "atemp": 0.3,
        "hum": 0.3,
        "windspeed": 0.3 
      }
    ]    
  },   
  "GlobalParameters": 1.0
}
````

5. Clique no botão Testar.

6. Revise os resultados do teste, que incluem o número previsto de aluguéis com base nas características de entrada - semelhante a isto:

````
{
  "Results": [
    444.27799000000000
  ]
}
````

O painel de teste utilizou os dados de entrada e o modelo que você treinou para retornar o número previsto de aluguéis.

Vamos revisar o que você fez. Você utilizou um conjunto de dados históricos de aluguéis de bicicletas para treinar um modelo. O modelo prevê o número de aluguéis de bicicletas esperado em um determinado dia, com base em características sazonais e meteorológicas.

### Ilustração:

![ml2](https://github.com/DevGustavus/Tutorial-Azure-ML/assets/103593279/0def9d32-696a-4bf9-a9c9-c3c665fe0469)

<hr>

## 6° Passo: Limpeza.

O serviço da web que você criou está hospedado em uma Instância de Contêiner do Azure. Se você não pretende experimentá-lo mais, deve excluir o endpoint para evitar acúmulo de uso desnecessário do Azure.

1. No Azure Machine Learning studio, na guia Endpoints, selecione o endpoint predict-rentals. Em seguida, selecione Excluir e confirme que deseja excluir o endpoint.

Excluir sua computação garante que sua assinatura não será cobrada por recursos de computação. No entanto, você será cobrado uma pequena quantia pelo armazenamento de dados enquanto o espaço de trabalho do Azure Machine Learning existir em sua assinatura. Se você terminou de explorar o Azure Machine Learning, pode excluir o espaço de trabalho do Azure Machine Learning e os recursos associados.

Para excluir seu espaço de trabalho:

1. No portal do Azure, na página de Grupos de recursos, abra o grupo de recursos que você especificou ao criar seu espaço de trabalho do Azure Machine Learning.
2. Clique em Excluir grupo de recursos, digite o nome do grupo de recursos para confirmar que deseja excluí-lo e selecione Excluir.

<hr>

## Meus resultados:

````
{
  "Results": [
    360.99138733679985
  ]
}
````
