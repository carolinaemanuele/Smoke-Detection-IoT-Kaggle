UNIVERSIDADE FEDERAL DA Bahia

TOMORROW

CAROLINA EMANUELE SANTOS DE ARAÚJO

ANÁLISE DOS DADOS GERADOS POR UM DISPOSITIVO IOT DE DETECÇÃO DE FUMAÇA

SALVADOR - BAHIA

2024

Carolina Emanuele Santos de Araújo

ANÁLISE DOS DADOS GERADOS POR UM DISPOSITIVO IOT DE DETECÇÃO DE FUMAÇA

> Relatório apresentado à professora Mariese Santos como requisito
> parcial para obtenção de aprovação no curso de Ciência de Dados para
> Iniciantes com Python do projeto Tomorrow.

SALVADOR - BAHIA

2024

LISTA DE ILUSTRAÇÕES

**Figura 1:** Gráfico de densidade do atributo \'Temperature\[C\]\'
[11](#_Toc166238269)

**Figura 2:** Gráfico de densidade do atributo \'Humidity\[%\]\'
[12](#_Toc166238270)

**Figura 3:** Gráfico de densidade do atributo \'TVOC\[ppb\]'
[12](#_Toc166238271)

**Figura 4:** Gráfico de densidade do atributo \'eCO2\[ppm\]\'
[12](#_Toc166238272)

**Figura 5:** Gráfico de densidade do atributo \'Raw H2\'
[13](#_Toc166238273)

**Figura 6:** Gráfico de densidade do atributo \'Raw Ethanol\'
[13](#_Toc166238274)

**Figura 7:** Gráfico de densidade do atributo \'Pressure\[hPa\]\'
[13](#_Toc166238275)

**Figura 8:** Gráfico de densidade do atributo \'TotalNC\'
[14](#_Toc166238276)

**Figura 9:** Gráfico de densidade do atributo \'TotalPM\'
[14](#_Toc166238277)

**Figura 10:** Boxplots dos atributos quantitativos [14](#_Toc166238278)

**Figura 11:** Frequências dos atributos categóricos
[15](#_Toc166238279)

**Figura 12:** Heatmap de correlações de Pearson entre os atributos
[17](#_Toc166238280)

**Figura 13:** Gráfico de dispersão dos atributos Humidity\[%\] e
Pressure\[hPa\] [18](#_Toc166238281)

**Figura 14:** Gráfico de dispersão dos atributos TVOC\[ppb\] e Raw
Ethanol [18](#_Toc166238282)

**Figura 15:** Gráfico de dispersão dos atributos Raw H2 e eCO2\[ppm\]
[19](#_Toc166238283)

**Figura 16:** Gráfico de dispersão entre TotalPM e TotalNC
[19](#_Toc166238284)

**Figura 17:** Heatmaps comparando as correlações de Pearson na presença
e ausência de incêndio [20](#_Toc166238285)

**Figura 18:** Gráfico de dispersão entre Pressure\[hPa\] e TotalNC
[20](#_Toc166238286)

**Figura 19:** Gráfico de dispersão entre Pressure\[hPa\] e
Temperature\[C\] [21](#_Toc166238287)

**Figura 20:** Gráficos QQ-plot dos atributos Raw Ethanol e
Temperature\[C\] [22](#_Toc166238288)

**Figura 21:** Regressão linear entre os atributos TotalPM e TotalNC
[23](#_Toc166238289)

**Figura 22:** Regressão linear entre os atributos Humidity\[%\] e
Pressure\[hPa\] [23](#_Toc166238290)

**Figura 23:** Matriz de confusão do modelo florestas randômicas
[25](#_Toc166238291)

LISTA DE TABELAS

[**Tabela 1:** Descrição estatística do banco de dados
[9](#_Toc166259878)](#_Toc166259878)

[**Tabela 2:** Frequências e percentuais do atributo \'TemperatureCat\'
[10](#_Toc166259879)](#_Toc166259879)

[**Tabela 3:** Frequências e percentuais do atributo \'HumidityCat\'
[10](#_Toc166259880)](#_Toc166259880)

[**Tabela 4:** Frequências e percentuais do atributo \'SmokeDetec\'
[10](#_Toc166259881)](#_Toc166259881)

[**Tabela 5:** Média e desvio padrão para cada valor de 'Fire Alarm'
[10](#_Toc166259882)](#_Toc166259882)

[**Tabela 6:** Tabela cruzada - TemperatureCat e SmokeDetec
[16](#_Toc166259883)](#_Toc166259883)

[**Tabela 7:** Tabela cruzada - HumidityCat e SmokeDetec
[16](#_Toc166259884)](#_Toc166259884)

[**Tabela 8:** Resultados da validação cruzada
[25](#_Toc166259885)](#_Toc166259885)

SUMÁRIO

[1 IntroDUÇÃO [5](#introdução)](#introdução)

[2 Desenvolvimento [6](#desenvolvimento)](#desenvolvimento)

[2.1 ObjetO DE Estudo [6](#objeto-de-estudo)](#objeto-de-estudo)

[2.2 Atributos [7](#atributos)](#atributos)

[2.3 Metodologia [8](#metodologia)](#metodologia)

[2.4 PRÉ-PROCESSAMENTO DOS DADOS
[8](#pré-processamento-dos-dados)](#pré-processamento-dos-dados)

[2.5 Análise estatística descritiva
[9](#análise-estatística-descritiva)](#análise-estatística-descritiva)

[2.5.1 ANÁLISE DE MEDIDAS [9](#análise-de-medidas)](#análise-de-medidas)

[2.5.2 ANÁLISE GRÁFICA [11](#análise-gráfica)](#análise-gráfica)

[2.6 Análise estatística inferencial
[15](#análise-estatística-inferencial)](#análise-estatística-inferencial)

[2.6.1 ANÁLISE BIVARIADA [15](#análise-bivariada)](#análise-bivariada)

[2.6.2 INFERÊNCIA ESTATÍSTICA
[21](#inferência-estatística)](#inferência-estatística)

[2.7 aplicação de técnicas de machine learning
[24](#aplicação-de-técnicas-de-machine-learning)](#aplicação-de-técnicas-de-machine-learning)

[2.7.1 TRANSFORMAÇÃO DOS DADOS
[24](#transformação-dos-dados)](#transformação-dos-dados)

[2.7.2 VALIDAÇÃO CRUZADA [24](#validação-cruzada)](#validação-cruzada)

[3 Conclusão [26](#conclusão)](#conclusão)

[REFERÊNCIAS BIBLIOGRÁFICAS
[27](#referências-bibliográficas)](#referências-bibliográficas)

# IntroDUÇÃO

No mundo atual bilhões de dados são gerados diariamente por aplicativos,
redes sociais, pesquisas na web, dispositivos de Internet das Coisas
(IOT), entre outros. A análise desse grande volume de dados, que são
variados e gerados velozmente, pode fornecer insights importantes sobre
como tornar os serviços mais personalizáveis, aperfeiçoar as estratégias
de marketing, gerar previsões em diversos contextos, como o risco de um
indivíduo desenvolver determinado tipo de doença, além otimizar o
funcionamento de diversos aparelhos, desde geladeiras até sensores.

No presente estudo vamos analisar os dados gerados por sensores de um
detector de fumaça, a fim de encontrar relações entre os dados que ele
gera e determinar técnicas que otimizem o seu processamento, reduzindo a
ocorrência de falhas, a fim de torná-lo mais preciso e eficaz no
controle de incêndios. Para isso serão utilizadas técnicas de ciência de
dados, como análises estatísticas, análises gráficas e aplicação de
algoritmos de machine learning, utilizando o Google Colab e bibliotecas
da linguagem de programação Python, como numpy, scikit learn, scipy,
pingouin, seaborn e matplotlib. Essa análise será feita com base em
dados disponibilizados no Kaggle sobre um dispositivo IOT composto por
sensores integrados para coleta de dados sobre a qualidade do ar em um
determinado ambiente.

Essa análise possibilita a aquisição de conhecimentos fundamentais para
análise de dados, como a estatística descritiva e inferencial, que são
fundamentais para observar a presença de padrões e correlações entre os
dados, possibilitando a compreensão dos fatores que levam a ocorrência
de fenômenos e a possibilidade de executar previsões sobre situações
futuras com base no comportamento do presente momento. Isso tem um
grande impacto positivo para a sociedade, tendo em vista que no caso em
questão, por exemplo, as previsões corretas podem evitar perdas humanas,
animais e materiais.

# Desenvolvimento

Nesse capítulo serão descritos o objeto de estudo, os dados analisados,
os métodos aplicados na análise e os resultados obtidos.

## ObjetO DE Estudo

O objeto de estudo desse trabalho é um banco de dados disponibilizado na
plataforma Kaggle, que é formado por dados coletados pelo engenheiro de
software Stefan Blattmann através da integração de sensores que captam
informações sobre as condições do ar do ambiente. Esses sensores são o
Sensirion SPS30, para fornecer dados sobre a dimensão e o número de
partículas em suspensão no ar, o sensor BME688 para analisar a
temperatura, a umidade e a concentração de compostos orgânicos voláteis
(VOC), o sensor SHT31 também para medir a temperatura e a umidade, os
sensores BMP390 e BMP388 para obter o valor da pressão do ar e o sensor
SPG30 para auxiliar na quantificação da concentração de gás VOC.

Esses sensores foram integrados utilizando um Arduino Pro Nicla Sense
ME, que é responsável por realizar o processamento dos dados obtidos,
combinando aqueles que são medidos por mais de um sensor, a fim de
aumentar o nível de confiança e, utilizando técnicas de inteligência
artificial, determinar se existe um incêndio em curso.

Esse banco de dados foi preenchido a partir da análise de vários
contextos e lugares diferentes, como interiores e exteriores em
condições normais, lareiras, incêndios a gás dentro de um ambiente
interior, churrasqueiras à madeira, carvão e gás em ambientes externos,
alta umidade exterior, entre outros. Assim, foram coletadas 62630
amostras, que não possuem dados faltantes e são únicas, ou seja não
existem linhas repetidas, já que não há fallback para o sensor Sensirion
SPS30.

Blattmann tinha como principal objetivo aumentar a precisão dos
dispositivos IOT de detecção de fumaça, aumentando a taxa de verdadeiros
positivos detectados, evitando falsos alarmes em situações como comida
queimada, alta umidade, vapor, acúmulo de poeira no sensor e utilização
de compostos químicos.

## Atributos

Os atributos do banco de dados são:

-   Atributos Previsores:

    -   Quantitativos Discretos:

        -   Unnamed: 0: Índice das amostras.

        -   UTC: Tempo em segundos UTC, que se refere ao momento em que
            cada amostra foi coletada.

        -   TVOC\[ppb\]: Concentração total de Compostos Voláteis
            Orgânicos (VOC) medida em partes por bilhão.

        -   eCO2\[ppm\]: Concentração equivalente de CO2, medida em
            partes por milhão.

        -   Raw H2: Hidrogênio molecular bruto, não compensado.

        -   Raw Ethanol: Etanol gasoso bruto.

        -   CNT: Contador de amostras.

    -   Quantitativos Contínuos:

        -   Temperature\[C\]: Temperatura do ar em graus Celsius.

        -   Humidity\[%\]: Porcentagem de umidade do ar.

        -   Pressure\[hPa\]: Pressão do ar em hectopascal.

        -   PM1.0: Material particulado com tamanho inferior a 1,0µm.

        -   PM2.5: Material particulado com tamanho entre 1,0µm e 2,5µm.

        -   NC0.5: Concentração numérica de material particulado de
            tamanho inferior a 0,5µm.

        -   NC1.0: Concentração numérica de material particulado de
            tamanho entre 0,5µm e 1,0µm.

        -   NC2.5: Concentração numérica de material particulado de
            tamanho entre 1,0µm e 2,5µm.

-   Atributo Meta:

    -   Quantitativo Discreto:

        -   Fire Alarm: Classifica a situação como incêndio, quando
            possui valor 1, caso contrário, seu valor é 0.

## Metodologia

A plataforma Google Colab foi utilizada para análise dos dados com a
linguagem de programação Python, com auxílio das bibliotecas pandas,
seaborn, matplotlib, math, numpy, scipy, plotly, pingouin e scikit
learn. A partir dessas ferramentas, foi possível fazer uma análise
estatística dos dados, através da obtenção de medidas de posição e
variação, como frequência, média, moda, mediana, desvio padrão,
variância e percentis. Além disso, foi realizada uma análise gráfica da
distribuição da frequência dos atributos e da correlação entre alguns
deles, através da criação de histogramas, boxplots, heatmaps e gráficos
de dispersão. Também foi desenvolvida uma inferência estatística sobre o
banco de dados e uma análise bivariada de seus atributos, a fim de
compreender a relação entre eles.

Ademais, foram utilizadas técnicas de machine learning para melhor
processamento dos dados, com utilização da técnica de validação cruzada
para seleção de um modelo capaz de realizar predições futuras quanto a
classificação de eventos cotidianos diversos, com o objetivo de elevar a
precisão dessas classificações e evitar o acionamento do sensor de
fumaça em casos negativos.

## PRÉ-PROCESSAMENTO DOS DADOS

Primeiramente, são extraídas informações do banco de dados, que mostram
a presença de 62630 entradas, sendo que nenhuma delas possui valores
nulos ou duplicados. Além disso, 8 atributos são do tipo 'int64' e 8 do
tipo 'float64'.

O próximo passo é avaliar a redundância de alguns atributos, como UTC,
que quando é convertido de tempo em segundos UTC para data, indica que
as amostras foram coletadas no mesmo ano, no mesmo mês e em um pequeno
intervalo de dias, dessa forma, esse atributo não tem influência na
detecção de incêndios, já que se tratam de eventos simulados, não
agregando possíveis informações como o mês de maior incidência de
incêndios.

Também foi avaliado o atributo Unnamed:0, que é apenas um índice para as
amostras, que possui um valor diferente para cada uma delas, não tendo
nenhum significado específico. Ademais, o atributo CNT também não possui
relevância, já que apenas informa o número de amostras coletadas,
possuindo 24994 valores únicos. Sendo assim, esses três atributos não
devem ser utilizados nesta análise.

Por outro lado, novas variáveis podem ser criadas para categorizar
atributos numéricos como Temperature\[C\], Humidity\[%\] e Fire Alarm.
Um dos atributos adicionado ao banco de dados é TemperatureCat, que
categoriza a temperatura com muito baixa abaixo de 0°C, baixa entre 0°C
e 10°C, moderada entre 10°C e 20°C, alta entre 20°C e 30°C e muito alta
acima de 30°C, considerando as categorias de temperatura da Alemanha,
país em que foram coletados os dados. Também foi criado o atributo
HumidityCat para classificar a umidade do ambiente com baixa abaixo de
30%, moderada entre 30% e 60% e alta quando superior a 60%. Por último,
para determinar a detecção ou não de um incêndio, foi criado o atributo
SmokeDetec que recebe o valor 'não' quando a variável Fire Alarm for 0 e
'sim' quando for 1.

## Análise estatística descritiva

###  ANÁLISE DE MEDIDAS

Após o pré-processamento dos dados, é feita uma descrição estatística
dos atributos quantitativos, que resulta na *Tabela 1*.

[]{#_Toc166259878 .anchor}**Tabela 1:** Descrição estatística do banco
de dados

![Interface gráfica do usuário Descrição gerada automaticamente com
confiança baixa](imagens/media/image1.png){width="6.299305555555556in"
height="1.7722222222222221in"}

Fonte: ARAÚJO, Carolina.

Através dos dados dessas tabelas é possível verificar as medidas de
posição e de variação de cada atributo, sendo elas a frequência total, a
média, o desvio padrão, o valor mínimo, o valor do primeiro quartil, a
mediana, o valor do terceiro quartil e o valor máximo, respectivamente.

Também foram obtidas as frequências e percentuais dos atributos
qualitativos:

[]{#_Toc166259879 .anchor}**Tabela 2:** Frequências e percentuais do
atributo \'TemperatureCat\'

![](imagens/media/image2.emf)

Fonte: ARAÚJO, Carolina.

[]{#_Toc166259880 .anchor}**Tabela 3:** Frequências e percentuais do
atributo \'HumidityCat\'

![](imagens/media/image3.emf)

Fonte: ARAÚJO, Carolina.

[]{#_Toc166259881 .anchor}**Tabela 4:** Frequências e percentuais do
atributo \'SmokeDetec\'

![](imagens/media/image4.emf)

Fonte: ARAÚJO, Carolina.

Ademais, também é relevante analisar o intervalo médio (média do
atributo ± desvio padrão do atributo) dos atributos para cada valor do
atributo alvo Fire Alarm:

[]{#_Toc166259882 .anchor}**Tabela 5:** Média e desvio padrão para cada
valor de 'Fire Alarm'

![](imagens/media/image5.emf)

Fonte: ARAÚJO, Carolina.

### ANÁLISE GRÁFICA

Plotar gráficos para analisar a distribuição da frequência de cada
atributo é importante para obter mais informações sobre os dados, como o
intervalo de concentração e a verificação da existência de outliers em
atributos quantitativos. Para isso, podem ser utilizados gráficos de
densidade e boxplots para os atributos quantitativos e gráficos de barra
para os atributos qualitativos.

Sendo assim, inicialmente ao analisar o gráfico da frequência da
temperatura é possível observar que seus dados não possuem distribuição
normal e estão mais concentrados à esquerda da média, 15,97°C, com
desvio padrão de 14,36°C, caracterizando uma assimetria positiva.

[]{#_Toc166238269 .anchor}**Figura 1:** Gráfico de densidade do atributo
\'Temperature\[C\]\'

![](imagens/media/image6.png){width="3.543307086614173in"
height="2.3622047244094486in"}

Fonte: ARAÚJO, Carolina.

Já o gráfico de densidade do atributo Humidity\[%\] mostra uma grande
concentração em torno da média, com uma assimetria positiva, que indica
que os valores do percentual de umidade coletados concentram-se em torno
de 48,54%, com mediana de 50,15% e desvio padrão de 8,86%. Esse atributo
não possui uma distribuição normal, já que apresenta densidades
heterogêneas.

[]{#_Toc166238270 .anchor}**Figura 2:** Gráfico de densidade do atributo
\'Humidity\[%\]\'

![](imagens/media/image7.png){width="3.543307086614173in"
height="2.3622036307961505in"}

Fonte: ARAÚJO, Carolina.

As densidades de TVOC\[ppb\] são ainda mais heterogêneas, possuindo 75%
de seus dados abaixo de 1189,00 ppb, mas também com presença de dados em
um intervalo muito superior, em torno de 60000 ppb. Essa variação
depende do contexto em que ocorre a medição, em caso de incêndio seu
intervalo médio é de 882,01±548,61 ppb, porém quando não há incêndio
esse intervalo é de 4596,59±14255,58 ppb. Como a média geral é 1942,06
ppb, existe uma grande assimetria positiva. Isso também ocorre com o
atributo eCO2\[ppm\], que possui média de 670,02 ppm e 85% de
concentração abaixo de 552 ppm.

[]{#_Toc166238271 .anchor}**Figura 3:** Gráfico de densidade do atributo
\'TVOC\[ppb\]'

![](imagens/media/image8.png){width="3.46875in"
height="2.3618055555555557in"}

Fonte: ARAÚJO, Carolina.

[]{#_Toc166238272 .anchor}**Figura 4:** Gráfico de densidade do atributo
\'eCO2\[ppm\]\'

![](imagens/media/image9.png){width="3.3958333333333335in"
height="2.3618055555555557in"}

Fonte: ARAÚJO, Carolina.

Os atributos Raw H2 e Raw Ethanol, também possuem assimetria negativa,
já que suas densidades estão concentradas a esquerda de suas médias.
Além disso, a falta de uniformidade na disposição de suas densidades faz
com que não possuam distribuição normal.

[]{#_Toc166238273 .anchor}**Figura 5:** Gráfico de densidade do atributo
\'Raw H2\'

![](imagens/media/image10.png){width="3.543307086614173in"
height="2.3622036307961505in"}

Fonte: ARAÚJO, Carolina.

[]{#_Toc166238274 .anchor}**Figura 6:** Gráfico de densidade do atributo
\'Raw Ethanol\'

![](imagens/media/image11.png){width="3.543307086614173in"
height="2.3622036307961505in"}

Fonte: ARAÚJO, Carolina.

O atributo Pressure\[hPa\] possui grande discrepância na distribuição de
suas densidades, apesar do baixo coeficiente de variabilidade definido
como 0,14%. Existem uma pequena concentração no intervalo entre 930hPa e
932hPa, porém a maior concentração ocorre a direita da média 938,63hPa,
sendo que 50% dos dados estão abaixo de 938,77, que é um valor acima da
média, caracterizando uma assimetria negativa, sem distribuição normal.

[]{#_Toc166238275 .anchor}**Figura 7:** Gráfico de densidade do atributo
\'Pressure\[hPa\]\'

![](imagens/media/image12.png){width="3.543307086614173in"
height="2.3622036307961505in"}

Fonte: ARAÚJO, Carolina.

Os atributos TotalPM e TotalNC apresentam 85% dos dados abaixo de 4,59 e
17,99, respectivamente, estando muito abaixo de suas médias, que são
285,06 e 775,10. Além disso, apresentam grande variabilidade, já que
seus coeficientes de variação estão em torno de 1000%.

[]{#_Toc166238276 .anchor}**Figura 8:** Gráfico de densidade do atributo
\'TotalNC\'

![Gráfico, Histograma Descrição gerada
automaticamente](imagens/media/image13.png){width="3.543307086614173in"
height="2.3622047244094486in"}

Fonte: ARAÚJO, Carolina.

[]{#_Toc166238277 .anchor}**Figura 9:** Gráfico de densidade do atributo
\'TotalPM\'

![Gráfico, Histograma Descrição gerada
automaticamente](imagens/media/image14.png){width="3.543307086614173in"
height="2.3622047244094486in"}

Fonte: ARAÚJO, Carolina.

Também é possível visualizar a distribuição dos quartis de cada atributo
quantitativo, as assimetrias e a presença de valores extremos,
utilizando boxplots. Eles foram plotados em diferentes escalas para
possibilitar uma melhor observação, sendo elas as escalas logarítmica,
logarítmica simétrica e linear.

[]{#_Toc166238278 .anchor}**Figura 10:** Boxplots dos atributos
quantitativos

![Diagrama, Gráfico de caixa estreita Descrição gerada
automaticamente](imagens/media/image15.png){width="5.5204286964129485in"
height="3.3125in"}

Fonte: ARAÚJO, Carolina.

Quanto aos atributos qualitativos, TemperatureCat, HumidityCat,
SmokeDetec, pode-se extrair informações quanto aos principais intervalos
de concentração dos dados através da categorização dos atributos
Temperature\[C\], Humidity\[%\] e Fire Alarm, respectivamente.

O atributo Temperature\[C\] possui a maioria de seus valores
caracterizados como temperatura alta, ou seja, entre 20°C e 30°C, com
percentual de 46,68%, e a minoria é composta por 4,19% de temperaturas
acima de 30°C, que são muito altas. Já a variável Humidity\[%\] tem
maior frequência de valores de umidade moderada, entre 30% e 60%, com
percentual de 92,44%. Por fim, o atributo Fire Alarm foi caracterizado
pela presença ou ausência de incêndio, possibilitando a conclusão de que
a maioria dos dados coletados indica 'Sim' para presença de incêndio,
com percentual de 71,46% e frequência de 44757.

[]{#_Toc166238279 .anchor}**Figura 11:** Frequências dos atributos
categóricos

![](imagens/media/image16.png){width="6.3381944444444445in"
height="2.2291666666666665in"}

Fonte: ARAÚJO, Carolina.

## Análise estatística inferencial

### ANÁLISE BIVARIADA

Nesta etapa é necessário analisar a relação entre as variáveis para
procurar associações que justifiquem o fenômeno estudado. Inicialmente,
foram criadas tabelas cruzadas para comparar os atributos qualitativos
em pares.

A primeira comparação é entre o atributo TemperatureCat, que categoriza
as temperaturas, e o atributo SmokeDetec, que determina a existência de
um incêndio. Através dessa análise, é possível observar que as maiores
probabilidades por categoria de temperatura de haver um incêndio ocorrem
quando ela é alta, entre 20°C e 30°C, ou baixa, entre 0°C e 10°C, com
73,7% e 79,8% de probabilidade, respectivamente.

Embora, a porcentagem para o caso positivo quando a temperatura é muito
baixa seja de 81,3%, deve ser levado em consideração o fato de que o
caso negativo só foi obtido nessa condição de temperatura em 2247
amostras ao contrário das amostras positivas que somam 9777, sendo no
total 3,6% do total de amostras contra 15,6%, respectivamente. Já um
ambiente com temperatura muita alta, que apresenta a menor porcentagem
do total de amostras, tem 65,5% de chance de não ser incêndio. É
importante salientar que como os eventos foram simulados, pode haver um
desbalanceamento na coleta dos dados, já que apenas 28,5% dos dados
avaliam situações em que não há incêndio.

Já a comparação entre os atributos HumidityCat e SmokeDetec mostrou que
a maioria das amostras foi coletada em ambientes com umidade entre 30% e
60%, categorizada como moderada, representando 92% do total. Dentro
desse intervalo a probabilidade de o evento em questão ser um incêndio é
de 74,3%. Do total de 5,9% de amostras na categoria baixa, a
probabilidade do caso negativo é de 76,4%. Por fim, a categoria alta,
com umidade acima de 60%, representa apenas 1,7% do total analisado,
sendo que a probabilidade é de 79,6% de ser um incêndio nessa condição.

[]{#_Toc166259883 .anchor}**Tabela 6:** Tabela cruzada - TemperatureCat
e SmokeDetec

![Tabela Descrição gerada
automaticamente](imagens/media/image17.png){width="2.716535433070866in"
height="2.3037762467191603in"}

Fonte: ARAÚJO, Carolina.

[]{#_Toc166259884 .anchor}**Tabela 7:** Tabela cruzada - HumidityCat e
SmokeDetec

![Tabela Descrição gerada
automaticamente](imagens/media/image18.png){width="2.716535433070866in"
height="1.8984284776902887in"}

Fonte: ARAÚJO, Carolina.

A relação entre os atributos quantitativos foi calculada através do
coeficiente de Pearson, que possui valor próximo de 1 para uma forte
correlação positiva, próximo de 0 para indicar que não há relação entre
as variáveis e próximo de -1 para indicar uma forte relação inversa
entre elas. Foram plotados gráficos de calor, heatmaps, para observação
dessas relações, tanto de forma geral, quanto de forma individual, para
análise separada da força das relações entre as variáveis na presença ou
ausência de incêndio.

[]{#_Toc166238280 .anchor}**Figura 12:** Heatmap de correlações de
Pearson entre os atributos

![](imagens/media/image19.png){width="6.197916666666667in"
height="4.581170166229222in"}

Fonte: ARAÚJO, Carolina.

No heatmap de correlações gerais é possível observar que a correlação
mais forte existente é entre os atributos referentes a umidade e a
pressão do ambiente, que possui valor de 0,69. Isso é justificado pelo
fato de que o aumento da umidade provoca o aumento da quantidade de
vapor d'água no ambiente, gerando, consequentemente, uma elevação da
pressão de vapor, que é uma das componentes da pressão total do ambiente
medida pelo atributo Pressure\[hPa\]. Na *Figura 13* é possível observar
um gráfico de dispersão da relação dessas variáveis.

[]{#_Toc166238281 .anchor}**Figura 13:** Gráfico de dispersão dos
atributos Humidity\[%\] e Pressure\[hPa\]

![](imagens/media/image20.png){width="4.330708661417323in"
height="2.7757403762029744in"}

Fonte: ARAÚJO, Carolina.

Outra forte correlação negativa, com valor -0,67, ocorre entre os
atributos TVOC\[ppb\] e Raw Ethanol, que pode ser explicada pela
degradação do etanol na atmosfera, relacionado a diminuição do valor de
Raw Ethanol, que fornece matéria-prima para geração de mais compostos
orgânicos voláteis, aumentando a concentração indicada pelo atributo
TVOC\[ppb\]. A *Figura 14* apresenta o gráfico de dispersão que
visibiliza essa relação.

[]{#_Toc166238282 .anchor}**Figura 14:** Gráfico de dispersão dos
atributos TVOC\[ppb\] e Raw Ethanol

![](imagens/media/image21.png){width="4.330708661417323in"
height="2.7996227034120733in"}

Fonte: ARAÚJO, Carolina.

Ademais, a correlação entre os atributos eCO2\[ppm\] e Raw H2 também é
importante, tendo valor de -0,68. Isso deve ao fato de que o hidrogênio
molecular possui baixa densidade quando comparado aos outras gases que
compõem a atmosfera, o que faz com que ele flutue em direção ao espaço,
além de não ser produzido em grandes quantidades. Esses fatores
contribuem para que sua concentração seja baixa, em oposição ao que
ocorre com o CO2, que é produto da combustão. Na *Figura 15* é possível
observar essa relação.

[]{#_Toc166238283 .anchor}**Figura 15:** Gráfico de dispersão dos
atributos Raw H2 e eCO2\[ppm\]

![](imagens/media/image22.png){width="4.05511811023622in"
height="2.52707239720035in"}

Fonte: ARAÚJO, Carolina.

Por último, a correlação entre TotalPM e TotalNC é a mais forte dentre
os atributos, sendo praticamente perfeita, com valor de 0,98. Isso
ocorre porque o atributo TotalNC é calculado com base nos valores de
TotalPM, indicando a concentração de material particulado no ambiente.

[]{#_Toc166238284 .anchor}**Figura 16:** Gráfico de dispersão entre
TotalPM e TotalNC

![Gráfico, Histograma Descrição gerada
automaticamente](imagens/media/image23.png){width="4.05511811023622in"
height="2.5053313648293964in"}

Fonte: ARAÚJO, Carolina.

Na avaliação dos heatmaps que analisam separadamente as correlações
entre os atributos na presença ou ausência de incêndio, é possível notar
que existem grandes variações.

[]{#_Toc166238285 .anchor}**Figura 17:** Heatmaps comparando as
correlações de Pearson na presença e ausência de incêndio

![](imagens/media/image24.png){width="6.290972222222222in"
height="3.1395833333333334in"}

Fonte: ARAÚJO, Carolina.

A maioria dos atributos, por exemplo, tem grande perda na força da
correlação com os atributos TotalPM e TotalNC na presença de incêndio,
passando a ser uma relação quase inexistente, com exceção apenas do
atributo Pressure\[Hpa\], que possui uma fraca correlação negativa. Na
*Figura 18* será visibilizada a relação entre Pressure\[hPa\] e TotalNC.

[]{#_Toc166238286 .anchor}**Figura 18:** Gráfico de dispersão entre
Pressure\[hPa\] e TotalNC

![](imagens/media/image23.png){width="4.330708661417323in"
height="2.6887084426946632in"}

Fonte: ARAÚJO, Carolina.

Por fim, a presença de incêndio também revela uma fraca correlação
negativa entre os atributos Pressure\[hPa\] e Teperature\[C\], que é
quase inexistente na ausência de incêndio. Essa pequena variação do
coeficiente de Pearson ocorre porque o ar atmosférico, quando aquecido
na presença de incêndio, passa a ter um maior coeficiente de
compressibilidade, o que indica que ele passa a ter um comportamento
mais próximo de um gás ideal, que estabelece uma relação entre
temperatura e pressão.

[]{#_Toc166238287 .anchor}**Figura 19:** Gráfico de dispersão entre
Pressure\[hPa\] e Temperature\[C\]

![Gráfico Descrição gerada
automaticamente](imagens/media/image25.png){width="4.330708661417323in"
height="2.6775207786526685in"}

Fonte: ARAÚJO, Carolina.

### INFERÊNCIA ESTATÍSTICA

Para aplicar a inferência estatística ao banco de dados, inicialmente é
necessário executar o teste de normalidade nos atributos, para verificar
se algum deles possui distribuição normal, para posterior execução dos
possíveis testes. Para essa etapa será atribuída um nível de confiança
de 95% para as amostras, tendo em vista que foi empregada uma integração
de sensores para garantir a confiabilidade dos dados coletados.

A execução do teste de normalidade no banco de dados e nos subgrupos
definidos pela presença ou ausência de incêndio retornou um p-valor de 0
para todos os atributos, indicando que a hipótese nula é rejeitada e que
em nenhum dos contextos existe um atributo com distribuição normal. Como
foi observado anteriormente nos gráficos de densidade e boxplots,
existem muitas assimetrias nas distribuições das

densidades e muitos valores extremos em alguns atributos que justificam
esse resultado.

Na *Figura 20* foram plotados gráficos do tipo QQ-plot para demonstrar
que não há distribuição normal.

[]{#_Toc166238288 .anchor}**Figura 20:** Gráficos QQ-plot dos atributos
Raw Ethanol e Temperature\[C\]

![](imagens/media/image26.png){width="5.118110236220472in"
height="2.302579833770779in"}

Fonte: ARAÚJO, Carolina.

Outro teste executado foi o teste de homoscedasticidade no atributo
Pressure\[hPa\] para verificar se a variância dos dados é a mesma dentro
dos subgrupos de presença ou ausência de incêndio. O p-valor usando o
método de Bartlett foi 8,8×10^-19^ e 0,0 usando o método de Levene. Isso
significa que a hipótese nula é rejeitada e a variância do atributo
Pressure\[hPa\] não é constante.

Ademais, o teste qui-quadrado foi aplicado inicialmente para as
variáveis TemperatureCat e SmokeDetec para verificar se existe alguma
relação entre elas. O p-valor retornado por todos os tipos de teste foi
de 0,0, o que indica que a hipótese nula é rejeitada e que existe uma
associação entre as categorias de temperatura e a presença ou não de
incêndio. Esse teste também foi aplicado para os atributos HumidityCat e
SmokeDetec, retornando o mesmo p-valor igual a 0,0, provando a
existência de uma dependência entre eles.

Em seguida, foram realizados os testes de correlação e regressão em três
conjuntos de atributos. O primeiro é composto pelas variáveis TotalPM e
TotalNC, que apresentam coeficiente de Pearson igual a 0,97332 com
p-valor de 0,0 e coeficiente de Spearman igual a 0,99952 com p-valor
também igual a 0, o que determina a rejeição da hipótese nula e
aceitação da existência de uma correlação entre os atributos. O teste de
regressão com essas variáveis retornou a equação linear:

Y = 2,39X + 94,51 (R^2^ = 0,95), sendo que Y corresponde ao atributo
TotalNC e X a TotalPM. Essa equação foi plotada em cima do gráfico de
dispersão dessas variáveis na *Figura 21*.

[]{#_Toc166238289 .anchor}**Figura 21:** Regressão linear entre os
atributos TotalPM e TotalNC

![](imagens/media/image27.png){width="3.7401574803149606in"
height="2.805015310586177in"}

Fonte: ARAÚJO, Carolina.

Esses testes também foram aplicados às variáveis Humidity\[%\] e
Pressure\[hPa\], retornando um coeficiente de Pearson igual a 0,69461 e
coeficiente de Spearman igual a 0,5558, ambos com p-valor igual a 0,
indicando a presença de correlação entre elas. O teste de regressão
forneceu os coeficientes para determinar a equação: Y = 0,10X + 933,56
(R^2^ = 0,48), com Y igual a Pressure\[hPa\] e X igual a Humidity\[%\].

[]{#_Toc166238290 .anchor}**Figura 22:** Regressão linear entre os
atributos Humidity\[%\] e Pressure\[hPa\]

![Gráfico, Gráfico de linhas Descrição gerada
automaticamente](imagens/media/image28.png){width="3.7401574803149606in"
height="2.805015310586177in"}

Fonte: ARAÚJO, Carolina.

Por fim, utilizando os atributos Raw H2, eCO2, Raw Ethanol, TotalNC,
TotalPM e TVOC\[ppb\], referentes às condições do ar do ambiente, a
aplicação dos teste de regressão resultou em p-valores muito baixos e
próximos ou iguais a 0, indicando a existência de uma relação de
dependência entre os atributos, que é definida pela equação linear: Y =
-5,44X~1~ + 0,33X~2~ -- 4,34X~3~ + 1,11X~5~ -- 2,00X~6~ + 157537,3 (R^2^
= 0,62), sendo que Y é TVOC\[ppb\], X~1~ é Raw H2, X~2~ é eCO2, X~3~ é
Raw Ethanol, X~4~ é TotalNC e X~5~ é TotalPM.

## aplicação de técnicas de machine learning

### TRANSFORMAÇÃO DOS DADOS

Para aplicar técnicas de machine learning e realizar futuras previsões
sobre a existência ou não de um incêndio em curso de acordo com os dados
coletados pelos sensores é necessário fazer um pré-processamento dos
dados. A parte inicial foi citada anteriormente, sendo o processo de
exclusão dos atributos redundantes e avaliação da presença de valores
nulos ou duplicados. Feito isso, é necessário escalonar os dados,
utilizando um pipeline com o método da padronização, Standard Scaler, e
aplicar o método Label Encoder para codificação dos atributos
categóricos.

Após executar as transformações nos dados, eles são divididos em
atributos previsores, X, e atributo alvo, Y, para um conjunto de
treinamento e um conjunto de validação, que são compostos por 80% do
conjunto total, equivalente a 50104 linhas, e 20%, correspondente a
12526 linhas, respectivamente.

### VALIDAÇÃO CRUZADA

Após o pré-processamento dos dados será utilizada a ferramenta de
validação cruzada, responsável por treinar e avaliar os modelos
selecionados para o número de subconjuntos definido por kfold. Nesse
caso serão utilizados os modelos regressões logística e linear, árvores
de decisão, florestas randômicas, KNN, Naive Bayes, SVM e redes neurais.
Esses modelos serão treinados e avaliados para 10 folds diferentes,

utilizando como score a acurácia, tendo em vista que o banco de dados
foi desenvolvido para aumentar a precisão das classificações de presença
ou ausência de incêndio. Foram calculadas as médias e os desvios padrões
para cada modelo utilizado, os resultados são descritos pela Tabela 8.

[]{#_Toc166259885 .anchor}**Tabela 8:** Resultados da validação cruzada

![](imagens/media/image29.png){width="3.1496062992125986in"
height="2.231306867891514in"}

Fonte: ARAÚJO, Carolina.

A maior acurácia média obtida foi de 0,999984 para o modelo florestas
randômicas (Random Forest), cuja implementação forneceu um relatório de
classificação com precisão e revocação iguais a 1,00 para ambas as
possibilidades de classificação. Plotando uma matriz de confusão,
exibida na *Figura 23*, é possível observar que 3534 situações foram
classificadas corretamente como ausência de incêndio, 1 situação foi
classificada incorretamente como ausência de incêndio e todas as 8991
situações de presença de incêndio foram classificadas corretamente, sem
nenhum erro.

[]{#_Toc166238291 .anchor}**Figura 23:** Matriz de confusão do modelo
florestas randômicas

![Gráfico, Gráfico de mapa de árvore Descrição gerada
automaticamente](imagens/media/image30.png){width="2.952755905511811in"
height="2.4606299212598426in"}

Fonte: ARAÚJO, Carolina.

# Conclusão

Com base no que foi discutido nessa análise, é possível concluir que os
dados sobre a temperatura, a umidade e a pressão do ar, a quantidade de
compostos orgânicos voláteis em suspensão, a concentração de CO2, a
quantidade de hidrogênio molecular e etanol e as quantidades e
concentrações de materiais particulados presentes no ambiente se
relacionam entre si e são fundamentais para determinação de um incêndio
em curso.

Além disso, foi possível obter diversos conhecimentos estatísticos
acerca de ferramentas como medidas de posição, medidas de variância,
distribuição das densidades e quartis, correlações e testes
estatísticos, assim como a forma de utilização da linguagem de
programação Python para execução dessa descrição estatística de uma base
de dados real.

Ademais, foi possível verificar que a aplicação de modelos de machine
learning é essencial na construção de dispositivos inteligentes para
detecção de fumaça, tendo em vista que elevam a precisão das
classificações com base nas variáveis do ar, elevando a taxa de acerto.
Uma alta precisão, como a que foi obtida, é muito importante para
acionar o dispositivo e controlar incêndios que poderiam gerar problemas
respiratórios, queimaduras, intoxicações, morte de humanos e animais,
perda de bens materiais e poluição atmosférica.

Portanto, conclui-se que a ciência de dados é uma importante ferramenta
para auxiliar os profissionais a compreenderem os mais variados
fenômenos e como cada variável contribui para a sua ocorrência. Também é
fundamental para criação de dispositivos inteligentes para auxiliar a
sociedade a solucionar grandes questões vitais.

###### REFERÊNCIAS BIBLIOGRÁFICAS {#referências-bibliográficas .unnumbered}

ARAÚJO, Carolina. **"Análise de um sensor de fumaça".** Google Colab.
Acesso em: 19 de abr. de 2024. Disponível em:
\<https://colab.research.google.com/drive/14kM-xWdNALWDRxMWg1nGXsG93W4kj9Pd?usp=sharing\>.

DEEP CONTRACTOR. **Smoke Detection Dataset**. Kaggle. Disponível em:
\<https://www.kaggle.com/datasets/deepcontractor/smoke-detection-dataset\>.
Acesso em: 19 de abr. de 2024.

BLATTMANN, Stefan. **Real-time Smoke Detection with AI based Sensor
Fusion**. Hackster.io. Disponível em:
\<https://www.hackster.io/stefanblattmann/real-time-smoke-detection-with-ai-based-sensor-fusion-1086e6#code\>.
Acesso em: 19 de abr. de 2024.

NEUTON.AI. **Using AI based sensor fusion for smoke detection**.
Neuton.AI. Disponível em:
\<https://neuton.ai/news/projects/86-using-ai-based-sensor-fusion-for-smoke-detection.html\>.
Acesso em: 19 de abr. de 2024.

GÉRON, Aurélien. *Mãos à obra: aprendizado de máquina com Scikit-Learn,
Keras e TensorFlow: conceitos, ferramentas e técnicas para a construção
de sistemas inteligentes. 2. ed*. Rio de Janeiro: Alta Books, 2021.

ZOUZA, Marcus. **Seu primeiro projeto de Machine Learning em Python:
Passo a passo**. Medium. Disponível em:
\<https://medium.com/blog-do-zouza/seu-primeiro-projeto-de-machine-learning-em-python-passo-a-passo-78c5f7bce22d\>.
Acesso em: 04 de maio de 2024.

Muzdadid, Hasib Al. **Fire Alarm Triggering Analysis (Accuracy 100%)**.
Kaggle. Disponível em:
\<https://www.kaggle.com/code/hasibalmuzdadid/fire-alarm-triggering-analysis-accuracy-100\>.
Acesso em: 04 de maio de 2024.

SAFESST. **Material Particulado**. Blog Safesst. Disponível em:
https://blog.safesst.com.br/material-particulado-2/. Acesso em: 06 de
maio de 2024.

ENVIRONMENTAL PROTECTION AGENCY (EPA). **What are Volatile Organic
Compounds (VOCs)?** Environmental Protection Agency. Disponível em:
https://www.epa.gov/indoor-air-quality-iaq/what-are-volatile-organic-compounds-vocs.
Acesso em: 06 de maio de 2024.
