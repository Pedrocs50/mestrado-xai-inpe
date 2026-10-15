# experiments/

Uma pasta por experimento, nomeada `EXP-001-descricao-curta/`, com:

- `config.yaml`: hiperparâmetros e caminhos de dados
- `run.py`: ponto de entrada (chama funções de `src/mestrado/`)
- `NOTA.md`: nota de experimento (use `docs/templates/nota-experimento.md`)

Cada execução deve ser registrada no MLflow ou W&B, com o hash do commit.
