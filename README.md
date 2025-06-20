# Análise do Impacto do Plano de Saúde na Saúde Subjetiva Utilizando Propensity Score Matching na PNS 2019

## 1. Resumo/Abstract



## 2. Introdução

O sistema de saúde brasileiro é caracterizado por sua dualidade, compreendendo o Sistema Único de Saúde (SUS), de caráter universal e público, e a saúde suplementar, predominantemente privada, que engloba os planos e seguros de saúde. Ambos os pilares desempenham funções cruciais na provisão de acesso e na garantia da saúde da população, embora com diferentes modelos de financiamento e acesso. A compreensão da dinâmica entre esses sistemas e seus impactos na percepção individual de saúde é fundamental para o planejamento e aprimoramento das políticas de saúde pública no país.

A saúde, em sua definição mais abrangente, transcende a mera ausência de doença, incorporando dimensões de bem-estar físico, mental e social. Nesse contexto, a saúde subjetiva emerge como um indicador de vital importância, uma vez que reflete a autoavaliação do indivíduo sobre seu próprio estado de saúde e bem-estar geral. Essa percepção pessoal, frequentemente influenciada por fatores além das condições clínicas objetivas, oferece insights valiosos sobre a qualidade de vida e a eficácia dos sistemas de saúde sob a ótica do cidadão. Para investigar essa complexa interação no contexto brasileiro, este estudo utiliza os dados da Pesquisa Nacional de Saúde (PNS) de 2019, uma fonte de informação robusta e representativa da população, que oferece um panorama detalhado das condições de saúde e acesso a serviços no país.

Diante do exposto, este estudo busca responder à seguinte questão de pesquisa: qual a influência da posse de um plano de saúde na percepção da saúde subjetiva de indivíduos no Brasil, considerando a heterogeneidade socioeconômica e demográfica da população? Para abordar essa questão, o objetivo geral é analisar a relação entre a posse de um plano de saúde e a saúde subjetiva da população brasileira, utilizando dados da PNS 2019 e técnicas de inferência causal.

Para alcançar este objetivo geral, foram estabelecidos os seguintes objetivos específicos:

- Caracterizar a distribuição da saúde subjetiva em grupos com e sem plano de saúde na amostra da PNS 2019.
- Identificar as principais covariáveis socioeconômicas e de saúde associadas tanto à posse de um plano de saúde quanto à saúde subjetiva.
- Empregar a metodologia de Propensity Score Matching (PSM) para balancear as covariáveis observadas entre os grupos com e sem plano de saúde, visando a obtenção de grupos comparáveis e a redução de vieses de seleção.
- Estimar o efeito da posse de um plano de saúde na saúde subjetiva por meio de um modelo de regressão ordinal, após a aplicação do balanceamento por PSM.

A relevância deste estudo reside em sua contribuição para a compreensão aprofundada dos determinantes da saúde da população brasileira. Ao aplicar métodos de inferência causal, como o Propensity Score Matching (PSM), este trabalho busca fornecer subsídios mais robustos sobre o impacto específico da posse de um plano de saúde na percepção da saúde subjetiva.

## 3. Referencial Teorico

A pesquisa em saúde pública no Brasil depende fundamentalmente da análise de dados complexos provenientes de inquéritos populacionais, como a Pesquisa Nacional de Saúde (PNS). A natureza observacional de muitos estudos nesse campo exige a aplicação de metodologias estatísticas avançadas para garantir a validade das inferências causais e a precisão das estimativas. A crescente disponibilidade de bases de dados abrangentes, aliada à necessidade de inferências robustas em cenários não-experimentais, demanda pesquisadores aptos a explorar as nuances metodológicas impostas pela busca por relações de causa e efeito em contextos não-controlados. Este estudo se insere nesse contexto, combinando a riqueza dos dados da PNS com técnicas avançadas como o Pareamento por Escore de Propensão (PSM) e a Regressão Logística Ordinal para aprofundar a compreensão sobre os determinantes da saúde subjetiva.

#### 3.1. Pesquisa Nacional de Saúde (PNS): Contexto e Relevância

A Pesquisa Nacional de Saúde (PNS) é um inquérito de base domiciliar de abrangência nacional, realizado pelo Instituto Brasileiro de Geografia e Estatística (IBGE) em parceria com o Ministério da Saúde, com periodicidade de aproximadamente cinco anos (edições em 2013 e 2019). Seu principal objetivo é produzir dados sobre o desempenho do sistema nacional de saúde e as condições de saúde da população brasileira. A PNS transcende a saúde estrita, coletando informações detalhadas sobre população, trabalho, educação, habitação, renda, despesas, consumo, administração pública, participação política e social, justiça, segurança e proteção social. Essa vasta gama de dados permite análises multifacetadas e a investigação de determinantes sociais da saúde, consolidando-a como uma ferramenta poderosa para a epidemiologia, políticas públicas e ciências sociais aplicadas à saúde. A PNS, portanto, não é apenas um inquérito de saúde, mas uma base de dados socioeconômica e de saúde integrada, capaz de subsidiar a compreensão holística dos fenômenos de saúde e doença, e de embasar políticas públicas que considerem múltiplos determinantes.

A metodologia da PNS é caracterizada por um desenho amostral complexo, que geralmente envolve amostragem por conglomerados em múltiplos estágios, fundamental para garantir a representatividade da população brasileira. O cálculo do tamanho da amostra considera a precisão desejada, os intervalos de confiança de 95%, o efeito do plano amostral (conglomerados), o número de domicílios selecionados e a taxa de não resposta. Para corrigir probabilidades de seleção desiguais e calibrar as estimativas para as populações totais conhecidas, são calculados pesos amostrais para os domicílios e seus residentes, ajustados também para a não resposta. A coleta de dados é baseada em questionários estruturados, com informações auto-referidas sobre saúde, satisfação do paciente e percepções. É crucial notar que o desenho amostral complexo impõe requisitos metodológicos rigorosos, pois ignorar os pesos amostrais e a estrutura de conglomerados pode levar a estimativas viesadas e inferências incorretas sobre a população brasileira, comprometendo a validade e a generalização dos resultados.

A PNS é uma fonte essencial para o monitoramento de doenças, comportamentos de risco, e acesso e uso de serviços de saúde, sendo primária para a identificação de padrões de doenças e custos de saúde, e para subsidiar o planejamento e a avaliação de políticas públicas de saúde. Ela transcende a mera coleta de dados, atuando como um instrumento de governança em saúde, cujos resultados influenciam práticas de cuidado médico e formulação de políticas públicas, permitindo uma tomada de decisão baseada em evidências em nível nacional.

No entanto, o uso dos dados da PNS apresenta desafios e oportunidades. A complexidade do desenho amostral exige softwares e métodos estatísticos específicos (e.g., pacotes survey e srvyr no R) para o cálculo correto de estimativas e variâncias, garantindo que a estrutura de conglomerados e os pesos amostrais sejam adequadamente considerados. A natureza auto-referida de alguns dados pode introduzir vieses de informação. Há também a necessidade de lidar com dados faltantes e outliers, problemas que, quando não abordados adequadamente (especialmente em estudos que utilizam regressão logística), podem comprometer a validade dos achados. Apesar desses desafios, a PNS oferece oportunidades substanciais, como sua representatividade nacional (permitindo a generalização dos achados), a riqueza de variáveis coletadas (possibilitando a investigação de relações causais complexas e o controle de múltiplos fatores de confusão), e a disponibilidade de dados em diferentes edições (permitindo análises de tendências temporais e avaliação do impacto de políticas a longo prazo). Contudo, persiste uma lacuna significativa na aplicação rigorosa de boas práticas metodológicas, indicando a necessidade de aprimorar a aplicação das metodologias estatísticas para explorar o potencial da PNS de forma mais robusta e confiável.

#### 3.2. Pareamento por Escore de Propensão (PSM): Fundamentos e Aplicação

O Pareamento por Escore de Propensão (PSM) é uma metodologia estatística quase-experimental fundamental para estimar o efeito de um tratamento, política ou intervenção em estudos observacionais, onde a randomização não é eticamente ou logisticamente viável. O PSM busca construir um grupo de controle artificial, emparelhando unidades tratadas com unidades não tratadas que possuem características observadas semelhantes, baseando-se no "escore de propensão" – a probabilidade condicional de uma unidade ser atribuída a um tratamento específico, dadas suas covariáveis observadas. Introduzido por Rosenbaum e Rubin (1983) e com contribuições de Heckman (1997), o PSM mimetiza a randomização ao balancear as covariáveis observadas entre grupos de tratamento e controle, buscando criar uma "pseudo-randomização" que permite atribuir diferenças de resultados ao tratamento de forma mais confiável, superando o viés de seleção inerente a dados não randomizados.

Para que o PSM produza estimativas válidas, dois pressupostos fundamentais devem ser satisfeitos: a Hipótese de Independência Condicional (CIA – Conditional Independence Assumption ou Ignorabilidade Forte), que afirma que, após ajustar por um conjunto relevante de covariáveis observadas, os desfechos potenciais são independentes da atribuição ao tratamento; e a Hipótese de Suporte Comum (Overlap or Common Support), que garante que, para cada valor das covariáveis observadas, haja uma probabilidade positiva de ser tratado e não tratado, assegurando sobreposição substancial nas distribuições dos escores de propensão entre os grupos. O pressuposto da independência condicional é infelizmente não testável com dados observacionais, implicando que a validade das inferências causais baseadas em PSM sempre conterá um grau de incerteza relacionado a vieses não observados, tornando a realização e o relato de testes de sensibilidade uma prática indispensável.

A aplicação do PSM envolve a identificação de unidades tratadas e não tratadas, e a coleta de características relevantes para a participação no tratamento e o desfecho. A Estimação do Escore de Propensão é geralmente realizada por meio de regressão logística (o método mais comum) ou probit, onde a variável dependente é binária (tratado/não tratado). O objetivo principal dessa estimação é balancear as covariáveis entre os grupos. Após a estimação, é crucial a Restrição ao Suporte Comum, descartando unidades fora dele. A escolha do algoritmo de pareamento (e.g., nearest neighbor, caliper, kernel) e a Avaliação do Balanço das Covariáveis (por meio de diferenças padronizadas e gráficos) são etapas cruciais e frequentemente iterativas; se o balanço não for adequado, é necessário refinar o procedimento. Finalmente, calcula-se a diferença média nos desfechos entre as unidades tratadas e seus pares de controle.

O PSM oferece a vantagem principal de reduzir o viés de seleção ao criar grupos comparáveis em características observadas, permitindo inferência causal em estudos observacionais onde RCTs (Ensaios Clínicos Randomizados) são inviáveis. Ele também reduz a dimensionalidade ao resumir múltiplas covariáveis em um único escore e diminui a dependência de modelagem específica do desfecho. Além disso, ao utilizar dados do "mundo real", pode aumentar a validade externa dos resultados. Contudo, suas limitações incluem o viés de variáveis não observadas (Hidden Bias), a exigência de grandes amostras e boa qualidade de dados com sobreposição substancial, a sensibilidade à especificação do modelo do escore de propensão, e a potencial perda de dados de unidades que não encontram pares adequados. A comparação entre PSM e RCTs revela um trade-off inerente entre a validade interna e a validade externa. Para mitigar o viés de covariáveis não observadas, testes de sensibilidade, como o método de Rosenbaum Bounds (que introduz um parâmetro Γ para limitar a razão das chances de tratamento), são essenciais para avaliar a robustez das conclusões.

#### 3.3. Regressão Logística Ordinal: Conceitos e Usos

A Regressão Logística Ordinal (RLO), também conhecida como regressão ordinal ou modelo de odds proporcionais (proportional odds logistic regression), é um modelo de regressão projetado para variáveis dependentes ordinais. É utilizada para prever uma variável dependente cujas categorias podem ser ranqueadas, mas a distância real entre elas é desconhecida (e.g., escalas Likert, níveis de gravidade de doença), com base em uma ou mais variáveis independentes (contínuas, categóricas ou ordinais). A principal motivação para usar a RLO é a preservação da informação contida na ordenação das categorias da variável resposta, pois procedimentos simplificados, como a dicotomização ou o tratamento como nominal, levam à perda de informação, de poder estatístico e a inferências incorretas.

Existem diversas variações de modelos de regressão ordinal. O Modelo de Chances Proporcionais (POM – Proportional Odds Model) é o mais comum, assumindo que o efeito de uma variável independente é constante em todas as divisões cumulativas da variável dependente ordinal (o pressuposto de odds proporcionais ou linhas paralelas), fornecendo uma única estimativa de Odds Ratio (OR). O Modelo de Chances Proporcionais Parciais (PPOM – Partial Proportional Odds Model) é uma extensão que permite a violação da suposição de odds proporcionais para algumas covariáveis. Outros modelos incluem o Modelo de Razão Contínua (CRM – Continuous Ratio Model) e o Modelo Estereótipo (SM – Stereotype Model). A escolha do modelo deve ser baseada no caráter da variável ordinal, na validade dos pressupostos, na qualidade do ajuste e na parcimônia.

A aplicação correta da RLO depende da satisfação de pressupostos cruciais: a variável dependente deve ser ordinal; as variáveis independentes podem ser de diferentes tipos; deve haver ausência de multicolinearidade entre as variáveis independentes; o Pressuposto de Odds Proporcionais (ou Linhas Paralelas) é o mais crítico e frequentemente violado, postulando que o efeito de cada variável independente é idêntico em cada divisão cumulativa da variável dependente ordinal; e a Independência das Observações, que é frequentemente violada em dados de inquéritos complexos devido ao desenho amostral por conglomerados, exigindo ajustes como a ponderação e a consideração do efeito do desenho amostral para obter estimativas válidas e variâncias corretas.

A interpretação dos resultados da RLO é feita em termos de log-odds cumulativos, onde um aumento de uma unidade na variável preditora está associado a uma mudança multiplicativa nas odds de estar em ou abaixo de uma categoria, mantendo outras variáveis constantes. Os Odds Ratios (OR) são centrais para compreender a magnitude e direção dos efeitos: OR > 1 indica aumento nas chances de estar em uma categoria superior, e OR < 1 indica diminuição. Sob o pressuposto de odds proporcionais, o OR é consistente em todas as categorias cumulativas, representando a mudança nas chances de transitar para uma categoria superior (ou inferior) em qualquer ponto da escala ordinal.

O diagnóstico do modelo e o tratamento de violações de pressupostos são cruciais para a validade da RLO. Isso inclui o teste do Pressuposto de Odds Proporcionais (e.g., teste de Brant ou Wald), a avaliação de multicolinearidade (e.g., VIF) e a qualidade do ajuste (e.g., pseudo-R², análise de resíduos). Se o pressuposto de odds proporcionais for violado, o PPOM pode ser uma alternativa, ou a utilização de modelos multinomiales (com perda de informação). Em inquéritos complexos, o tratamento de dados faltantes (idealmente com imputação múltipla) e o manejo de outliers são essenciais. A complexidade da RLO, especialmente o diagnóstico e tratamento da violação do pressuposto de odds proporcionais, pode limitar sua utilização, embora a disponibilidade de software livre (como R) democratize o acesso.

#### 3.4. Integração e Aplicações: PNS, PSM e Regressão Logística Ordinal

A combinação de PSM e RLO em dados de inquéritos complexos, como a PNS, representa um pico de complexidade metodológica, mas é poderosa para inferência causal com desfechos ordinais.

#### 3.4.1. Aplicações do PSM com Dados da PNS: Estudos de Caso e Boas Práticas

O PSM é uma ferramenta valiosa para estudos de avaliação de impacto de políticas públicas e intervenções de saúde que utilizam dados observacionais como os da PNS, permitindo a criação de grupos de comparação balanceados. No contexto brasileiro, exemplos de aplicação incluem a avaliação de políticas de segurança pública (com dados do Censo Demográfico 2010), a estimação de elasticidades-preço do consumo de cigarros (com dados da PNS 2013 e 2019), a investigação da relação causal entre adversidades na infância e problemas crônicos de saúde na idade adulta (com dados do ELSI-Brasil), e a análise da desigualdade de renda e mortalidade em São Paulo (com dados do Censo 2000). Boas práticas observadas nesses estudos incluem o uso de dados de linha de base para estimação do escore, seleção de covariáveis que influenciam tanto o tratamento quanto o desfecho, avaliação rigorosa do balanço e consideração de métodos de pareamento "com reposição".

#### 3.4.2. Aplicações da Regressão Logística Ordinal com Dados da PNS: Estudos de Caso e Boas Práticas

A RLO é particularmente útil para analisar desfechos de saúde medidos em escalas ordinais (e.g., autoavaliação da saúde, níveis de qualidade de vida, gravidade de doenças), que são frequentemente presentes na PNS. Ela otimiza a análise desses desfechos, extraindo informações mais refinadas sobre os fatores associados a diferentes níveis de bem-estar ou gravidade. Embora o referencial mencione estudos de qualidade de vida em pacientes com esquizofrenia (utilizando escalas como QLS-BR), análise de fatores de risco para hipertensão arterial (PNS 2019, mas com regressão logística binária, sendo RLO aplicável para desfechos ordinais de pressão arterial), e modelagem de desfechos categorizados em estudos de hipertensão (combinando RLO com redes neurais), esses exemplos ilustram a aplicabilidade da RLO a desfechos semelhantes aos da PNS. Boas práticas incluem o reconhecimento da natureza ordinal da variável resposta, teste e validação dos pressupostos (especialmente odds proporcionais), uso de software estatístico apropriado que considere o desenho amostral complexo da PNS, e interpretação cuidadosa dos coeficientes e odds ratios.

#### 3.4.3. Desafios e Sinergias na Combinação de PSM e Regressão Logística Ordinal em Inquéritos Complexos

A combinação de PSM e RLO em dados de inquéritos complexos como a PNS representa um desafio metodológico significativo, embora poderosa para inferência causal com desfechos ordinais. Os desafios incluem a necessidade de ambos os métodos considerarem o desenho amostral complexo (pesos, estratos, conglomerados), o que é frequentemente negligenciado na prática. A integração mais comum envolve aplicar a RLO após o PSM ter criado grupos balanceados, para analisar o efeito do tratamento em um desfecho ordinal. A RLO também pode ser usada para estimar escores de propensão generalizados para tratamentos ordinais. A gestão robusta de dados faltantes e a identificação de outliers são cruciais.

As sinergias permitem abordagens como a sequência lógica de usar o PSM primeiro para minimizar o viés de seleção e, em seguida, aplicar a RLO ao subconjunto de dados balanceado para modelar o desfecho ordinal, estimando o efeito causal do "tratamento". O ajuste duplo (PSM com ajuste de regressão adicional) ou a ponderação por escore de propensão (aplicando RLO ponderada) são outras abordagens. Contudo, a falha em abordar adequadamente essas complexidades pode levar a resultados inválidos.

## 4. Metodologia

### 4.1. Fonte de Dados

Este estudo utilizou dados secundários provenientes da Pesquisa Nacional de Saúde (PNS) de 2019, um inquérito de base domiciliar de abrangência nacional, realizado pelo Instituto Brasileiro de Geografia e Estatística (IBGE) em parceria com o Ministério da Saúde. Os microdados da PNS 2019, que incluem informações detalhadas sobre a saúde da população brasileira, foram acessados e baixados publicamente através do portal da Pesquisa Nacional de Saúde, disponível em https://www.pns.icict.fiocruz.br/bases-de-dados/. A PNS é caracterizada por um desenho amostral complexo, que geralmente envolve amostragem por conglomerados em múltiplos estágios, fundamental para garantir a representatividade da população brasileira em suas estimativas.

### 4.2. Variáveis do Estudo

As variáveis foram selecionadas com base em sua relevância para o problema de pesquisa e disponibilidade na PNS 2019. A variável de tratamento (ou alvo) foi a posse de ```plano de saúde``` (originalmente ```I00102```, renomeada para plano_saude), dicotomizada em ```0``` para ```"não"``` e ```1``` para ```"sim"```. A variável de desfecho (ou de análise) foi a ```saúde subjetiva``` (originalmente ```N001```, renomeada para ```saude_subjetivo```), uma variável ordinal com categorias que foram transformadas para representar uma escala Likert de ```0``` (Muito ruim) a ```4``` (Muito boa).

As covariáveis utilizadas no estudo, para controlar potenciais fatores de confusão e para a estimação do escore de propensão, incluíram:

Demográficas: ```sexo (C006)```, ```idade (C008)```, ```cor_raca (C009)```.

Socioeconômicas: ```renda_domiciliar_per_capita (VDF003)```, ```instrucao (VDD004A)```, ```tipo_area (V0031)```, ```uf (sigla_uf_sigla)```.

Comportamentais e Hábitos de Vida: ```qtd_consultas_12_meses (J012)```, ```internacoes_12_meses (J037)```, ```alcool_30_dias (P03201)```, ```atividade_fisica_3_meses (P034)```, ```fumante (P050)```.

Condições de Saúde e Morbidades: ```hipertensao (Q00201)```, ```diagnostico_diabetes (Q03001)```, ```diagnostico_colesterol (Q060)```, ```doenca_cardiaca (Q06306)```, ```avc (Q068)```, ```asma (Q074)```, ```dor_coluna (Q084)```, ```depressao (Q092)```, ```ansiedade (Q11006)```.

### 4.3. Tratamento e Pré-processamento de Dados

A etapa de tratamento de dados foi realizada conforme as seguintes especificações:

Remoção Inicial de Colunas: Colunas que não eram essenciais para a análise ou que possuíam alta redundância foram descartadas. Isso incluiu sigla_uf, sigla_uf_nome, V0020, V0006_PNS, UPA_PNS, e VDF002.
Renomeação de Variáveis: As colunas foram renomeadas para nomes mais intuitivos, facilitando a legibilidade e o manuseio no ambiente de análise (vide a lista de variáveis acima).
Substituição de Valores Ausentes por NaN: A string 'não informado', presente em diversas colunas para indicar valores ausentes, foi substituída pelo valor padrão np.nan.
Remoção de Linhas com Alta Taxa de NaN:
Inicialmente, foram removidas linhas onde todas as variáveis da coluna 6 em diante (que incluem a maioria das variáveis de saúde e comportamento) eram NaN, o que reduziu o DataFrame de 344.887 para 279.382 linhas.
Em seguida, colunas com mais de 80% de valores ausentes foram removidas, resultando na exclusão de 3 colunas, que eram N001 (saude_subjetivo), P03201 (alcool_30_dias) e P035 (atividade_fisica_por_semana). No entanto, uma revisão do notebook indica que saude_subjetivo foi mantida no dataset, o que sugere que a ordem ou a condição de remoção podem ter sido ajustadas subsequentemente no processo de desenvolvimento do notebook. (Nota: N001 - saude_subjetivo é utilizada no modelo final, e a variável alcool_30_dias e P035 - atividade_fisica_por_semana foram dropadas. É importante verificar a consistência no artigo final).
Finalmente, linhas que possuíam mais de 9 valores ausentes em suas colunas foram removidas, resultando em um DataFrame com 90.846 linhas. Esta etapa foi crucial para focar a análise em observações com dados mais completos.
Padronização e Transformação de Variáveis Categóricas:
A coluna tipo_area teve seus valores padronizados para 'Capital', 'Resto da RM' e 'Resto da UF', e 'RIDE'.
A string ' ou equivalente' foi removida da coluna instrucao.
Conversão para Tipo Numérico e Ordinal:
Variáveis binárias como plano_saude e internacoes_12_meses foram padronizadas, substituindo 'não' por 0 e 'sim' por 1.
A variável saude_subjetivo teve suas categorias textuais ('Muito ruim', 'Ruim', 'Regular', 'Boa', 'Muito boa') convertidas para uma escala numérica ordinal de 0 a 4, respectivamente.
A variável fumante teve suas categorias textuais convertidas para 0 (Não fumo atualmente) e 1 (Sim, diariamente/Sim, menos que diariamente).
A variável instrucao teve suas categorias textuais convertidas para uma escala numérica ordinal de 0 (Sem instrução) a 6 (Superior completo).
Todas as colunas numéricas (exceto renda_domiciliar_per_capita) foram convertidas para o tipo inteiro (int), preenchendo NaN com 0 onde necessário antes da conversão.
A coluna idade foi convertida para tipo inteiro.
A coluna estrato foi convertida para tipo string.

### 4.4. Imputação de Valores Ausentes (MICE)

Para as colunas restantes que ainda continham valores ausentes, a imputação por Multiple Imputation by Chained Equations (MICE) foi aplicada. Utilizando IterativeImputer da sklearn.experimental, as colunas numéricas do DataFrame foram preenchidas, garantindo a completude dos dados para as análises subsequentes. Após a imputação, uma nova conversão de colunas numéricas (exceto renda_domiciliar_per_capita) para o tipo inteiro foi realizada.

### 4.5. Qualidade dos Dados Pós-Tratamento

Após todas as etapas de tratamento e imputação, uma verificação final da qualidade dos dados foi realizada. O percentual de valores ausentes em todas as colunas foi avaliado, confirmando a ausência total de valores nulos no DataFrame resultante, com um total de 90.846 linhas. Adicionalmente, o domínio (valores únicos) de cada variável foi inspecionado para assegurar a consistência e a validade dos dados. A coluna estrato foi então descartada, pois não seria utilizada nos modelos finais.

### 4.6. Transformação de Variáveis Categóricas (Dummies)

As variáveis categóricas remanescentes que não eram ordinais (uf, tipo_area, sexo, cor_raca) foram transformadas em variáveis dummy (ou one-hot encoding) usando pd.get_dummies(). Este processo converte cada categoria única em uma nova coluna binária, preparando o DataFrame para a modelagem estatística.

### 4.7. Balanceamento de Dados por Propensity Score Matching (PSM)

Para mitigar o viés de seleção inerente a estudos observacionais e criar grupos comparáveis de indivíduos com e sem plano de saúde, foi aplicada a metodologia de Propensity Score Matching (PSM). As etapas foram as seguintes:

Estimação do Escore de Propensão: Primeiramente, um modelo de Regressão Logística (sm.Logit) foi ajustado para estimar a probabilidade condicional de um indivíduo possuir um plano de saúde (plano_saude) dadas suas covariáveis observadas (todas as variáveis do DataFrame, exceto plano_saude e saude_subjetivo). Todas as variáveis foram convertidas para float e uma constante foi adicionada ao modelo preditor. O resultado dessa predição gerou o propensity_score para cada indivíduo.
Avaliação do Balanço Pré-Pareamento: A distribuição dos propensity_score para os grupos com e sem plano de saúde foi visualizada através de um histograma com estimativa de densidade (kde=True). Esta análise inicial revelou a necessidade de um balanceamento mais efetivo, pois a sobreposição entre as distribuições não era ideal para garantir a comparabilidade direta dos grupos.
Balanceamento por Downsampling: Para criar grupos de tratamento e controle com distribuições de covariáveis mais homogêneas, foi aplicado um downsampling na classe majoritária (indivíduos sem plano de saúde, plano_saude == 0). Um subconjunto aleatório da classe majoritária foi selecionado sem reposição, com um número de amostras igual ao da classe minoritária (indivíduos com plano de saúde, plano_saude == 1). As duas classes balanceadas foram então concatenadas para formar o df_balanced.
Avaliação do Balanço Pós-Pareamento: Após o balanceamento, um novo modelo de Regressão Logística foi ajustado no df_balanced para recalcular os propensity_score e verificar a sobreposição das distribuições. O histograma resultante demonstrou uma ampla região de sobreposição (especialmente entre 0.1 e 0.9), indicando que o balanceamento foi bem-sucedido em encontrar indivíduos com e sem plano de saúde que possuem características observadas muito semelhantes, fortalecendo a capacidade de inferências causais.

### 4.8. Aplicação do Modelo de Regressão Logística Ordinal

Para analisar o efeito da posse de plano de saúde na saúde subjetiva, que é uma variável dependente ordinal, foi aplicado um Modelo de Regressão Logística Ordinal (OrderedModel do statsmodels).

Variável Dependente: saude_subjetivo (escala ordinal de 0 a 4).
Variáveis Independentes: Todas as covariáveis utilizadas na estimação do escore de propensão foram incluídas como preditoras no modelo de regressão ordinal, com exceção da própria saude_subjetivo e do propensity_score, que não é utilizado como preditor no modelo final de desfecho após o pareamento. Todas as variáveis foram convertidas para o tipo float antes do ajuste do modelo.
Especificação do Modelo: O modelo foi ajustado utilizando a distribuição probit (distr='probit'), que é uma alternativa comum à distribuição logística em modelos ordinais.
Ajuste do Modelo: O modelo foi ajustado usando o método 'bfgs' de otimização. O sumário do res_prob.summary() forneceu os coeficientes, erros padrão, valores-z, p-valores e intervalos de confiança para cada preditor, além de informações sobre a qualidade do ajuste do modelo.

## 5. Resultados
**6. Resultados**

A análise dos dados da Pesquisa Nacional de Saúde (PNS) de 2019, após as etapas de tratamento, imputação e balanceamento, revelou insights importantes sobre a percepção da saúde subjetiva e sua relação com a posse de plano de saúde e outras covariáveis.

**6.1. Caracterização da Amostra**

Inicialmente, a amostra bruta da PNS 2019 continha 344.887 linhas, que foram reduzidas para 90.846 após o pré-processamento e a remoção de valores ausentes. Para a análise principal, a amostra foi balanceada por meio do *downsampling* na classe majoritária, resultando em um DataFrame balanceado (`df_balanced`) com 41.136 observações, onde há uma distribuição equitativa entre indivíduos com plano de saúde (20.568) e sem plano de saúde (20.568).

**6.2. Análise Descritiva Comparativa entre Grupos**

A comparação entre os grupos com e sem plano de saúde, na amostra original, revelou disparidades importantes antes do balanceamento por Propensity Score Matching (PSM):

* **Atividade Física:** Indivíduos com plano de saúde apresentaram uma maior proporção de prática de atividade física nos últimos 3 meses (56.19%) em comparação com aqueles sem plano (35.35%).
    * **[INSERIR GRÁFICO: Frequência de Atividade Física por Plano de Saúde]**
* **Hábito de Fumar:** A prevalência de tabagismo foi menor no grupo com plano de saúde (7.95%) do que no grupo sem plano (13.87%).
    * **[INSERIR GRÁFICO: Frequência de Fumantes por Plano de Saúde]**
* **Internações nos Últimos 12 Meses:** Uma proporção ligeiramente maior de indivíduos com plano de saúde relatou internações nos últimos 12 meses (9.81%) em comparação com aqueles sem plano (7.06%).
* **Percepção da Saúde Subjetiva:** O grupo com plano de saúde apresentou uma percepção de saúde subjetiva notavelmente mais positiva. Indivíduos com plano de saúde relataram "Boa" (53.88%) e "Muito boa" (22.47%) em maior proporção, enquanto no grupo sem plano, as categorias "Regular" (33.72%) e "Ruim" (6.28%) foram mais frequentes.
    * **[INSERIR GRÁFICO: Frequência de Saúde Subjetiva por Plano de Saúde]**
* **Renda Domiciliar Per Capita:** Uma diferença substancial na renda foi observada, com a média de renda per capita para pessoas com plano de saúde sendo R$ 3583.88, significativamente superior à média de R$ 1013.76 para pessoas sem plano de saúde.
    * **[INSERIR GRÁFICO: Média de Renda Per Capita por Plano de Saúde]**

**6.3. Balanço dos Propensity Scores**

A avaliação da distribuição dos *Propensity Scores* (PS) após o balanceamento por *downsampling* demonstrou uma significativa melhoria na sobreposição entre os grupos de tratamento e controle. Conforme ilustrado no histograma gerado, as distribuições dos PS para indivíduos com e sem plano de saúde no `df_balanced` mostraram uma ampla região de sobreposição, especialmente entre 0.1 e 0.9. Esta sobreposição indica que o processo de balanceamento foi eficaz em criar grupos comparáveis em termos das covariáveis observadas, permitindo uma inferência causal mais robusta.

* **[INSERIR GRÁFICO: Distribuição dos Propensity Scores por Grupo de Tratamento (pós-balanceamento)]**

**6.4. Resultados da Regressão Logística Ordinal**

O modelo de Regressão Logística Ordinal (probit), ajustado no DataFrame balanceado, analisou o impacto da posse de plano de saúde na saúde subjetiva, controlando por um conjunto abrangente de covariáveis. Os principais resultados do sumário do modelo (`res_prob.summary()`) são apresentados a seguir:

* **Impacto do Plano de Saúde:** A variável `plano_saude` apresentou um coeficiente de **0.2822** (p < 0.001). Este resultado sugere que, mantendo as outras variáveis constantes e após o balanceamento das covariáveis, a posse de um plano de saúde está associada a uma maior probabilidade de relatar uma percepção de saúde subjetiva mais elevada (ou seja, categorias de saúde melhor avaliadas).
* **Outras Covariáveis Relevantes:** Diversas outras covariáveis demonstraram associações estatisticamente significativas com a saúde subjetiva:
    * **Idade:** O coeficiente de `idade` foi negativo (-0.0077, p < 0.001), indicando que o aumento da idade está associado a uma menor probabilidade de relatar saúde subjetiva melhor.
    * **Atividade Física:** A `atividade_fisica_3_meses` teve um coeficiente positivo (0.2772, p < 0.001), mostrando associação com uma melhor percepção da saúde.
    * **Fumante:** A variável `fumante` apresentou um coeficiente negativo (-0.0457, p = 0.011), indicando que ser fumante está associado a uma pior saúde subjetiva.
    * **Condições Crônicas e Morbidades:** Variáveis como `hipertensao` (-0.2529, p < 0.001), `diagnostico_diabetes` (-0.4393, p < 0.001), `diagnostico_colesterol` (-0.1582, p < 0.001), `doenca_cardiaca` (-0.3352, p < 0.001), `avc` (-0.2382, p < 0.001), `asma` (-0.2198, p < 0.001), `dor_coluna` (-0.4305, p < 0.001), `depressao` (-0.3456, p < 0.001) e `ansiedade` (-0.2607, p < 0.001) apresentaram coeficientes negativos e altamente significativos, indicando que a presença dessas condições está associada a uma pior percepção da saúde subjetiva.
    * **Instrução e Renda:** A variável `instrucao` (0.0939, p < 0.001) e `renda_domiciliar_per_capita` (2.715e-05, p < 0.001) tiveram coeficientes positivos, sugerindo que níveis mais altos de escolaridade e renda per capita estão associados a uma melhor percepção da saúde.
    * **Sexo:** Ser do `sexo_Homem` apresentou coeficiente positivo (0.0585, p < 0.001), indicando que homens tendem a relatar uma saúde subjetiva ligeiramente melhor, controlando pelas demais variáveis.
    * **Raça/Cor:** `cor_raca_Branca` (0.2059, p < 0.001) e `cor_raca_Parda` (0.0819, p < 0.001) apresentaram coeficientes positivos em relação à categoria de referência (provavelmente 'Preta' ou 'Indígena', dependendo da ordenação das dummies), indicando melhor percepção de saúde subjetiva. `cor_raca_Amarela` (0.0319, p = 0.599) e `cor_raca_Indígena` (0.0088, p = 0.901) e `cor_raca_Ignorado` (0.0036, p = 0.993) não foram estatisticamente significativas.
    * **Localização:** `tipo_area_Capital` (0.0480, p < 0.001) teve coeficiente positivo, sugerindo que residir na capital está associado a uma melhor percepção de saúde subjetiva. `tipo_area_RIDE` (-0.0702, p = 0.285) e `tipo_area_Resto da RM` (-0.0070, p = 0.684) não foram estatisticamente significativas. Várias UFs apresentaram coeficientes positivos e negativos significativos, indicando variações regionais na saúde subjetiva percebida.

* **[INSERIR TABELA: Sumário do Modelo de Regressão Logística Ordinal (`res_prob.summary()`)]**
## 6. Discussão

## 7. Conclusão

## 8. Referências Bibliográficas

## 9. Apêndices (se necessário)

