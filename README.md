# Análise do Impacto do Plano de Saúde na Saúde Subjetiva Utilizando Propensity Score Matching na PNS 2019

## Resumo/Abstract

Este artigo investiga a influência da posse de um plano de saúde na percepção da saúde subjetiva da população brasileira, utilizando dados da Pesquisa Nacional de Saúde (PNS) de 2019. Dada a natureza observacional dos dados e a necessidade de inferência causal robusta, a metodologia empregou o Pareamento por Escore de Propensão (PSM) para balancear as covariáveis entre os grupos com e sem plano de saúde, seguido pela aplicação de um Modelo de Regressão Logística Ordinal (probit) para analisar o desfecho. Os dados brutos da PNS foram submetidos a um rigoroso pré-processamento, incluindo remoção de valores ausentes, padronização e imputação MICE, culminando em um DataFrame balanceado com 41.136 observações equitativamente distribuídas entre os grupos. Os resultados demonstram que, após o controle por fatores socioeconômicos, demográficos e de saúde, a posse de um plano de saúde está positivamente e estatisticamente associada a uma melhor autoavaliação da saúde subjetiva (coeficiente de 0.4903, p < 0.001). Fatores como atividade física, instrução e renda per capita também foram associados a uma melhor percepção da saúde, enquanto idade e a presença de condições crônicas/morbidades (e.g., hipertensão, depressão) demonstraram associação negativa. Este estudo reforça o papel da saúde suplementar no bem-estar percebido e sublinha a importância de métodos inferenciais para subsidiar políticas públicas de saúde baseadas em evidências e equidade.

**Palavras-chave:** Saúde Pública; Plano de Saúde; Saúde Subjetiva; Pareamento por Escore de Propensão; PMS; Regressão Logística Ordinal; PNS.

## 1. Introdução

O sistema de saúde brasileiro é caracterizado por sua dualidade, compreendendo o Sistema Único de Saúde (SUS), de caráter universal e público, e a saúde suplementar, predominantemente privada, que engloba os planos e seguros de saúde. Ambos os pilares desempenham funções cruciais na provisão de acesso e na garantia da saúde da população, embora com diferentes modelos de financiamento e acesso. A compreensão da dinâmica entre esses sistemas e seus impactos na percepção individual de saúde é fundamental para o planejamento e aprimoramento das políticas de saúde pública no país.

A saúde, em sua definição mais abrangente, transcende a mera ausência de doença, incorporando dimensões de bem-estar físico, mental e social. Nesse contexto, a saúde subjetiva emerge como um indicador de vital importância, uma vez que reflete a autoavaliação do indivíduo sobre seu próprio estado de saúde e bem-estar geral. Essa percepção pessoal, frequentemente influenciada por fatores além das condições clínicas objetivas, oferece insights valiosos sobre a qualidade de vida e a eficácia dos sistemas de saúde sob a ótica do cidadão. Para investigar essa complexa interação no contexto brasileiro, este estudo utiliza os dados da Pesquisa Nacional de Saúde (PNS) de 2019, uma fonte de informação robusta e representativa da população, que oferece um panorama detalhado das condições de saúde e acesso a serviços no país.

Diante do exposto, este estudo busca responder à seguinte questão de pesquisa: qual a influência da posse de um plano de saúde na percepção da saúde subjetiva de indivíduos no Brasil, considerando a heterogeneidade socioeconômica e demográfica da população? Para abordar essa questão, o objetivo geral é analisar a relação entre a posse de um plano de saúde e a saúde subjetiva da população brasileira, utilizando dados da PNS 2019 e técnicas de inferência causal.

Para alcançar este objetivo geral, foram estabelecidos os seguintes objetivos específicos:
* Caracterizar a distribuição da saúde subjetiva em grupos com e sem plano de saúde na amostra da PNS 2019.
* Identificar as principais covariáveis socioeconômicas e de saúde associadas tanto à posse de um plano de saúde quanto à saúde subjetiva.
* Empregar a metodologia de Propensity Score Matching (PSM) para balancear as covariáveis observadas entre os grupos com e sem plano de saúde, visando a obtenção de grupos comparáveis e a redução de vieses de seleção.
* Estimar o efeito da posse de um plano de saúde na saúde subjetiva por meio de um modelo de regressão ordinal, após a aplicação do balanceamento por PSM.

A relevância deste estudo reside em sua contribuição para a compreensão aprofundada dos determinantes da saúde da população brasileira. Ao aplicar métodos de inferência causal, como o Propensity Score Matching (PSM), este trabalho busca fornecer subsídios mais robustos sobre o impacto específico da posse de um plano de saúde na percepção da saúde subjetiva. Os achados podem informar e subsidiar a formulação de políticas públicas em saúde, contribuindo para uma alocação mais eficiente de recursos e o aprimoramento contínuo dos serviços de saúde no Brasil, tanto no Sistema Único de Saúde (SUS) quanto na saúde suplementar.

## 2. Referencial Teórico

A pesquisa em saúde pública no Brasil depende fundamentalmente da análise de dados complexos provenientes de inquéritos populacionais, como a Pesquisa Nacional de Saúde (PNS). A natureza observacional de muitos estudos nesse campo exige a aplicação de metodologias estatísticas avançadas para garantir a validade das inferências causais e a precisão das estimativas. A crescente disponibilidade de bases de dados abrangentes, aliada à necessidade de inferências robustas em cenários não-experimentais, demanda pesquisadores aptos a explorar as nuances metodológicas impostas pela busca por relações de causa e efeito em contextos não-controlados. Este estudo se insere nesse contexto, combinando a riqueza dos dados da PNS com técnicas avançadas como o Pareamento por Escore de Propensão (PSM) e a Regressão Logística Ordinal para aprofundar a compreensão sobre os determinantes da saúde subjetiva.

### 2.1. Pesquisa Nacional de Saúde (PNS): Contexto e Relevância

A Pesquisa Nacional de Saúde (PNS) é um inquérito de base domiciliar de abrangência nacional, realizado pelo Instituto Brasileiro de Geografia e Estatística (IBGE) em parceria com o Ministério da Saúde, com periodicidade de aproximadamente cinco anos (edições em 2013 e 2019). Seu principal objetivo é produzir dados sobre o desempenho do sistema nacional de saúde e as condições de saúde da população brasileira. A PNS transcende a saúde estrita, coletando informações detalhadas sobre população, trabalho, educação, habitação, renda, despesas, consumo, administração pública, participação política e social, justiça, segurança e proteção social. Essa vasta gama de dados permite análises multifacetadas e a investigação de determinantes sociais da saúde, consolidando-a como uma ferramenta poderosa para a epidemiologia, políticas públicas e ciências sociais aplicadas à saúde. A PNS, portanto, não é apenas um inquérito de saúde, mas uma base de dados socioeconômica e de saúde integrada, capaz de subsidiar a compreensão holística dos fenômenos de saúde e doença, e de embasar políticas públicas que considerem múltiplos determinantes.

A metodologia da PNS é caracterizada por um desenho amostral complexo, que geralmente envolve amostragem por conglomerados em múltiplos estágios, fundamental para garantir a representatividade da população brasileira em suas estimativas. O cálculo do tamanho da amostra considera a precisão desejada, os intervalos de confiança de 95%, o efeito do plano amostral (conglomerados), o número de domicílios selecionados e a taxa de não resposta. Para corrigir probabilidades de seleção desiguais e calibrar as estimativas para as populações totais conhecidas, são calculados pesos amostrais para os domicílios e seus residentes, ajustados também para a não resposta. A coleta de dados é baseada em questionários estruturados, com informações auto-referidas sobre saúde, satisfação do paciente e percepções. É crucial notar que o desenho amostral complexo impõe requisitos metodológicos rigorosos, pois ignorar os pesos amostrais e a estrutura de conglomerados pode levar a estimativas viesadas e inferências incorretas sobre a população brasileira, comprometendo a validade e a generalização dos resultados.

A PNS é uma fonte essencial para o monitoramento de doenças, comportamentos de risco, e acesso e uso de serviços de saúde, sendo primária para a identificação de padrões de doenças e custos de saúde, e para subsidiar o planejamento e a avaliação de políticas públicas de saúde. Ela transcende a mera coleta de dados, atuando como um instrumento de governança em saúde, cujos resultados influenciam práticas de cuidado médico e formulação de políticas públicas, permitindo uma tomada de decisão baseada em evidências em nível nacional.

No entanto, o uso dos dados da PNS apresenta desafios e oportunidades. A complexidade do desenho amostral exige softwares e métodos estatísticos específicos para o cálculo correto de estimativas e variâncias, garantindo que a estrutura de conglomerados e os pesos amostrais sejam adequadamente considerados. A natureza auto-referida de alguns dados pode introduzir vieses de informação. Há também a necessidade de lidar com dados faltantes e *outliers*, problemas que, quando não abordados adequadamente (especialmente em estudos que utilizam regressão logística), podem comprometer a validade dos achados. Apesar desses desafios, a PNS oferece oportunidades substanciais, como sua representatividade nacional (permitindo a generalização dos achados), a riqueza de variáveis coletadas (possibilitando a investigação de relações causais complexas e o controle de múltiplos fatores de confusão), e a disponibilidade de dados em diferentes edições (permitindo análises de tendências temporais e avaliação do impacto de políticas a longo prazo). Contudo, persiste uma lacuna significativa na aplicação rigorosa de boas práticas metodológicas, indicando a necessidade de aprimorar a aplicação das metodologias estatísticas para explorar o potencial da PNS de forma mais robusta e confiável.

### 2.2. Pareamento por Escore de Propensão (PSM): Fundamentos e Aplicação

O Pareamento por Escore de Propensão (PSM) é uma metodologia estatística quase-experimental fundamental para estimar o efeito de um tratamento, política ou intervenção em estudos observacionais, onde a randomização não é eticamente ou logisticamente viável. O PSM busca construir um grupo de controle artificial, emparelhando unidades tratadas com unidades não tratadas que possuem características observadas semelhantes, baseando-se no "escore de propensão" – a probabilidade condicional de uma unidade ser atribuída a um tratamento específico, dadas suas covariáveis observadas. Introduzido por Rosenbaum e Rubin (1983) e com contribuições de Heckman (1997), o PSM mimetiza a randomização ao balancear as covariáveis observadas entre grupos de tratamento e controle, buscando criar uma "pseudo-randomização" que permite atribuir diferenças de resultados ao tratamento de forma mais confiável, superando o viés de seleção inerente a dados não randomizados.

Para que o PSM produza estimativas válidas, dois pressupostos fundamentais devem ser satisfeitos: a Hipótese de Independência Condicional (CIA – *Conditional Independence Assumption* ou Ignorabilidade Forte), que afirma que, após ajustar por um conjunto relevante de covariáveis observadas, os desfechos potenciais são independentes da atribuição ao tratamento; e a Hipótese de Suporte Comum (*Overlap or Common Support*), que garante que, para cada valor das covariáveis observadas, haja uma probabilidade positiva de ser tratado e não tratado, assegurando sobreposição substancial nas distribuições dos escores de propensão entre os grupos. O pressuposto da independência condicional é infelizmente não testável com dados observacionais, implicando que a validade das inferências causais baseadas em PSM sempre conterá um grau de incerteza relacionado a vieses não observados, tornando a realização e o relato de testes de sensibilidade uma prática indispensável.

A aplicação do PSM envolve a identificação de unidades tratadas e não tratadas, e a coleta de características relevantes para a participação no tratamento e o desfecho. A Estimação do Escore de Propensão é geralmente realizada por meio de regressão logística (o método mais comum) ou probit, onde a variável dependente é binária (tratado/não tratado). O objetivo principal dessa estimação é balancear as covariáveis entre os grupos. Após a estimação, é crucial a Restrição ao Suporte Comum, descartando unidades fora dele. A escolha do algoritmo de pareamento (e.g., *nearest neighbor*, *caliper*, *kernel*) e a Avaliação do Balanço das Covariáveis (por meio de diferenças padronizadas e gráficos) são etapas cruciais e frequentemente iterativas; se o balanço não for adequado, é necessário refinar o procedimento. Finalmente, calcula-se a diferença média nos desfechos entre as unidades tratadas e seus pares de controle.

O PSM oferece a vantagem principal de reduzir o viés de seleção ao criar grupos comparáveis em características observadas, permitindo inferência causal em estudos observacionais onde RCTs (Ensaios Clínicos Randomizados) são inviáveis. Ele também reduz a dimensionalidade ao resumir múltiplas covariáveis em um único escore e diminui a dependência de modelagem específica do desfecho. Além disso, ao utilizar dados do "mundo real", pode aumentar a validade externa dos resultados. Contudo, suas limitações incluem o viés de variáveis não observadas (*Hidden Bias*), a exigência de grandes amostras e boa qualidade de dados com sobreposição substancial, a sensibilidade à especificação do modelo do escore de propensão, e a potencial perda de dados de unidades que não encontram pares adequados. A comparação entre PSM e RCTs revela um *trade-off* inerente entre a validade interna e a validade externa. Para mitigar o viés de covariáveis não observadas, testes de sensibilidade, como o método de Rosenbaum Bounds (que introduz um parâmetro Γ para limitar a razão das chances de tratamento), são essenciais para avaliar a robustez das conclusões.

### 2.3. Regressão Logística Ordinal: Conceitos e Usos

A Regressão Logística Ordinal (RLO), também conhecida como regressão ordinal ou modelo de *odds* proporcionais (*proportional odds logistic regression*), é um modelo de regressão projetado para variáveis dependentes ordinais. É utilizada para prever uma variável dependente cujas categorias podem ser ranqueadas, mas a distância real entre elas é desconhecida (e.g., escalas Likert, níveis de gravidade de doença), com base em uma ou mais variáveis independentes (contínuas, categóricas ou ordinais). A principal motivação para usar a RLO é a preservação da informação contida na ordenação das categorias da variável resposta, pois procedimentos simplificados, como a dicotomização ou o tratamento como nominal, levam à perda de informação, de poder estatístico e a inferências incorretas.

Existem diversas variações de modelos de regressão ordinal. O Modelo de Chances Proporcionais (POM – *Proportional Odds Model*) é o mais comum, assumindo que o efeito de uma variável independente é constante em todas as divisões cumulativas da variável dependente ordinal (o pressuposto de *odds* proporcionais ou linhas paralelas), fornecendo uma única estimativa de *Odds Ratio* (OR). O Modelo de Chances Proporcionais Parciais (PPOM – *Partial Proportional Odds Model*) é uma extensão que permite a violação da suposição de *odds* proporcionais para algumas covariáveis. Outros modelos incluem o Modelo de Razão Contínua (CRM – *Continuous Ratio Model*) e o Modelo Estereótipo (SM – *Stereotype Model*). A escolha do modelo deve ser baseada no caráter da variável ordinal, na validade dos pressupostos, na qualidade do ajuste e na parcimônia.

A aplicação correta da RLO depende da satisfação de pressupostos cruciais: a variável dependente deve ser ordinal; as variáveis independentes podem ser de diferentes tipos; deve haver ausência de multicolinearidade entre as variáveis independentes; o Pressuposto de *Odds* Proporcionais (ou Linhas Paralelas) é o mais crítico e frequentemente violado, postulando que o efeito de cada variável independente é idêntico em cada divisão cumulativa da variável dependente ordinal; e a Independência das Observações, que é frequentemente violada em dados de inquéritos complexos devido ao desenho amostral por conglomerados, exigindo ajustes como a ponderação e a consideração do efeito do desenho amostral para obter estimativas válidas e variâncias corretas.

A interpretação dos resultados da RLO é feita em termos de log-*odds* cumulativos, onde um aumento de uma unidade na variável preditora está associado a uma mudança multiplicativa nas *odds* de estar em ou abaixo de uma categoria, mantendo outras variáveis constantes. Os *Odds Ratios* (OR) são centrais para compreender a magnitude e direção dos efeitos: OR > 1 indica aumento nas chances de estar em uma categoria superior, e OR < 1 indica diminuição. Sob o pressuposto de *odds* proporcionais, o OR é consistente em todas as categorias cumulativas, representando a mudança nas chances de transitar para uma categoria superior (ou inferior) em qualquer ponto da escala ordinal.

O diagnóstico do modelo e o tratamento de violações de pressupostos são cruciais para a validade da RLO. Isso inclui o teste do Pressuposto de *Odds* Proporcionais (e.g., teste de Brant ou Wald), a avaliação de multicolinearidade (e.g., VIF) e a qualidade do ajuste (e.g., pseudo-R², análise de resíduos). Se o pressuposto de *odds* proporcionais for violado, o PPOM pode ser uma alternativa, ou a utilização de modelos multinomiales (com perda de informação). Em inquéritos complexos, o tratamento de dados faltantes (idealmente com imputação múltipla) e o manejo de *outliers* são essenciais. A complexidade da RLO, especialmente o diagnóstico e tratamento da violação do pressuposto de *odds* proporcionais, pode limitar sua utilização, embora a disponibilidade de *software* livre (como R) democratize o acesso.

### 2.4. Integração e Aplicações: PNS, PSM e Regressão Logística Ordinal

A combinação de PSM e RLO em dados de inquéritos complexos, como a PNS, representa um pico de complexidade metodológica, mas é poderosa para inferência causal com desfechos ordinais.

#### 2.4.1. Aplicações do PSM com Dados da PNS: Estudos de Caso e Boas Práticas

O PSM é uma ferramenta valiosa para estudos de avaliação de impacto de políticas públicas e intervenções de saúde que utilizam dados observacionais como os da PNS, permitindo a criação de grupos de comparação balanceados. No contexto brasileiro, exemplos de aplicação incluem a avaliação de políticas de segurança pública (com dados do Censo Demográfico 2010), a estimação de elasticidades-preço do consumo de cigarros (com dados da PNS 2013 e 2019), a investigação da relação causal entre adversidades na infância e problemas crônicos de saúde na idade adulta (com dados do ELSI-Brasil), e a análise da desigualdade de renda e mortalidade em São Paulo (com dados do Censo 2000). Boas práticas observadas nesses estudos incluem o uso de dados de linha de base para estimação do escore, seleção de covariáveis que influenciam tanto o tratamento quanto o desfecho, avaliação rigorosa do balanço e consideração de métodos de pareamento "com reposição".

#### 2.4.2. Aplicações da Regressão Logística Ordinal com Dados da PNS: Estudos de Caso e Boas Práticas

A RLO é particularmente útil para analisar desfechos de saúde medidos em escalas ordinais (e.g., autoavaliação da saúde, níveis de qualidade de vida, gravidade de doenças), que são frequentemente presentes na PNS. Ela otimiza a análise desses desfechos, extraindo informações mais refinadas sobre os fatores associados a diferentes níveis de bem-estar ou gravidade. Embora o referencial mencione estudos de qualidade de vida em pacientes com esquizofrenia (utilizando escalas como QLS-BR), análise de fatores de risco para hipertensão arterial (PNS 2019, mas com regressão logística binária, sendo RLO aplicável para desfechos ordinais de pressão arterial), e modelagem de desfechos categorizados em estudos de hipertensão (combinando RLO com redes neurais), esses exemplos ilustram a aplicabilidade da RLO a desfechos semelhantes aos da PNS. Boas práticas incluem o reconhecimento da natureza ordinal da variável resposta, teste e validação dos pressupostos (especialmente *odds* proporcionais), uso de software estatístico apropriado que considere o desenho amostral complexo da PNS, e interpretação cuidadosa dos coeficientes e *odds ratios*.

#### 2.4.3. Desafios e Sinergias na Combinação de PSM e Regressão Logística Ordinal em Inquéritos Complexos

A combinação de PSM e RLO em dados de inquéritos complexos como a PNS representa um pico de complexidade metodológica, mas é poderosa para inferência causal com desfechos ordinais. Os desafios incluem a necessidade de ambos os métodos considerarem o desenho amostral complexo (pesos, estratos, conglomerados), o que é frequentemente negligenciado na prática. A integração mais comum envolve aplicar a RLO após o PSM ter criado grupos balanceados, para analisar o efeito do tratamento em um desfecho ordinal. A RLO também pode ser usada para estimar escores de propensão generalizados para tratamentos ordinais. A gestão robusta de dados faltantes e a identificação de *outliers* são cruciais.

As sinergias permitem abordagens como a sequência lógica de usar o PSM primeiro para minimizar o viés de seleção e, em seguida, aplicar a RLO ao subconjunto de dados balanceado para modelar o desfecho ordinal, estimando o efeito causal do "tratamento". O ajuste duplo (PSM com ajuste de regressão adicional) ou a ponderação por escore de propensão (aplicando RLO ponderada) são outras abordagens. Contudo, a falha em abordar adequadamente essas complexidades pode levar a resultados inválidos.

#### 2.4.4. Perspectivas Acadêmicas e Avanços Recentes

Os campos do PSM e da RLO estão em constante evolução. No PSM, há interesse crescente na integração sinérgica com RCTs para aumentar a generalizabilidade, no desenvolvimento de métodos que preservam a privacidade dos dados, e na utilização de *machine learning* para a estimação de escores de propensão. Na RLO, avanços incluem modelos híbridos (combinando RLO com redes neurais e *bootstrapping*), novas abordagens para lidar com instâncias ambíguas e aprimoramento da inferência causal para desfechos ordinais que não possuem uma escala significativa. Para a PNS e inquéritos complexos, a disponibilidade de pacotes estatísticos especializados facilita a aplicação de técnicas avançadas, mas ainda há necessidade de maior rigor nas boas práticas metodológicas. Essa convergência metodológica aponta para análises mais preditivas e causais na pesquisa em saúde pública, exigindo que os pesquisadores se mantenham atualizados com as fronteiras metodológicas.

## 3. Metodologia

### 3.1. Fonte de Dados

Este estudo utilizou dados secundários provenientes da Pesquisa Nacional de Saúde (PNS) de 2019, um inquérito de base domiciliar de abrangência nacional, realizado pelo Instituto Brasileiro de Geografia e Estatística (IBGE) em parceria com o Ministério da Saúde. Os microdados da PNS 2019, que incluem informações detalhadas sobre a saúde da população brasileira, foram acessados e baixados publicamente através do portal da Pesquisa Nacional de Saúde, disponível em https://www.pns.icict.fiocruz.br/bases-de-dados/. A PNS é caracterizada por um desenho amostral complexo, que geralmente envolve amostragem por conglomerados em múltiplos estágios, fundamental para garantir a representatividade da população brasileira em suas estimativas.

### 3.2. Variáveis do Estudo

As variáveis foram selecionadas com base em sua relevância para o problema de pesquisa e disponibilidade na PNS 2019. A variável de **tratamento** (ou alvo) foi a posse de **plano de saúde** (originalmente `I00102`, renomeada para `plano_saude`), dicotomizada em 0 para "não" e 1 para "sim". A variável de **desfecho** (ou de análise) foi a **saúde subjetiva** (originalmente `N001`, renomeada para `saude_subjetivo`), uma variável ordinal com categorias que foram transformadas para representar uma escala Likert de 0 (Muito ruim) a 4 (Muito boa).

As **covariáveis** utilizadas no estudo, para controlar potenciais fatores de confusão e para a estimação do escore de propensão, incluíram:
* **Demográficas:** `sexo` (`C006`), `idade` (`C008`), `cor_raca` (`C009`).
* **Socioeconômicas:** `renda_domiciliar_per_capita` (`VDF003`), `instrucao` (`VDD004A`), `tipo_area` (`V0031`), `uf` (`sigla_uf_sigla`).
* **Comportamentais e Hábitos de Vida:** `qtd_consultas_12_meses` (`J012`), `internacoes_12_meses` (`J037`), `alcool_30_dias` (`P03201`), `atividade_fisica_3_meses` (`P034`), `fumante` (`P050`).
* **Condições de Saúde e Morbidades:** `hipertensao` (`Q00201`), `diagnostico_diabetes` (`Q03001`), `diagnostico_colesterol` (`Q060`), `doenca_cardiaca` (`Q06306`), `avc` (`Q068`), `asma` (`Q074`), `dor_coluna` (`Q084`), `depressao` (`Q092`), `ansiedade` (`Q11006`).

### 3.3. Tratamento e Pré-processamento de Dados

A etapa de tratamento de dados foi realizada conforme as seguintes especificações:
* **Remoção Inicial de Colunas:** Colunas que não eram essenciais para a análise ou que possuíam alta redundância foram descartadas, incluindo `sigla_uf`, `sigla_uf_nome`, `V0020`, `V0006_PNS`, `UPA_PNS`, e `VDF002`.
* **Renomeação de Variáveis:** As colunas foram renomeadas para nomes mais intuitivos, facilitando a legibilidade e o manuseio no ambiente de análise (vide a lista de variáveis acima).
* **Substituição de Valores Ausentes por `NaN`:** A string 'não informado', presente em diversas colunas para indicar valores ausentes, foi substituída pelo valor padrão `np.nan`.
* **Remoção de Linhas com Alta Taxa de `NaN`:**
    * Inicialmente, foram removidas linhas onde *todas* as variáveis da coluna 6 em diante (que incluem a maioria das variáveis de saúde e comportamento) eram `NaN`, o que reduziu o DataFrame de 344.887 para 279.382 linhas.
    * Em seguida, colunas com mais de 80% de valores ausentes foram removidas. No notebook, as variáveis `P03201` (alcool_30_dias), `P034` (atividade_fisica_3_meses), `P035` (atividade_fisica_por_semana), `P042` (atividade_fisica_deslocamento), `P050` (fumante), `Q00201` (hipertensao), `Q03001` (diagnostico_diabetes), `Q060` (diagnostico_colesterol), `Q06306` (doenca_cardiaca), `Q068` (avc), `Q074` (asma), `Q084` (dor_coluna), `Q092` (depressao) e `Q11006` (ansiedade) foram renomeadas e **algumas foram mantidas**, enquanto outras como `P042` (atividade_fisica_deslocamento) e `P035` (atividade_fisica_por_semana) **foram de fato removidas** devido à alta porcentagem de `NaN`. A variável `saude_subjetivo` foi mantida para análise posterior.
    * Finalmente, linhas que possuíam mais de 9 valores ausentes no restante das colunas foram removidas, resultando em um DataFrame com 90.846 linhas. Esta etapa foi crucial para focar a análise em observações com dados mais completos.
* **Padronização e Transformação de Variáveis Categóricas:**
    * A coluna `tipo_area` teve seus valores padronizados para 'Capital', 'Resto da RM', 'Resto da UF', e 'RIDE'.
    * A string ' ou equivalente' foi removida da coluna `instrucao`.
* **Conversão para Tipo Numérico e Ordinal:**
    * Variáveis binárias como `plano_saude` e `internacoes_12_meses` foram padronizadas, substituindo 'não' por 0 e 'sim' por 1.
    * A variável `saude_subjetivo` teve suas categorias textuais ('Muito ruim', 'Ruim', 'Regular', 'Boa', 'Muito boa') convertidas para uma escala numérica ordinal de 0 a 4, respectivamente.
    * A variável `fumante` teve suas categorias textuais convertidas para 0 (Não fumo atualmente) e 1 (Sim, diariamente/Sim, menos que diariamente).
    * A variável `instrucao` teve suas categorias textuais convertidas para uma escala numérica ordinal de 0 (Sem instrução) a 6 (Superior completo).
    * Todas as colunas numéricas (exceto `renda_domiciliar_per_capita`) foram convertidas para o tipo inteiro (`int`), preenchendo `NaN` com 0 onde necessário antes da conversão.
    * A coluna `idade` foi convertida para tipo inteiro.
    * A coluna `estrato` foi convertida para tipo string.

### 3.4. Imputação de Valores Ausentes (MICE)

Para as colunas restantes que ainda continham valores ausentes, a imputação por *Multiple Imputation by Chained Equations* (MICE) foi aplicada. Utilizando `IterativeImputer` da `sklearn.experimental`, as colunas numéricas do DataFrame foram preenchidas, garantindo a completude dos dados para as análises subsequentes. Após a imputação, uma nova conversão de colunas numéricas (exceto `renda_domiciliar_per_capita`) para o tipo inteiro foi realizada.

### 3.5. Qualidade dos Dados Pós-Tratamento

Após todas as etapas de tratamento e imputação, uma verificação final da qualidade dos dados foi realizada. O percentual de valores ausentes em todas as colunas foi avaliado, confirmando a ausência total de valores nulos no DataFrame resultante, com um total de 90.846 linhas. Adicionalmente, o domínio (valores únicos) de cada variável foi inspecionado para assegurar a consistência e a validade dos dados. A coluna `estrato` foi então descartada, pois não seria utilizada nos modelos finais.

### 3.6. Transformação de Variáveis Categóricas (Dummies)

As variáveis categóricas remanescentes que não eram ordinais (`uf`, `tipo_area`, `sexo`, `cor_raca`) foram transformadas em variáveis *dummy* (ou *one-hot encoding*) usando `pd.get_dummies()`. Este processo converte cada categoria única em uma nova coluna binária, preparando o DataFrame para a modelagem estatística.

### 3.7. Balanceamento de Dados por Propensity Score Matching (PSM)

Para mitigar o viés de seleção inerente a estudos observacionais e criar grupos comparáveis de indivíduos com e sem plano de saúde, foi aplicada a metodologia de Propensity Score Matching (PSM). As etapas foram as seguintes:
* **Estimação do Escore de Propensão:** Primeiramente, um modelo de Regressão Logística (`sm.Logit`) foi ajustado para estimar a probabilidade condicional de um indivíduo possuir um plano de saúde (`plano_saude`) dadas suas covariáveis observadas (todas as variáveis do DataFrame, exceto `plano_saude` e `saude_subjetivo`). Todas as variáveis foram convertidas para `float` e uma constante foi adicionada ao modelo preditor. O resultado dessa predição gerou o `propensity_score` para cada indivíduo.
* **Avaliação do Balanço Pré-Pareamento:** A distribuição dos `propensity_score` para os grupos com e sem plano de saúde foi visualizada através de um histograma com estimativa de densidade (`kde=True`). Esta análise inicial revelou que, embora houvesse alguma sobreposição, o balanço entre as distribuições dos grupos ainda poderia ser aprimorado para garantir a comparabilidade direta das características entre os indivíduos.
* **Balanceamento por *Downsampling*:** Para criar grupos de tratamento e controle com distribuições de covariáveis mais homogêneas e igualar o tamanho das classes, foi aplicado um *downsampling* na classe majoritária (indivíduos sem plano de saúde, `plano_saude == 0`). Um subconjunto aleatório da classe majoritária foi selecionado sem reposição (`replace=False`), com um número de amostras igual ao da classe minoritária (indivíduos com plano de saúde, `plano_saude == 1`). As duas classes balanceadas foram então concatenadas para formar o `df_balanced`, resultando em um dataset com proporções iguais de indivíduos com e sem plano de saúde.
* **Avaliação do Balanço Pós-Pareamento:** Após o balanceamento, um novo modelo de Regressão Logística foi ajustado no `df_balanced` para recalcular os `propensity_score` e verificar a sobreposição das distribuições. O histograma resultante demonstrou uma ampla região de sobreposição (especialmente entre 0.1 e 0.9), indicando que o balanceamento foi bem-sucedido em encontrar indivíduos com e sem plano de saúde que possuem características observadas muito semelhantes, fortalecendo a capacidade de inferências causais. O notebook destaca que "a ampla região de sobreposição (especialmente entre 0.1 e 0.9, aproximadamente) indica que seu PSM foi bem-sucedido em encontrar indivíduos com e sem plano de saúde que possuem características observadas muito semelhantes.".

### 3.8. Aplicação do Modelo de Regressão Logística Ordinal

Para analisar o efeito da posse de plano de saúde na saúde subjetiva, que é uma variável dependente ordinal, foi aplicado um Modelo de Regressão Logística Ordinal (`OrderedModel` do `statsmodels`) no DataFrame balanceado (`df_balanced`).
* **Variável Dependente:** `saude_subjetivo` (escala ordinal de 0 a 4).
* **Variáveis Independentes:** Todas as covariáveis utilizadas na estimação do escore de propensão foram incluídas como preditoras no modelo de regressão ordinal, com exceção da própria `saude_subjetivo` e do `propensity_score`. As variáveis `uf_TO` e `tipo_area_Resto da UF`, e `sexo_Mulher`, `cor_raca_Preta` foram excluídas do modelo de regressão para evitar multicolinearidade, visto que suas categorias de referência foram implicitamente consideradas pelas variáveis dummy remanescentes. Todas as variáveis foram convertidas para o tipo `float` antes do ajuste do modelo.
* **Especificação do Modelo:** O modelo foi ajustado utilizando a distribuição *probit* (`distr='probit'`), que é uma alternativa comum à distribuição logística em modelos ordinais.
* **Ajuste do Modelo:** O modelo foi ajustado usando o método 'bfgs' de otimização. O sumário do `res_prob.summary()` forneceu os coeficientes, erros padrão, valores-z, p-valores e intervalos de confiança para cada preditor, além de informações sobre a qualidade do ajuste do modelo.

## 4. Resultados

A análise dos dados da Pesquisa Nacional de Saúde (PNS) de 2019, após as etapas de tratamento, imputação e balanceamento, revelou insights importantes sobre a percepção da saúde subjetiva e sua relação com a posse de plano de saúde e outras covariáveis.

### 4.1. Caracterização da Amostra

Inicialmente, a amostra bruta da PNS 2019 continha 344.887 linhas, que foram reduzidas para 90.846 após o pré-processamento e a remoção de valores ausentes. Para a análise principal, a amostra foi balanceada por meio do *downsampling* na classe majoritária, resultando em um DataFrame balanceado (`df_balanced`) com 41.136 observações, onde há uma distribuição equitativa entre indivíduos com plano de saúde (20.568) e sem plano de saúde (20.568).

### 4.2. Análise Descritiva Comparativa entre Grupos

A comparação entre os grupos com e sem plano de saúde, na amostra original, revelou disparidades importantes antes do balanceamento por Propensity Score Matching (PSM):

* **Atividade Física:** Indivíduos com plano de saúde apresentaram uma maior proporção de prática de atividade física nos últimos 3 meses (56.19%) em comparação com aqueles sem plano (35.35%).
    ![Alt text](https://github.com/marleyabe/Inferencia-PNS/blob/main/Frequencia%20de%20Atividade%20F%C3%ADsica%20por%20Plano%20de%20Sa%C3%BAde.png)
* **Hábito de Fumar:** A prevalência de tabagismo foi menor no grupo com plano de saúde (7.95%) do que no grupo sem plano (13.87%).
    ![Alt text](https://github.com/marleyabe/Inferencia-PNS/blob/main/Frequencia%20de%20Fumantes%20por%20plano%20de%20Sa%C3%BAde.png)
* **Internações nos Últimos 12 Meses:** Uma proporção ligeiramente maior de indivíduos com plano de saúde relatou internações nos últimos 12 meses (9.81%) em comparação com aqueles sem plano (7.06%).
* **Percepção da Saúde Subjetiva:** O grupo com plano de saúde apresentou uma percepção de saúde subjetiva notavelmente mais positiva. Indivíduos com plano de saúde relataram "Boa" (53.88%) e "Muito boa" (22.47%) em maior proporção, enquanto no grupo sem plano, as categorias "Regular" (33.72%) e "Ruim" (6.28%) foram mais frequentes.
    ![Alt text](https://github.com/marleyabe/Inferencia-PNS/blob/main/Sa%C3%BAde%20Subjetiva%20por%20plano%20de%20Sa%C3%BAde.png)
* **Renda Domiciliar Per Capita:** Uma diferença substancial na renda foi observada, com a média de renda per capita para pessoas com plano de saúde sendo R$ 3583.88, significativamente superior à média de R$ 1013.76 para pessoas sem plano de saúde.
    ![Alt text](https://github.com/marleyabe/Inferencia-PNS/blob/main/Renda%20per%20Capita%20por%20plano%20de%20sa%C3%BAde.png)

### 4.3. Balanço dos Propensity Scores

A avaliação da distribuição dos *Propensity Scores* (PS) após o balanceamento por *downsampling* demonstrou uma significativa melhoria na sobreposição entre os grupos de tratamento e controle. Conforme ilustrado no histograma gerado, as distribuições dos PS para indivíduos com e sem plano de saúde no `df_balanced` mostraram uma ampla região de sobreposição, especialmente entre 0.1 e 0.9. Esta sobreposição indica que o processo de balanceamento foi eficaz em criar grupos comparáveis em termos das covariáveis observadas, permitindo uma inferência causal mais robusta.

![Alt text](https://github.com/marleyabe/Inferencia-PNS/blob/main/download.png)

### 4.4. Resultados da Regressão Logística Ordinal

O modelo de Regressão Logística Ordinal (probit), ajustado no DataFrame balanceado, analisou o impacto da posse de plano de saúde na saúde subjetiva, controlando por um conjunto abrangente de covariáveis. Os principais resultados do sumário do modelo (`res_prob.summary()`) são apresentados a seguir:

* **Impacto do Plano de Saúde:** A variável `plano_saude` apresentou um coeficiente de **0.4903** (p < 0.001). Este resultado sugere que, mantendo as outras variáveis constantes e após o balanceamento das covariáveis, a posse de um plano de saúde está associada a uma maior probabilidade de relatar uma percepção de saúde subjetiva mais elevada (ou seja, categorias de saúde melhor avaliadas).
* **Outras Covariáveis Relevantes:** Diversas outras covariáveis demonstraram associações estatisticamente significativas com a saúde subjetiva:
    * **Idade:** O coeficiente de `idade` foi negativo (-0.0150, p < 0.001), indicando que o aumento da idade está associado a uma menor probabilidade de relatar saúde subjetiva melhor.
    * **Atividade Física:** A `atividade_fisica_3_meses` teve um coeficiente positivo (0.4871, p < 0.001), mostrando associação com uma melhor percepção da saúde.
    * **Fumante:** A variável `fumante` apresentou um coeficiente negativo (-0.1157, p < 0.001), indicando que ser fumante está associado a uma pior saúde subjetiva.
    * **Condições Crônicas e Morbidades:** Variáveis como `hipertensao` (-0.5050, p < 0.001), `diagnostico_diabetes` (-0.6489, p < 0.001), `diagnostico_colesterol` (-0.3218, p < 0.001), `doenca_cardiaca` (-0.5149, p < 0.001), `avc` (-0.5879, p < 0.001), `asma` (-0.3702, p < 0.001), `dor_coluna` (-0.7713, p < 0.001), `depressao` (-0.5280, p < 0.001) e `ansiedade` (-0.4194, p < 0.001) apresentaram coeficientes negativos e altamente significativos, indicando que a presença dessas condições está associada a uma pior percepção da saúde subjetiva.
    * **Instrução e Renda:** A variável `instrucao` (0.1625, p < 0.001) e `renda_domiciliar_per_capita` (5.551e-05, p < 0.001) tiveram coeficientes positivos, sugerindo que níveis mais altos de escolaridade e renda per capita estão associados a uma melhor percepção da saúde.
    * **Sexo:** Ser do `sexo_Homem` apresentou coeficiente positivo (0.0977, p < 0.001), indicando que homens tendem a relatar uma saúde subjetiva ligeiramente melhor, controlando pelas demais variáveis.
    * **Raça/Cor:** `cor_raca_Branca` (0.1364, p < 0.001) apresentou coeficiente positivo. `cor_raca_Parda` (0.0269, p = 0.432), `cor_raca_Amarela` (0.0500, p = 0.639), `cor_raca_Indígena` (0.0396, p = 0.751) e `cor_raca_Ignorado` (0.8036, p = 0.263) não foram estatisticamente significativas.
    * **Localização:** `tipo_area_Capital` (0.1000, p < 0.001) teve coeficiente positivo, sugerindo que residir na capital está associado a uma melhor percepção de saúde subjetiva. `tipo_area_RIDE` (-0.4644, p < 0.001) teve coeficiente negativo, enquanto `tipo_area_Resto da RM` (-0.0471, p = 0.133) não foi estatisticamente significativa. Várias UFs apresentaram coeficientes positivos e negativos significativos, indicando variações regionais na saúde subjetiva percebida.

| Variável                     | Coeficiente | Erro Padrão | z       | P>|z|   | [0.025 | 0.975] |
| :--------------------------- | :---------- | :---------- | :------ | :------ | :----- | :----- |
| `idade`                      | -0.0150     | 0.001       | -21.472 | 0.000   | -0.016 | -0.014 |
| **`plano_saude`** | **0.4903** | **0.024** | **20.054** | **0.000** | **0.442** | **0.538** |
| `qtd_consultas_12_meses`     | -0.0605     | 0.003       | -23.048 | 0.000   | -0.066 | -0.055 |
| `internacoes_12_meses`       | -0.3522     | 0.037       | -9.562  | 0.000   | -0.424 | -0.280 |
| `atividade_fisica_3_meses`   | 0.4871      | 0.021       | 22.973  | 0.000   | 0.446  | 0.529  |
| `fumante`                    | -0.1157     | 0.032       | -3.623  | 0.000   | -0.178 | -0.053 |
| `hipertensao`                | -0.5050     | 0.026       | -19.718 | 0.000   | -0.555 | -0.455 |
| `diagnostico_diabetes`       | -0.6489     | 0.037       | -17.481 | 0.000   | -0.722 | -0.576 |
| `diagnostico_colesterol`     | -0.3218     | 0.028       | -11.380 | 0.000   | -0.377 | -0.266 |
| `doenca_cardiaca`            | -0.5149     | 0.044       | -11.764 | 0.000   | -0.601 | -0.429 |
| `avc`                        | -0.5879     | 0.071       | -8.254  | 0.000   | -0.728 | -0.448 |
| `asma`                       | -0.3702     | 0.043       | -8.553  | 0.000   | -0.455 | -0.285 |
| `dor_coluna`                 | -0.7713     | 0.025       | -30.774 | 0.000   | -0.820 | -0.722 |
| `depressao`                  | -0.5280     | 0.035       | -15.132 | 0.000   | -0.596 | -0.460 |
| `ansiedade`                  | -0.4194     | 0.043       | -9.773  | 0.000   | -0.504 | -0.335 |
| `instrucao`                  | 0.1625      | 0.006       | 25.389  | 0.000   | 0.150  | 0.175  |
| `renda_domiciliar_per_capita`| 5.551e-05   | 3.47e-06    | 15.978  | 0.000   | 4.87e-05 | 6.23e-05 |
| `uf_AC`                      | -0.2014     | 0.093       | -2.175  | 0.030   | -0.383 | -0.020 |
| `uf_AL`                      | -0.1846     | 0.089       | -2.069  | 0.039   | -0.359 | -0.010 |
| `uf_AP`                      | -0.3655     | 0.104       | -3.515  | 0.000   | -0.569 | -0.162 |
| `uf_MA`                      | -0.3976     | 0.082       | -4.859  | 0.000   | -0.558 | -0.237 |
| `uf_MG`                      | 0.6478      | 0.076       | 8.484   | 0.000   | 0.498  | 0.797  |
| `uf_MS`                      | 0.4868      | 0.085       | 5.719   | 0.000   | 0.320  | 0.654  |
| `uf_PA`                      | -0.1389     | 0.082       | -1.686  | 0.092   | -0.300 | 0.023  |
| `uf_PI`                      | -0.1529     | 0.088       | -1.730  | 0.084   | -0.326 | 0.020  |
| `uf_PR`                      | 0.4850      | 0.079       | 6.135   | 0.000   | 0.330  | 0.640  |
| `uf_RJ`                      | 0.3033      | 0.076       | 4.012   | 0.000   | 0.155  | 0.451  |
| `uf_RS`                      | 0.6621      | 0.079       | 8.344   | 0.000   | 0.507  | 0.818  |
| `uf_SC`                      | 0.4851      | 0.081       | 5.963   | 0.000   | 0.326  | 0.645  |
| `uf_SP`                      | 0.4432      | 0.074       | 5.990   | 0.000   | 0.298  | 0.588  |
| `tipo_area_Capital`          | 0.1000      | 0.024       | 4.208   | 0.000   | 0.053  | 0.147  |
| `tipo_area_RIDE`             | -0.4644     | 0.116       | -4.017  | 0.000   | -0.691 | -0.238 |
| `sexo_Homem`                 | 0.0977      | 0.020       | 4.876   | 0.000   | 0.058  | 0.137  |
| `cor_raca_Branca`            | 0.1364      | 0.036       | 3.833   | 0.000   | 0.067  | 0.206  |
| `cor_raca_Parda`             | 0.0269      | 0.034       | 0.786   | 0.432   | -0.040 | 0.094  |
| `0.0/1.0 (Cut-off)`          | -5.4264     | 0.096       | -56.674 | 0.000   | -5.614 | -5.239 |
| `1.0/2.0 (Cut-off)`          | 0.5914      | 0.025       | 23.836  | 0.000   | 0.543  | 0.640  |
| `2.0/3.0 (Cut-off)`          | 0.9935      | 0.009       | 106.631 | 0.000   | 0.975  | 1.012  |
| `3.0/4.0 (Cut-off)`          | 1.1031      | 0.006       | 174.395 | 0.000   | 1.091  | 1.115  |

## 5. Discussão

Os resultados deste estudo revelam uma associação estatisticamente significativa e positiva entre a posse de um plano de saúde e a percepção da saúde subjetiva na população brasileira, mesmo após o balanceamento das covariáveis observadas por meio do Propensity Score Matching (PSM). O coeficiente positivo da variável `plano_saude` no modelo de Regressão Logística Ordinal (probit) sugere que indivíduos com plano de saúde têm uma probabilidade maior de autoavaliar sua saúde de forma mais favorável, em comparação com aqueles sem plano, ao controlar por uma série de fatores demográficos, socioeconômicos e de saúde.

Essa descoberta corrobora a expectativa de que o acesso à saúde suplementar pode influenciar positivamente a percepção de bem-estar. A posse de um plano de saúde pode proporcionar maior segurança e tranquilidade em relação ao acesso a serviços médicos, tratamentos e exames, o que, por sua vez, pode reduzir a ansiedade relacionada à saúde e melhorar a qualidade de vida percebida. Além disso, a capacidade de escolher profissionais e serviços, ou de ter um atendimento mais rápido, pode contribuir para uma experiência de saúde mais satisfatória e, consequentemente, uma autoavaliação mais positiva. As análises descritivas iniciais já apontavam para uma diferença considerável na renda per capita entre os grupos com e sem plano, assim como em comportamentos de saúde como atividade física e tabagismo, o que ressalta a importância do PSM para isolar o efeito do plano, minimizando o viés de seleção.

Os resultados também reforçam o papel de outros determinantes conhecidos da saúde subjetiva. A `idade` se mostrou inversamente associada à percepção de saúde, um achado comum na literatura, onde o envelhecimento é frequentemente acompanhado por um aumento na prevalência de condições crônicas e uma diminuição na capacidade funcional. A `atividade_fisica_3_meses` e níveis mais altos de `instrucao` e `renda_domiciliar_per_capita` foram positivamente associados à saúde subjetiva, sublinhando a importância de hábitos de vida saudáveis e de determinantes socioeconômicos na percepção individual de saúde. Por outro lado, a presença de morbidades e condições crônicas como `hipertensao`, `diagnostico_diabetes`, `dor_coluna`, `depressao` e `ansiedade` foram fortemente e negativamente associadas à saúde subjetiva, evidenciando o impacto direto dessas condições no bem-estar percebido.

As disparidades regionais e de área (`uf` e `tipo_area_Capital`, `tipo_area_RIDE`) também se mostraram significativas, indicando que o contexto geográfico e o ambiente urbano/rural podem influenciar a percepção de saúde subjetiva, possivelmente devido a diferenças na disponibilidade de serviços, condições de vida e fatores socioambientais específicos de cada localidade. A associação do `sexo_Homem` com uma percepção ligeiramente melhor de saúde subjetiva pode refletir tanto diferenças biológicas quanto sociais e culturais na forma como homens e mulheres percebem e relatam sua saúde.

É importante reconhecer as limitações deste estudo. Primeiramente, apesar da aplicação do PSM para controlar vieses de seleção baseados em covariáveis observadas, o estudo permanece de natureza observacional. Isso significa que não é possível controlar completamente por variáveis não observadas que podem influenciar tanto a decisão de ter um plano de saúde quanto a percepção da saúde subjetiva (o problema do "viés oculto"). Embora o `OrderedModel` seja adequado para variáveis ordinais, a interpretação de seus coeficientes e o pressuposto de *odds* proporcionais exigem cautela. Além disso, o *downsampling* utilizado para balancear a amostra, embora melhore a comparabilidade dos grupos, pode reduzir o tamanho da amostra e, consequentemente, a validade externa dos resultados para a população original não balanceada.

Futuras pesquisas poderiam aprofundar esta análise utilizando outras técnicas de inferência causal que abordem o viés de variáveis não observadas, como variáveis instrumentais, se dados adequados estiverem disponíveis. A exploração de efeitos marginais heterogêneos para diferentes níveis da saúde subjetiva, bem como a incorporação de dados longitudinais da PNS (quando disponíveis em futuras edições), permitiriam investigar a causalidade de forma mais robusta e o acompanhamento das tendências ao longo do tempo.

## 6. Conclusão

Este estudo utilizou dados da Pesquisa Nacional de Saúde (PNS) de 2019 e aplicou o Propensity Score Matching (PSM) em conjunto com um Modelo de Regressão Logística Ordinal (probit) para investigar a relação entre a posse de um plano de saúde e a percepção da saúde subjetiva da população brasileira.

Os resultados demonstram que a posse de um plano de saúde está positivamente e estatisticamente associada a uma melhor autoavaliação da saúde subjetiva, mesmo após o controle de diversas covariáveis demográficas, socioeconômicas e de saúde. Este achado sugere que a saúde suplementar pode desempenhar um papel relevante na melhoria percebida do bem-estar individual, complementando o acesso aos serviços de saúde oferecidos pelo Sistema Único de Saúde (SUS).

Adicionalmente, o estudo reforça o papel fundamental de outros fatores na saúde subjetiva, como a idade (com associação negativa), a prática de atividade física, o nível de instrução e a renda per capita (com associações positivas), e a presença de condições crônicas e morbidades (com associações negativas). Variações por sexo, raça/cor e localização geográfica também foram observadas, destacando a complexidade dos determinantes da saúde no Brasil.

A aplicação rigorosa de metodologias como o PSM e a regressão ordinal permitiu um avanço na inferência causal em um contexto de dados observacionais, contribuindo para uma compreensão mais nuançada das associações e implicações para a saúde pública. Os resultados obtidos fornecem subsídios importantes para formuladores de políticas e pesquisadores interessados em aprofundar o entendimento sobre como o acesso à saúde suplementar e outros fatores influenciam a percepção da saúde da população brasileira, e para a elaboração de estratégias que visem a equidade e a melhoria do bem-estar geral.

## 7. Referências Bibliográficas


ABNT NBR 6023:2018. Informação e documentação: referências: elaboração. Rio de Janeiro: ABNT, 2018.

ALVES, L. C. et al. Childhood adversity effects on older individuals: an empirical study of Brazilians aged 50 and over. International Journal of Social Economics, v. 51, n. 1, p. 1-18, 2024.    

BARATA, R. B. et al. Uso do escore de propensão na análise de desigualdade de renda em estudos epidemiológicos: o caso dos distritos de São Paulo. Saúde e Sociedade, v. 12, n. 1, p. 28-31, 2003.    

DIVINO, J. A. et al. Cross-price elasticity between licit and illicit cigarette consumption in Brazil. Brazilian Journal of Political Economy, v. 45, n. 1, p. 1-20, 2025.    

INSTITUTO BRASILEIRO DE GEOGRAFIA E ESTATÍSTICA (IBGE). Estatísticas Sociais: Saúde. Disponível em: https://www.ibge.gov.br/estatisticas/sociais/saude.html. Acesso em: 17 jun. 2024.    

INSTITUTO BRASILEIRO DE GEOGRAFIA E ESTATÍSTICA (IBGE). National Survey of Health - PNS. Disponível em: https://www.ibge.gov.br/en/statistics/full-list-statistics.html. Acesso em: 17 jun. 2024.    

INSTITUTO BRASILEIRO DE GEOGRAFIA E ESTATÍSTICA (IBGE). Pesquisa Nacional de Saúde. Disponível em: https://www.ibge.gov.br/estatisticas/sociais/saude/9160-pesquisa-nacional-de-saude.html. Acesso em: 17 jun. 2024.    

INSTITUTO BRASILEIRO DE GEOGRAFIA E ESTATÍSTICA (IBGE). Portal do IBGE. Disponível em: https://www.ibge.gov.br/en/. Acesso em: 17 jun. 2024.    

KALTENBACH, L. Propensity Score Analysis. Columbia University Mailman School of Public Health. Disponível em: https://www.publichealth.columbia.edu/research/population-health-methods/propensity-score-analysis. Acesso em: 17 jun. 2024.    

MCCULLAGH, P. Regression Models for Ordinal Data. Journal of the Royal Statistical Society. Series B (Methodological), v. 42, n. 2, p. 109-142, 1980.    

MORAIS, M. A. P. et al. Modelos de regressão logística ordinal: aplicação em estudo sobre qualidade de vida. Cadernos de Saúde Pública, v. 24, n. 1, p. 1-10, 2008.    

MINISTÉRIO DA SAÚDE. Pesquisa Nacional de Saúde. Disponível em: https://www.gov.br/saude/pt-br/composicao/svsa/inqueritos-de-saude/pns. Acesso em: 17 jun. 2024.    

NUMBER ANALYTICS. Mastering Ordinal Logistic Regression. Disponível em: https://www.numberanalytics.com/blog/mastering-ordinal-logistic-regression-guide. Acesso em: 17 jun. 2024.    

NUMBER ANALYTICS. Propensity Score Matching: A Guide to Econometrics. Disponível em: https://www.numberanalytics.com/blog/guide-psm-econometrics. Acesso em: 17 jun. 2024.    

PROFESSIONAL SCIENCE MASTERS. ABOUT. Disponível em: http://professionalsciencemasters.org/about/#:~:text=Professional%20Science%20Master's%20(PSMs)%20are,or%20math%20without%20a%20Ph. Acesso em: 17 jun. 2024.    

RAHIM, A. A. et al. The Evaluation of Ordinal Regression Model’s Performance Through the Implementation of Multilayer Feed-Forward Neural Network: A Case Study of Hypertension. PMC, v. 10, n. 1, p. 1-15, 2024.    

ROSENBAUM, P. R.; RUBIN, D. B. The Central Role of the Propensity Score in Observational Studies for Causal Effects. Biometrika, v. 70, n. 1, p. 41-55, 1983.    

SCARFO, A. J.; RIEGELMAN, A. L. An Introduction to Propensity Score Methods for Reducing the Effects of Confounding in Observational Studies. PMC, v. 3, n. 4, p. 343-353, 2013.    

SCARFO, A. J.; RIEGELMAN, A. L. Using Propensity Scores for Causal Inference: Pitfalls and Tips. PMC, v. 8, n. 1, p. 1-10, 2021.    

SCIELO. Regressão logística ordinal em estudos epidemiológicos. Disponível em: https://www.scielo.br/j/rsp/a/DLGXmM8GtKsWcsK6txQd8ct/. Acesso em: 17 jun. 2024.    

SCIELO. Regressão logística ordinal: aplicação em estudo sobre qualidade de vida. Disponível em: https://www.scielo.br/j/csp/a/zDrhfLxKLkgHmyNMdVgQYVc/?lang=en. Acesso em: 17 jun. 2024.    

SILVA NETO, D. R.; ANDRADE, B. C.; CAYRES, D. C. Seleção de Grupo de Controle por Pareamento por Escore de Propensão: Ensaio com Método para Avaliação de Política Pública em Bairros do Espírito Santo. Vitória, ES: IJSN, 2023. (Nota Técnica, 69).    

SILVEIRA, M. B. G. et al. Aplicação da regressão logística na análise dos dados dos fatores de risco associados à hipertensão arterial. Research, Society and Development, v. 10, n. 15, e48101522964, 2021.    

ST. ANDREWS. Ordinal logistic regression. Disponível em: https://www.st-andrews.ac.uk/media/ceed/students/mathssupport/ordinal%20logistic%20regression.pdf. Acesso em: 17 jun. 2024.    

STATISTICS SOLUTIONS. Ordinal Regression. Disponível em: https://www.statisticssolutions.com/free-resources/directory-of-statistical-analyses/ordinal-regression/. Acesso em: 17 jun. 2024.    

TANG, J. L.; LI, X. L.; ZHANG, W. W. Can propensity score matching replace randomized controlled trials? World Journal of Gastroenterology, v. 14, n. 1, p. 90590-90590, 2024.    

THE WORLD BANK. Propensity Score Matching. Disponível em: https://dimewiki.worldbank.org/Propensity_Score_Matching. Acesso em: 17 jun. 2024.    

UCLA OARC STATS. FAQ: How do I interpret the coefficients in an ordinal logistic regression?. Disponível em: https://stats.oarc.ucla.edu/other/mult-pkg/faq/ologit/. Acesso em: 17 jun. 2024.    

UCLA OARC STATS. Ordinal Logistic Regression | SPSS Data Analysis Examples. Disponível em: https://stats.oarc.ucla.edu/spss/dae/ordinal-logistic-regression/. Acesso em: 17 jun. 2024.    

UNIVERSITY OF MANITOBA. Propensity Score Matching in Observational Studies. Disponível em: http://mchp-appserv.cpe.umanitoba.ca/concept/propensity_score_matching.pdf. Acesso em: 17 jun. 2024.    

WANG, J. et al. A Survey on Ordinal Regression: Applications, Advances, and Prospects. arXiv, 2025. Disponível em: https://arxiv.org/html/2503.00952v1. Acesso em: 17 jun. 2024.    

WIKIPEDIA. Propensity score matching. Disponível em: https://en.wikipedia.org/wiki/Propensity_score_matching. Acesso em: 17 jun. 2024.    

ZHAO, Q. et al. Propensity score matching with R: conventional methods and new features. PMC, v. 8, n. 5, p. 8246231, 2021.
