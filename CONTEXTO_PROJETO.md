# Contexto recuperado do projeto

Recuperado em 13/10/2026 a partir dos arquivos locais, do histórico Git e das saídas salvas no notebook. Este documento permite retomar o desenvolvimento neste dispositivo.

## Alcance e limites

- Repositório: https://github.com/JoaoFerrett/Simple-Linear-Regression.git.
- Branch local: `main`, commit `e91f0aa`. A referência local `origin/main` aponta para o mesmo commit; o servidor remoto não foi consultado nesta recuperação.
- Não havia alterações locais antes da criação deste documento.
- Nenhuma conversa original deste projeto foi identificada nos 50 chats recentes acessíveis; a consulta de chats Codex arquivados retornou vazia. Isso não prova que a conversa não exista no outro dispositivo.
- Decisões tomadas apenas em conversas e arquivos não sincronizados não foram recuperadas.
- Os resultados abaixo foram lidos das saídas salvas. O notebook não foi reexecutado nem alterado nesta recuperação.

## Objetivo e entrega

Disciplina ACH2036 — Métodos Quantitativos para Análise Multivariada. Atividade 1: Modelos de Regressão, análise de resíduos e transformações de escala. Enunciado local na versão de 05/10.

O trabalho exige analisar três conjuntos:

| Conjunto | X (preditor) | Y (resposta) | Origem indicada no enunciado |
| --- | --- | --- | --- |
| Treadwear | mileage | groove | STAT501, seção 4.4 |
| Alligators | length | weight | STAT501, seção 4.7 |
| ConcPatog.txt | CPatog1 | CPatog2 | Pasta datasets do Drive ACH2036_2026 |

Para cada conjunto, fazer análise inicial sem transformação, explorar transformações e repetir a análise completa para a combinação escolhida. A análise completa inclui dispersão, resumo do ajuste, interpretação do R² ajustado, reta com intervalos de confiança e predição, resíduos versus preditos, QQ-plot e avaliação das premissas LINE (linearidade, independência, normalidade e variância constante). O histograma de resíduos é solicitado, com exceção explícita de Treadwear por sua amostra pequena.

Explorar raiz quadrada, quadrado e log10 em X, em Y e em ambas: nove possibilidades. Os gráficos exploratórios não precisam todos entrar no relatório.

Entrega: relatório PDF sem código Python; individual ou em dupla; identificação dos participantes e números USP na primeira página; submissão no e-disciplinas por um integrante. Prazo escrito no enunciado: 13/10.

## Arquivos disponíveis

- `treadwear.ipynb`: notebook principal, com 12 células de código preenchidas e uma célula final vazia; sem células Markdown explicativas.
- `treadwear.txt`: nove observações, separadas por tabulação; mileage de 0 a 32 em passos de 4; groove de 394,33 a 150,33.
- `.ipynb_checkpoints/treadwear-checkpoint.ipynb`: checkpoint versionado.
- `Atividade1 ACH2036 - Ativ1_Enunciado1005.pdf`: enunciado com seis páginas.
- Não foram encontrados dados/notebooks de Alligators ou ConcPatog, relatório final, README ou arquivo de dependências.

## Histórico recuperado

Horários conforme os commits, UTC−03:00.

| Commit | Data/hora | Registro |
| --- | --- | --- |
| a89dd24 | 11/10/2026 15:39 | Criação: enunciado, dados e notebook Untitled |
| 77e751c | 11/10/2026 20:27 | Notebook passa a treadwear.ipynb e recebe desenvolvimento |
| 650d147 | 12/10/2026 03:32 | Ampliação da análise e exploração das transformações |
| e91f0aa | 12/10/2026 03:38 | Mensagem “fixing a bug”; saída de NameError na última comparação substituída por figura válida |

Detalhe da última alteração: o erro salvo mencionava `resultado_raiz_ambas`; no código salvo atual e no anterior, a variável usada já era `result_root_both`. A diferença textual nessa célula é de formatação. O histórico confirma atualização bem-sucedida da saída, mas não permite afirmar que uma correção de nome tenha sido feita nesse commit.

## Desenvolvimento existente

1. Leitura dos dados com pandas e gráfico de dispersão.
2. Regressão linear simples por mínimos quadrados, com intercepto, usando statsmodels.
3. Reta estimada e faixas de confiança e predição de 95%.
4. Tabela de valores observados, preditos e resíduos, e gráfico de resíduos versus preditos.
5. QQ-plot dos resíduos com distribuição normal de referência.
6. Dispersões para raiz em X, raiz em Y e raiz em ambas.
7. Dispersões para quadrado em X, em Y e em ambas.
8. Dispersão e regressão para log10(Y), com gráfico de resíduos.
9. Regressão de Y sobre raiz(X), com resumo e gráfico de resíduos.
10. Ajustes de raiz(Y) sobre X e de raiz(Y) sobre raiz(X), com comparação dos resíduos.

Resultados salvos:

| Modelo | Equação aproximada | R² | R² ajustado |
| --- | --- | --- | --- |
| Original | groove = 360,6367 − 7,2806 × mileage | 0,953 | 0,946 |
| Log em Y | log10(groove) = 2,5736 − 0,0129 × mileage | 0,993 | 0,992 |
| Raiz em X | groove = 408,0836 − 45,2420 × sqrt(mileage) | 0,990 | 0,988 |

As escalas da resposta diferem entre alguns modelos; esses R² não devem ser usados isoladamente para declarar uma transformação vencedora.

O modelo original tem resíduos positivos nas extremidades e negativos no meio, sinal de curvatura. O notebook registra que log em Y melhora visualmente o alinhamento, mas ainda deixa padrão em U nos resíduos. Também registra ressalva de instabilidade para raiz em X. Nenhuma escolha final foi documentada. O último trabalho substantivo foi comparar os resíduos de raiz somente em Y com raiz em ambas.

## Pendências e ponto de retomada

1. Retomar a comparação das transformações de Treadwear e justificar a escolha final a partir dos gráficos e diagnósticos.
2. Tratar explicitamente a limitação de log10(X): mileage contém zero. Não remover a observação ou somar constante silenciosamente; documentar a decisão metodológica.
3. Para a transformação escolhida, produzir todos os itens da etapa 3.1, inclusive reta com intervalos, QQ-plot, interpretação do R² ajustado e discussão das premissas LINE.
4. Escrever as interpretações da análise original e transformada; atualmente predominam código, gráficos e comentários curtos.
5. Corrigir os títulos dos primeiros gráficos nas células de raiz e quadrado: o primeiro `set` usa `axis[1]` quando deveria usar `axis[0]`. A configuração é depois sobrescrita pelo título do segundo gráfico.
6. Reexecutar o notebook em ordem antes de utilizar as saídas no relatório. Existe uma saída “teste” sem comando correspondente no código atual da célula de QQ-plot, evidência de saída desatualizada.
7. Obter os dados de Alligators e ConcPatog e realizar as respectivas análises, incluindo histogramas conforme o enunciado.
8. Montar e revisar o relatório PDF final, sem código, com identificação dos participantes.

Essas pendências resultam da comparação do enunciado com os arquivos disponíveis; não são decisões recuperadas de uma conversa anterior.

## Ambiente para continuidade

Bibliotecas importadas: pandas, matplotlib, statsmodels, numpy e scipy. O notebook declara kernel Python 3 (ipykernel) e versão de linguagem 3.14.7 em seus metadados; isso descreve o arquivo, não uma instalação validada neste dispositivo. A leitura usa caminho relativo `treadwear.txt`, portanto executar com a pasta do projeto como diretório de trabalho. Não há versões de bibliotecas fixadas nem instalação/teste do ambiente realizado nesta recuperação.
