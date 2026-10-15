# mestrado-xai-inpe

Caderno de pesquisa, código e experimentos do meu projeto de mestrado em Computação Aplicada (CAP/INPE) sobre **quando confiar na explicação que um modelo dá para a previsão de um evento extremo** (tempestades geomagnéticas, disrupções em plasmas de tokamak).

> **Status (outubro de 2026):** em processo de ingresso; orientação a confirmar. Ainda não há resultados. O repositório é público para documentar o percurso, dar rastreabilidade aos resultados e facilitar a citação.

## Pergunta de pesquisa

Como avaliar se a explicação de um modelo de previsão de eventos extremos é **fisicamente consistente**, isto é, se respeita a causalidade, a defasagem e o alcance espacial da dinâmica, e em que condições SHAP e LIME produzem explicações assim? SHAP e LIME são instrumentos do experimento, não o objeto da pesquisa.

1. **Critério:** que medidas derivadas da dinâmica distinguem explicações consistentes das que não são, e elas discriminam melhor do que as métricas usuais de fidelidade?
2. **Condições:** em séries da equação de Ginzburg-Landau com precursor de defasagem conhecida, como a consistência varia com ruído, colinearidade, intermitência, janela, referência (*baseline*) e arquitetura? Quanto do erro vem do explicador e quanto do modelo?
3. **Validação:** o critério se sustenta em dados reais de clima espacial, onde há uma relação física conhecida (vento solar e índice Dst)?

## Abordagem

- **Dados sintéticos com dinâmica conhecida**, em ordem crescente de complexidade: sistema autorregressivo linear (teste de sanidade), rede de mapas acoplados e equação complexa de Ginzburg-Landau com forçamento atrasado.
- **Modelos em dois níveis:** um oráculo que implementa a própria dinâmica e modelos treinados (XGBoost e LSTM), com divisão temporal entre treino, validação e teste. Se o explicador falha no oráculo, o problema é do método.
- **Explicadores:** SHAP e LIME, com a referência (*baseline*) tratada como fator experimental.
- **Critério de consistência:** violação causal, erro de defasagem, concentração e estabilidade, comparados com métricas usuais e com controles nulos.
- **Validação em clima espacial** com dados abertos (OMNI, Dst). Tokamak fica como continuidade.

Hipóteses: **H1** a consistência cai com colinearidade e intermitência; **H2** a violação causal é maior nos modelos treinados do que no oráculo; **H3** o critério discrimina explicações melhor do que a concordância de ranking sozinha. Resultado contrário também é contribuição.

## Onde estamos

- [x] Estrutura do repositório, templates de nota e cronograma
- [ ] Revisão sistemática (buscas em [docs/log-de-busca.md](docs/log-de-busca.md))
- [ ] Gerador de dados sintéticos (`src/mestrado/`)
- [ ] EXP-001: sistema autorregressivo linear com SHAP e LIME (teste de sanidade)
- [ ] Modelos treinados e oráculo
- [ ] Critério de consistência
- [ ] Validação em clima espacial

## Estrutura

```
data/         dados (raw, interim, processed), versionados com DVC, fora do Git
notebooks/    exploração; código reutilizável vai para src/
src/mestrado/ código reutilizável (simulação, modelos, explicações, métricas)
experiments/  um diretório por experimento (EXP-001-...), com config, run e nota
reports/      figuras e tabelas prontas para artigos e dissertação
docs/         cronograma, fontes de pesquisa, log de busca e templates de nota
tests/        testes do que for crítico (simulação, pré-processamento, métricas)
```

## Fontes de pesquisa

- [docs/fontes-de-pesquisa.md](docs/fontes-de-pesquisa.md): bases de artigos, periódicos, dados abertos, bibliotecas de XAI e leituras-semente.
- [docs/log-de-busca.md](docs/log-de-busca.md): registro de cada busca feita.
- [data/README.md](data/README.md): origem e versão de cada conjunto de dados.

## Fluxo de trabalho

1. **Ler** no Zotero (coleções por tema) e criar uma **nota de literatura** (`docs/templates/nota-literatura.md`).
2. **Entender** e escrever uma **nota de conceito** com minhas palavras (`nota-conceito.md`).
3. **Experimentar**: abrir uma issue, rodar o experimento, registrar no MLflow/W&B e escrever a **nota de experimento** (`nota-experimento.md`).
4. **Decidir**: registrar cada escolha relevante em um **registro de decisão** (`registro-decisao.md`).
5. **Publicar**: conceitos e resultados maduros viram post de blog, seção de artigo ou capítulo da dissertação.

## Gestão do projeto

- **Pergunta de pesquisa** (épico) → **milestone** (fase) → **issue** (tarefa com critério de pronto).
- Labels: `leitura`, `experimento`, `escrita`, `burocracia`.
- Cronograma completo em [docs/cronograma.md](docs/cronograma.md).
- Revisão semanal de 15 minutos.

## Ambiente

Requer Python 3.11 ou superior e [uv](https://docs.astral.sh/uv/).

```bash
uv sync --group dev
pre-commit install
pytest
```

Grupos opcionais: `--group data` (cliente HAPI para baixar OMNI) e `--group xai-extra` (Captum).

## Como citar

Veja [CITATION.cff](CITATION.cff). Cada marco do projeto gera uma release com DOI via Zenodo.

## Licença

Código sob licença MIT (veja o arquivo [LICENSE](LICENSE)). Para texto e dados próprios, a sugestão é CC-BY 4.0 (a definir).
