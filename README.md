UNIVERSIDADE PRESBITERIANA MACKENZIE







PREVISÃO DE CRESCIMENTO E MENSURAÇÃO DO EFEITO DE SUBSTITUIÇÃO DO PIX SOBRE OS MEIOS DE PAGAMENTO CONCORRENTES NO BRASIL











CAINÃ FERNANDES GUIMARÃES DA SILVA
GABRIEL DE OLIVEIRA MELONI
HUMBERTO GUTTAU BRAVO
JIMMY PAIVA GOMES






















São Paulo
2026
CAINÃ FERNANDES GUIMARÃES DA SILVA
GABRIEL DE OLIVEIRA MELONI
HUMBERTO GUTTAU BRAVO
JIMMY PAIVA GOMES





PREVISÃO DE CRESCIMENTO E MENSURAÇÃO DO EFEITO DE SUBSTITUIÇÃO DO PIX SOBRE OS MEIOS DE PAGAMENTO CONCORRENTES NO BRASIL














Trabalho de dissertação apresentado ao curso de ciência de dados da Universidade Presbiteriana Mackenzie, como requisito parcial da matéria de projeto aplicado IV













São Paulo
2026
LISTA DE TABELAS


























































LISTA DE ILUSTRAÇÕES

Figura 1: Cronograma do projeto	8


























































SUMÁRIO
1. INTRODUÇÃO	6
2. MOTIVAÇÕES E JUSTIFICATIVA	6
3. OBJETIVO	8
4. CRONOGRAMA DO PROJETO	8
5. REPOSITÓRIO DO PROJETO	8
6. DESCRIÇÃO DA BASE DE DADOS	9
REFERÊNCIAS	10





























 INTRODUÇÃO
O Pix, sistema de pagamentos instantâneos lançado pelo Banco Central do Brasil (BCB) em novembro de 2020, tornou-se em poucos anos um dos principais meios de pagamento eletrônico do país, alterando de forma substancial a dinâmica de uso de instrumentos já consolidados como boletos bancários, cheques, transferências eletrônicas (TED/DOC) e cartões de crédito e débito. A literatura recente destaca que sua criação esteve associada à digitalização dos pagamentos e a mudanças na estrutura competitiva do mercado financeiro (SCHAPIRO; MOUALLEM; DANTAS, 2023; FERREIRA, 2022). Este projeto se insere na área de Ciência de Dados aplicada a séries temporais financeiras, com foco na modelagem estatística de adoção tecnológica e na quantificação de efeitos de substituição entre instrumentos de pagamento concorrentes.
A relevância do tema ultrapassa o interesse acadêmico. Em 2025, o Escritório do Representante Comercial dos Estados Unidos (USTR) iniciou uma investigação sob a Seção 301 do Trade Act de 1974 contra práticas comerciais brasileiras, incluindo explicitamente os serviços de pagamento eletrônico (USTR, 2025). O relatório de determinação, publicado em 2026, argumenta que o Pix prejudica a competitividade de empresas norte-americanas do setor de pagamentos ao operar como iniciativa regulada e ao mesmo tempo operada pelo próprio Banco Central (USTR, 2026). Como consequência dessa disputa comercial, tarifas foram aplicadas a produtos brasileiros exportados aos Estados Unidos.
Entretanto, dados setoriais recentes sugerem uma relação mais complexa do que a de simples substituição. Segundo a Associação Brasileira das Empresas de Cartões de Crédito e Serviços (Abecs), o setor de cartões encerrou 2025 com R$ 4,5 trilhões movimentados, crescimento de 10,1% em relação a 2024, com destaque para o cartão de crédito, que avançou 14,5% no período (CNN BRASIL, 2026). Esse comportamento é consistente com a hipótese de que o Pix atuou como vetor de bancarização, ampliando o acesso da população a contas digitais e, indiretamente, ao próprio mercado de cartões, ao mesmo tempo em que substituiu diretamente instrumentos mais simples de transferência, como boletos, cheques e TED.
O problema selecionado por este grupo é, portanto: em que medida o Pix efetivamente substituiu cada um dos meios de pagamento concorrentes, e em que medida ele os complementou, ao invés de substituir, por meio da expansão da base de usuários bancarizados?
MOTIVAÇÕES E JUSTIFICATIVA
A literatura recente já documenta efeitos distintos do Pix sobre diferentes instrumentos de pagamento, reforçando a necessidade de investigar quantitativamente a relação de substituição ou complementaridade entre os meios. Sampaio e Ornelas (2024), por exemplo, encontram evidências de complementaridade entre o Pix e pagamentos por cartão, enquanto Balan, Klotzle e Norden (2026) identificam efeitos associados à inclusão financeira e à substituição do uso de dinheiro em espécie. Nesse contexto, permanece relevante uma abordagem quantitativa e reprodutível que isole o efeito do Pix da tendência natural de cada série. A lacuna metodológica motiva o presente projeto: propõe-se aplicar técnicas de análise de intervenção em séries temporais para estimar, de forma independente e replicável, a magnitude do efeito do Pix sobre cada instrumento concorrente — testando especificamente a hipótese de que esse efeito é heterogêneo, sendo de substituição para uns instrumentos e de complementaridade (bancarização) para outros.
A análise exploratória preliminar já realizada pela equipe sobre a série de transações Pix (novembro de 2020 a julho de 2026) fornece um primeiro indício empírico favorável à hipótese de bancarização: o ticket médio por transação (valor total dividido pela quantidade de transações) caiu de aproximadamente R$ 880 em novembro de 2020 para cerca de R$ 400 em 2023, estabilizando-se em um platô entre R$ 380 e R$ 450 a partir de então. Essa trajetória é compatível com uma primeira fase de incorporação de novos usuários e novos casos de uso de menor valor, seguida de maturação do padrão de uso — achado detalhado no notebook de análise exploratória que acompanha este documento.
O projeto contribui para o Objetivo de Desenvolvimento Sustentável 8 (Trabalho Decente e Crescimento Econômico) e para o Objetivo 9 (Indústria, Inovação e Infraestrutura), ao produzir uma análise quantitativa e de acesso público sobre a infraestrutura de pagamentos digitais brasileira — tema de relevância direta para formuladores de política pública, instituições financeiras e para o debate comercial internacional em curso. A publicação aberta do código e dos resultados no GitHub, conforme exigido pelo caráter extensionista da disciplina, permite que a metodologia seja replicada para outros países que adotaram ou pretendem adotar sistemas de pagamento instantâneo semelhantes.
Do ponto de vista de aplicabilidade, o método proposto (análise contrafactual via ARIMAX de intervenção, combinada com testes de causalidade de Granger e detecção de pontos de mudança estrutural) não se limita ao caso do Pix — constitui uma metodologia geral para avaliar o impacto de qualquer inovação tecnológica disruptiva sobre séries temporais de mercado, sendo replicável para outras questões de política pública e de estratégia empresarial.
 OBJETIVO
Modelar a trajetória de adoção do Pix e mensurar seu efeito sobre os principais meios de pagamento concorrentes no Brasil (boleto bancário, cheque, TED/DOC e cartões de crédito e débito), por meio de:
a) previsão da série de volume e quantidade de transações Pix via modelos ARIMA/SARIMA — etapa já iniciada, com modelo base SARIMA(0,1,0)(0,1,1,12) ajustado e validado sobre a série do Pix;
b) construção de cenários contrafactuais (ARIMAX com variável de intervenção) para cada instrumento concorrente, comparando a trajetória projetada sem o Pix com a trajetória real observada;
c) confirmação estatística do efeito estimado por meio de testes de causalidade de Granger e detecção de pontos de mudança estrutural (change point detection).

CRONOGRAMA DO PROJETO
Figura 1: Cronograma do projeto

Fonte: Autoral 
REPOSITÓRIO DO PROJETO
Para o projeto, foi disponibilizado o seguinte repositório no github:

 DESCRIÇÃO DA BASE DE DADOS
São utilizadas exclusivamente fontes primárias e públicas do Banco Central do Brasil, disponibilizadas em formato aberto (JSON) via API OData (plataforma Olinda), sem necessidade de autenticação. Até o momento da elaboração deste documento, quatro bases foram identificadas, das quais três já foram efetivamente coletadas e validadas:
a) Estatísticas de Transações Pix (endpoint EstatisticasTransacoesPix): série mensal de novembro de 2020 a julho de 2026 (69 observações), com granularidade de microdados por combinação de 9 variáveis categóricas (tipo de pagador/recebedor, região, faixa etária, forma de iniciação, natureza e finalidade), agregada para quantidade e valor total de transações por mês. Disponível em: https://dadosabertos.bcb.gov.br/dataset/pix.
b) Meios de Pagamento Mensal (endpoint MeiosdePagamentosMensalDA): série mensal de novembro de 2020 a julho de 2026 (69 observações), consolidando em uma única tabela a quantidade e o valor de Pix, TED, cheque, boleto e DOC. Constatou-se que as colunas referentes a DOC apresentam valor zero em todo o período, consistente com a descontinuação desse instrumento próxima ao período de lançamento do Pix. Disponível em: https://dadosabertos.bcb.gov.br/dataset/estatisticas-meios-pagamentos.
c) Quantidade e Transações de Cartões (endpoint Quantidadeetransacoesdecartoes): série trimestral do 4º trimestre de 2020 ao 1º trimestre de 2026 (22 observações), com dados de estoque e de transações de cartões de crédito e débito.
d) Meios de Pagamento Trimestral (endpoint MeiosdePagamentosTrimestralDA): destinada a complementar a série de cartões com granularidade adicional. Todas as tentativas de acesso a este endpoint retornaram erro 500 (Internal Server Error) diretamente do servidor do Banco Central, para os 22 trimestres testados, o que configura indisponibilidade do lado do provedor de dados, não falha de implementação da equipe. Esta fonte permanece como pendência técnica, a ser resolvida por nova tentativa em momento de menor instabilidade do serviço ou substituída por fonte consolidada equivalente da Abecs, se necessário.
O processo completo de coleta — incluindo os obstáculos técnicos encontrados (parâmetros obrigatórios não documentados publicamente, limites de tempo de resposta da API, granularidade dos microdados, duplicidade de registros em reexecuções) e as decisões de pré-processamento adotadas (tratamento de sazonalidade multiplicativa, normalização por dias no mês, correção de instabilidade numérica na modelagem) — está integralmente documentado, com código reprodutível, no notebook de análise exploratória que acompanha este documento.

REFERÊNCIAS
BALAN, Philipe; KLOTZLE, Marcelo Cabus; NORDEN, Lars. Fast payment systems and deposit dynamics: evidence from Brazil's Pix. [S. l.]: SSRN, 2026. Disponível em: https://doi.org/10.2139/ssrn.6415438. Acesso em: 30 ago. 2026.
BANCO CENTRAL DO BRASIL. Instrução Normativa BCB nº 32, de 26 de outubro de 2020. Dispõe sobre os requisitos de remessa de informações relativas ao arranjo de pagamento Pix. Brasília, DF: BCB, 2020.
BANCO CENTRAL DO BRASIL. Portal de Dados Abertos: Estatísticas de Meios de Pagamento. Brasília, DF: BCB, [2026]. Disponível em: https://dadosabertos.bcb.gov.br/dataset/estatisticas-meios-pagamentos. Acesso em: 30 ago. 2026.
BANCO CENTRAL DO BRASIL. Portal de Dados Abertos: Estatísticas do Pix. Brasília, DF: BCB, [2026]. Disponível em: https://dadosabertos.bcb.gov.br/dataset/pix. Acesso em: 30 ago. 2026.
BANCO CENTRAL DO BRASIL. Relatório de Gestão do Pix 2023-2025. Brasília, DF: BCB, 2026. Disponível em: https://www.bcb.gov.br/detalhenoticia/21227/noticia. Acesso em: 30 ago. 2026.
BANCO CENTRAL DO BRASIL. Resolução BCB nº 1, de 12 de agosto de 2020. Institui o arranjo de pagamentos Pix e aprova o seu Regulamento. Brasília, DF: BCB, 2020. Disponível em: https://www.bcb.gov.br/estabilidadefinanceira/exibenormativo?numero=1&tipo=Resolu%C3%A7%C3%A3o%20BCB. Acesso em: 30 ago. 2026.
CNN BRASIL. Setor de cartões movimenta R$ 4,5 tri em 2025, mostra Abecs. São Paulo, 11 fev. 2026. Disponível em: https://www.cnnbrasil.com.br/economia/macroeconomia/setor-de-cartoes-movimenta-r-45-trilhoes-em-2025-alta-de-101-ante-2024-mostra-abec/. Acesso em: 30 ago. 2026.
FERREIRA, Alexandre Rebêlo. Arranjo Pix: regulação e concorrência em pagamentos digitais. Revista da Procuradoria-Geral do Banco Central, Brasília, DF, v. 16, n. 1, p. 100-113, 2022. DOI: https://doi.org/10.58766/rpgbcb.v16i1.1158. Acesso em: 30 ago. 2026.
SAMPAIO, Matheus C.; ORNELAS, José Renato Haas. Payment technology complementarities and their consequences in the banking sector: evidence from Brazil's Pix. Brasília, DF: Banco Central do Brasil, 2024. (Working Paper Series, n. 600). Disponível em: https://www.bcb.gov.br/publicacoes/workingpaperseries_all. Acesso em: 30 ago. 2026.
SCHAPIRO, Mario G.; MOUALLEM, Pedro Salomon Bezerra; DANTAS, Eric Gil. PIX: explaining a state-owned Fintech. Brazilian Journal of Political Economy, São Paulo, v. 43, n. 4, p. 874-892, 2023. DOI: https://doi.org/10.1590/0101-31572023-3470. Acesso em: 30 ago. 2026.
UNITED STATES TRADE REPRESENTATIVE (USTR). Initiation of Section 301 Investigation: Brazil's Acts, Policies, and Practices Related to Digital Trade and Electronic Payment Services. Federal Register, Washington, DC, 18 jul. 2025. Disponível em: https://www.federalregister.gov/documents/2025/07/18/2025-13498. Acesso em: 30 ago. 2026.
UNITED STATES TRADE REPRESENTATIVE (USTR). Notice of Determination and Request for Comments Concerning Action Pursuant to Section 301: Brazil's Acts, Policies, and Practices Related to Digital Trade and Electronic Payment Services. Federal Register, Washington, DC, 4 jun. 2026. Disponível em: https://www.federalregister.gov/documents/2026/06/04/2026-11158. Acesso em: 30 ago. 2026.
