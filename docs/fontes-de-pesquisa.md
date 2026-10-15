# Fontes de pesquisa

Lista curada para este projeto (XAI avaliada com dinâmica conhecida, em séries temporais de eventos extremos). Revisada em 2026-10-15. Mantenha curta: se uma fonte não for usada em dois meses, remova.

Cada busca feita deve ser registrada em [log-de-busca.md](log-de-busca.md) (data, base, string, resultados).

## 1. Onde achar artigos

| Fonte | Para que serve | Dica |
|---|---|---|
| [Google Scholar](https://scholar.google.com) | Cobertura ampla, alertas, "citado por" | Crie alertas para as strings da seção 7 |
| [Semantic Scholar](https://www.semanticscholar.org) | Busca semântica, resumos curtos (TLDR), citações | Bom para achar trabalhos parecidos com um artigo-semente |
| [OpenAlex](https://openalex.org) | Base aberta com API e filtros | Exporta listas para análise bibliométrica depois |
| [arXiv](https://arxiv.org) | Preprints, onde XAI e física saem primeiro | Categorias: `cs.LG`, `stat.ML`, `physics.space-ph`, `physics.plasm-ph`, `physics.ao-ph`, `nlin.CD` (caos), `nlin.PS` (padrões, Ginzburg-Landau) |
| [NASA ADS](https://ui.adsabs.harvard.edu) | Índice de astrofísica e física espacial, com citações | Melhor que o Scholar para clima espacial |
| [Connected Papers](https://www.connectedpapers.com), [Litmaps](https://www.litmaps.com), ResearchRabbit | Grafo de citações a partir de um artigo-semente | Use depois de ter 3 a 5 artigos centrais |

Ferramentas de IA para busca de literatura ajudam a explorar, mas inventam referências com frequência: só entra no Zotero o que você abriu e conferiu pelo DOI.

## 2. Periódicos e eventos por tema

- **XAI e aprendizado de máquina:** NeurIPS (trilha Datasets and Benchmarks), ICML, ICLR, JMLR, World Conference on Explainable AI.
- **Geociências + XAI:** Artificial Intelligence for the Earth Systems (AMS), onde saiu Mamalakis et al.
- **Clima espacial:** Space Weather (AGU), JGR Space Physics, Journal of Space Weather and Space Climate, Frontiers in Astronomy and Space Sciences.
- **Plasma e fusão:** Nuclear Fusion, Physics of Plasmas, Plasma Physics and Controlled Fusion, Fusion Engineering and Design, Frontiers in Physics.
- **Dinâmica não linear (Ginzburg-Landau, mapas acoplados):** Reviews of Modern Physics, Chaos, Physical Review E, Physica D.

## 3. Acesso e fontes no Brasil

- [Portal de Periódicos CAPES](https://www.periodicos.capes.gov.br): acesso a artigos pagos com login institucional (CAFe). Confirme com a biblioteca do IFSP ou do INPE como entrar de casa.
- [BDTD (IBICT)](https://bdtd.ibict.br): teses e dissertações brasileiras, inclusive as do INPE.
- [SciELO](https://www.scielo.org): periódicos abertos ibero-americanos.
- [Biblioteca Digital da Memória Científica do INPE](https://www.gov.br/inpe/pt-br/area-conhecimento/biblioteca/acervo-digital/base-de-dados): teses, dissertações e relatórios do instituto. Leia dissertações anteriores do CAP para ver estrutura e nível esperado.
- [Página do LAMIFE](https://www.gov.br/inpe/pt-br/area-conhecimento/pesquisa-aplicada-e-desenvolvimento-tecnologico/laboratorios-banco-de-testes-grupos-p-d/laboratorio-de-aprendizagem-de-maquina-interpretavel-em-fisica-de-eventos-extremos-lamife): modelos e aplicações do laboratório.

## 4. Dados abertos

### Clima espacial (plano principal)

| Dado | Fonte | Cuidados |
|---|---|---|
| Vento solar, campo magnético interplanetário e índices (resolução de 1 h e 1 min) | [OMNIWeb (NASA SPDF)](https://omniweb.gsfc.nasa.gov) | Série composta de várias naves: veja a fonte de cada intervalo |
| Dst | [WDC Kyoto](https://wdc.kugi.kyoto-u.ac.jp/dst_final/) (final, provisório e tempo real) | O Dst **final** tem atraso de anos. Na tabela de disponibilidade da OMNIWeb o final ia até 2020 quando consultei; depois entra provisório ou tempo real, que mudam. Registre qual versão usou. DOI para citar: 10.17593/14515-74000 |
| Kp | [GFZ Potsdam](https://kp.gfz.de) | CC BY 4.0. Valores recentes são *nowcast* e são substituídos pelos definitivos. DOI: [10.5880/Kp.0001](https://doi.org/10.5880/Kp.0001) |
| Dados e índices do Brasil | [Portal EMBRACE/INPE](https://www2.inpe.br/climaespacial/portal/) | Magnetômetros e índices regionais; veja a seção de dados (EmbraceData) |
| Tempo real | [NOAA SWPC](https://www.swpc.noaa.gov) | Para operação, não para séries de pesquisa reprodutíveis |

Acesso por código (evita baixar arquivo à mão e deixa o download reproduzível):

- [HAPI](https://hapi-server.org) com o cliente Python `hapiclient`. O CDAWeb serve o OMNI horário pelo conjunto `OMNI2_H0_MRG1HR`.
- [pySPEDAS](https://pyspedas.readthedocs.io/en/latest/geomagnetic_indices.html): baixa Kp, Dst e OMNIWeb.

### Tokamak (continuidade, depois do plano principal)

Dados de JET e ITER costumam ter acesso restrito. Uma opção aberta é o [FAIR-MAST (UKAEA)](https://www.ukaea.org/service/fair-mast/), com dados de diagnósticos das campanhas M05 a M09 do MAST (API de metadados e dados em S3/Zarr; veja também o [portal de dados abertos](https://opendata.ukaea.uk/)). Antes de contar com ele, confira se há rótulos de disrupção utilizáveis e a licença.

## 5. Bibliotecas de XAI para séries temporais

| Biblioteca | O que oferece | Observação |
|---|---|---|
| `shap`, `lime` | Os dois explicadores do projeto | Já estão no `pyproject.toml` |
| [Captum](https://captum.ai) | Atribuição para PyTorch (Integrated Gradients, GradientSHAP) | Entra no grupo opcional `xai-extra` |
| [Time Interpret (`tint`)](https://pypi.org/project/time-interpret) | Estende o Captum para séries temporais; traz conjuntos sintéticos com saliência verdadeira e métodos de avaliação | Mais próximo do que você quer fazer; leia o código como referência |
| [TSInterpret](https://joss.theoj.org/papers/10.21105/joss.05220) | Interface unificada de interpretação | Foco em classificação de séries |
| [Quantus](https://www.jmlr.org/beta/papers/v24/22-0142.html) | Mais de 30 métricas de qualidade de explicação (fidelidade, robustez, localização) | Nasceu em visão computacional: confira o suporte a séries temporais |
| [OpenXAI](https://arxiv.org/abs/2206.11104) | Benchmark de explicações pós-hoc | Dados tabulares; útil como ponto de comparação |

## 6. Leituras-semente (do plano de estudos)

Comece o *snowballing* (ler as referências e quem citou) por estes:

| Tema | Referência |
|---|---|
| Avaliação com verdade conhecida em séries | Ismail et al. 2020, [arXiv:2010.13924](https://arxiv.org/abs/2010.13924) |
| Métricas de perturbação vs. verdade conhecida | Baer et al. 2025, [arXiv:2506.11790](https://arxiv.org/abs/2506.11790) |
| Fidelidade de XAI em geociências | Mamalakis, Barnes e Ebert-Uphoff 2022, [arXiv:2202.03407](https://arxiv.org/abs/2202.03407) |
| Avaliação sistemática em séries temporais | Turbé et al. 2022, [arXiv:2202.05656](https://arxiv.org/abs/2202.05656) |
| Explicar o modelo vs. explicar os dados | Chen et al. 2020, [arXiv:2006.16234](https://arxiv.org/abs/2006.16234) |
| XAI em disrupções de tokamak | Bonalumi et al. 2024, [10.3389/fphy.2024.1359656](https://doi.org/10.3389/fphy.2024.1359656) |
| Aprendizado de máquina em clima espacial | Camporeale 2019, [10.1029/2018SW002061](https://doi.org/10.1029/2018SW002061) |
| Equação de Ginzburg-Landau complexa | Aranson e Kramer 2002, [10.1103/RevModPhys.74.99](https://doi.org/10.1103/RevModPhys.74.99) |
| Relação vento solar e Dst | Burton, McPherron e Russell 1975 (J. Geophys. Res., 80, 4204) |

## 7. Strings de busca de partida

Adapte a sintaxe a cada base e registre a versão usada no log.

```
("time series" OR "multivariate time series") AND (attribution OR saliency OR explanation OR XAI) AND (benchmark OR "ground truth" OR synthetic OR evaluation)
("space weather" OR geomagnetic OR Dst) AND (explainab* OR interpretab* OR SHAP OR LIME)
(tokamak AND disruption) AND (explainab* OR interpretab* OR saliency OR SHAP)
("Ginzburg-Landau" OR "coupled map lattice") AND ("machine learning" OR "neural network") AND (forecast* OR predict*)
("extreme events" OR "rare events") AND (explainab* OR interpretab*) AND "time series"
```

Se o resultado for chamado de **revisão sistemática**, siga o [PRISMA 2020](https://www.prisma-statement.org) e registre o protocolo (por exemplo no [OSF](https://osf.io)) antes de buscar.
