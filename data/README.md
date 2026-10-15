# data/

Dados do projeto. **Nada aqui vai para o Git**; o conteúdo pesado é versionado com DVC.

- `raw/`: dados originais, nunca editados à mão
- `interim/`: etapas intermediárias de limpeza
- `processed/`: dados prontos para modelagem

Registre a origem de cada conjunto (fonte, data de download, versão) neste arquivo. Prefira baixar por código (HAPI, pySPEDAS) a baixar à mão, e guarde o script em `src/mestrado/`. Lista de fontes em [docs/fontes-de-pesquisa.md](../docs/fontes-de-pesquisa.md).

## Conjuntos

| Conjunto | Fonte | Baixado em | Observações |
|---|---|---|---|
| Séries sintéticas (AR linear, mapas acoplados, Ginzburg-Landau) | Gerado por `src/mestrado/` | (planejado) | Registrar semente, parâmetros e commit |
| OMNI horário (vento solar, campo magnético interplanetário) | OMNIWeb / CDAWeb (HAPI, `OMNI2_H0_MRG1HR`) | (planejado) | Série composta: anotar a fonte de cada intervalo |
| Dst | WDC Kyoto (final, provisório ou tempo real) | (planejado) | Registrar **qual versão** foi usada; o final tem atraso de anos |
| Kp | GFZ Potsdam | (planejado, opcional) | Valores recentes são *nowcast* até virarem definitivos |
