## Desafio de data science para formação de ciência de dados - Indicium

 Projeto realizado com objetivo de colocar em prática os conteúdos lecionados durante o programa lighthouse para formação em ciência de dados. O desafio basea-se na análise de séries temporais, especificamente sobre o dataset de [GDP](https://www.imf.org/en/Home) com objetivos principais de traçar estratégias para imputação dos valores faltantes, e realizar predições para os anos de 2024 à 2028

## Estratégias adotadas

#### Dados faltantes

 - Aqui, é possível notar que além de existir uma grande quantidade de valores faltantes, esses valores são recorrentes em períodos contíguos, e não dispersos sobre todo o período de análise, o que pode dificultar possível interpolações baseadas nos dados do próprios país.
 
 - Dessa forma, é válido observar que pode ser vantajoso a análise por grupos econômicos, visto que esses grupos são formados por caracerísticas econômicas similares e cada participante possui determinada influência em seu grupo. Os grupos aqui listados são denominados de *Analytical Groups*, que podem ser encontrados em [IMF](https://www.imf.org/en/Publications/WEO/weo-database/2023/April/groups-and-aggregates).

 - Para isso, é impotante que os dados de cada grupo tenha menos ou nenhum valor faltante, além disso, podemos utilizar a correlação entre países, desconsiderando proximidades geográficas e sim apenas fatores econômicos, visto que devido a economia globalizada, algums países possuem grandes influências em outros.

#### Forecast

Dentro do catálogo de modelos disponíveis na biblioteca statsforecast, a escolha dos modelos se baseia em um caráter exploratório de difentes classes que levam ou não em consideração padrões de sazonalidades ou tendências, visto que todos serão aplicados a cada uma das séries e, como observado no EDA, existem séries bastantes ruidosas e outras com caráter mais suave e com possíveis tendências.

- AutoArima: Modelo que se ajusta de forma autoática aos parâmetros de um modelo ARIMA (Auto-regressive Integraded Moving Average), combinando componentes autoregressivos e de média móvel para realizar a captura de tendências e autocorrelações dentro da série.

- HistoricAverage: Modelo que pode ser utilizado como basline, se baseia na média histórica da série temporal para produzir previsões. Não considera nenhum tipo de variação dos dados e pode ser utilizado em séries muito ruidosas e sem padrão aparente. Podendo se encaixar bem algumas séries jaqui obseervadas

- RandomWalkWithDrift: Modelo que assume que o valor futuro será igual ao valor atual mais um termo de tendênciam tendo uma evolução "aleatória", com alguma tendência de aumento ou diminuição ao longo do tempo. também não leva em conta tendências ou sazonalidades nos dados.

- DynamicOptimizedTheta: Modelo que propõe a decomposição da série temporal em duas ou mais "linhas theta" que realçam os movimentos de curto e longo prazo nos dados. A seleção dessas linhas são enão otimizadas com base em diferentes esquemas de validação onde a precisão fora da amostra dos candidatos é medida.

### Métricas de avaliação

##### MAPE
- O MAPE é uma média de diferenças percentuais absolutas entre os valores previstos e reais.
- É expresso como uma porcentagem, tornando fácil de entender e comparar com os valores da base de dados.
- O MAPE é menos sensível a valores discrepantes do que o RMSE, no entanto, pode ser problemático quando os valores reais estão próximos de zero ou quando há valores extremos nos dados, pois devido à divisão, os resultados podem explodir.

## Como executar o projeto

1. Para execução do projeto, realize um fork do repositório e um clone para sua máquina local.

```
git clone https://github.com/Lineker98/desafio_ds.git
```

2. Crie um abiente virtual para instalação das dependências com:

- Criação do ambiente virtual para instalação das dependências:
```
pip install virtualenv
```

- Com o venv instalado, e dentro do diretório do projeto, execute:
```
python3 -m venv <nome_do_ambiente>
```

- Para ativação do ambiente, digite no terminal
    - Linux:
    ```console
    source <nome_do_ambiente>/bin/activate
    ```

    - Windows:
    ```
    <name_do_ambientet>\Scripts\activate
    ```

3. Instalação das depedências:

- Dentro do diretório do projeto, abra o terminal e digite:
```
pip install -r requirements.txt
```

Você já está apto para executar o projeto, basta digitar no seu terminal o comando ``jupyter lab`` para navegar entre os dados e os notebooks.