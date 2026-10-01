# Data Mining Geo-Espacial — 4 Estudos de Caso (KNIME Analytics Platform)

**Autor:** Áureo Miguel Rodrigues de Almeida
**Curso:** MSc Geographic Information Science and Systems, NOVA IMS · U.C. Data Mining Geo-Espacial (2025/2026)

## Resumo

Quatro problemas de data mining resolvidos na plataforma **KNIME Analytics Platform**, cobrindo clustering não supervisionado, redes neuronais para regressão e classificação supervisionada.

---

## Tarefa 1 — Classificação Geodemográfica de Lisboa

Segmentação das **882 secções estatísticas** do município de Lisboa em grupos socioeconómicos homogéneos, com base em 96 variáveis do Censo (INE, 2001).

- Seleção de variáveis apoiada por **Random Forest Regression** (variável-alvo FE, R² = 0,91)
- Normalização Min-Max e clustering **k-Means**, testado para k ∈ {2,3,6,7,9} e avaliado por Silhouette
- **k = 3** selecionado (Silhouette = 0,307): três perfis territoriais — envelhecido/desempregado (histórico), jovem/qualificado (moderno), e de maior dimensão/habitação antiga (expansão urbana)
- Confirmação de autocorrelação espacial na percentagem de idosos (**Moran's I = 0,58, p < 0,001**)
- Resultados exportados via GeoFile Writer e cartografados em ArcGIS Pro

## Tarefa 2 — Classificação de Imagens de Satélite

Classificação não supervisionada de pixels (300 registos, 4 bandas espectrais) em 3 classes de uso do solo (água, urbano, outros), comparando **k-Means, Hierarchical Clustering e SOM**.

- k-Means (k=3) selecionado; k=4 e k=7 não melhoraram a separação (Silhouette)
- A classe **água é separada com perfeição** (entropia = 0) nos três métodos
- Urbano e "outros usos" partilham assinaturas espectrais sobrepostas (Quality < 0,6)
- Qualidade global: **Quality = 0,723**, teste Qui-Quadrado x² = 297,4 (p = 3,94×10⁻⁶³)
- Recomendação: incorporar bandas adicionais (infravermelho próximo, NDVI) para separar urbano/outros

## Tarefa 3 — Otimização de Rede de Estações Meteorológicas

Decisão sobre qual de 4 estações meteorológicas costeiras (E1–E4) encerrar, mantendo a capacidade de estimar a sua temperatura a partir das restantes.

- 4 redes neuronais **RProp MLP** paralelas (3 inputs → 5 neurónios ocultos (Tanh) → 1 output), uma por estação-alvo
- Partição 70/30, correlações inter-estações muito elevadas (r > 0,98)
- **Estação E2** identificada para encerramento: menor MSE (0,001), maior R² (0,983) — a sua temperatura é a mais facilmente reconstruída pelas outras 3 (erro real ≈ 1 °C)

## Tarefa 4 — Sistema de Recomendação de Fármaco

Sistema preditivo para recomendar o fármaco mais adequado (entre 5 composições) a novos pacientes, com base em características clínicas.

- Comparação entre **RProp MLP** e **Árvore de Decisão** (profundidade máx. 5), treinados sobre 500 pacientes (70/30)
- RProp MLP: accuracy 64,9% (kappa 0,486) — classificou quase todos os pacientes na mesma classe, sem discriminação útil
- **Árvore de Decisão: accuracy 88,7% (kappa 0,841)** — modelo final escolhido
- Preditor principal identificado: **c4 (concentração de potássio)**, raiz da árvore (c4 ≤ 0,0459 → drugY)
- Previsões aplicadas a 20 pacientes sem diagnóstico: drugY×11, drugX×4, drugA×3, drugC×1, drugB×1

---

## Stack

KNIME Analytics Platform · k-Means · Hierarchical Clustering · SOM (Self-Organizing Maps) · RProp MLP · Decision Trees · Random Forest · ArcGIS Pro

## Nota

Os workflows foram construídos visualmente no KNIME Analytics Platform (não são scripts de texto). O relatório completo, com todos os workflows, figuras e tabelas, está incluído neste repositório (`relatorio.docx`). Se tiveres os ficheiros `.knwf` dos workflows, podem ser adicionados a este repositório para tornar o projeto totalmente reprodutível.
