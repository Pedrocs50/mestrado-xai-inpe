# mestrado-xai-inpe

Caderno de pesquisa, código e experimentos do meu mestrado em **IA explicável (XAI)** aplicada a **plasma (tokamak)** e **clima espacial**, no INPE.

> Projeto em andamento. Este repositório é público para documentar a jornada, dar rastreabilidade aos resultados e facilitar a citação.

## Estrutura

```
data/         dados (raw, interim, processed) - versionados com DVC, fora do Git
notebooks/    exploração; código reutilizável vai para src/
src/mestrado/ código reutilizável (pré-processamento, modelos, explicações, métricas)
experiments/  um diretório por experimento (EXP-001-...), com config, run e nota
reports/      figuras e tabelas prontas para artigos e dissertação
docs/         cronograma e templates de nota
tests/        testes do que for crítico (pré-processamento, métricas)
```

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

```bash
uv sync --group dev
pre-commit install
pytest
```

## Como citar

Veja [CITATION.cff](CITATION.cff). Cada marco do projeto gera uma release com DOI via Zenodo.

## Licença

Código sob licença MIT (veja o arquivo [LICENSE](LICENSE)). Para texto e dados próprios, a sugestão é CC-BY 4.0 (a definir).
