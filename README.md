# Monitoramento de Base de Clientes · Power BI

Dashboard para acompanhamento diário da base ativa por categoria de plano, grupo e empresa.
**Dados fictícios: nomes e números não correspondem a nenhuma empresa real.**

![Visão do dia](VisaoDeCarteira.png)

## Problema de negócio
Times de operação e gestão precisavam identificar rapidamente oscilações na base ativa (quedas por empresa e evolução por categoria de plano) sem consolidar planilhas manualmente.

## Solução
| Recurso | Descrição |
|---|---|
| KPIs com variação | Δ Dia e Δ Mês por categoria de plano e no total |
| Desempenho por grupo | Ranking com indicadores visuais de alta e queda |
| Rankings automáticos | Maiores aumentos e maiores quedas por empresa |
| Distribuição | Participação de cada categoria na base |
| Filtros | Região, Grupo, Empresa e Categoria, com botão para limpar |
| Navegação | Visão do Dia · Outros Dias · Mês a Mês (bookmarks) |

## Arquitetura
```mermaid
flowchart LR
  A[Fontes: Excel/CSV] --> B[Power Query: ETL e limpeza]
  B --> C[Star Schema: fato de base diária + dimensões]
  C --> D[Medidas DAX: deltas, rankings, ISINSCOPE]
  D --> E[Relatório: 3 páginas]
```

## Destaques técnicos
- Variação diária e mensal com medidas DAX de time intelligence
- Rankings dinâmicos com `TOPN` + `ADDCOLUMNS`
- `ISINSCOPE` para adaptar os cálculos ao nível de drill
- Star Schema separando fato e dimensões, o que reduziu o modelo e acelerou a atualização

## Decisões técnicas e trade-offs
- **Star Schema em vez de tabela única:** modelo menor e DAX mais simples, com um passo a mais de ETL.
- **Bookmarks em vez de páginas duplicadas:** menos manutenção, mas exige cuidado ao editar os visuais.

## Próximos passos
- Publicar uma versão do .pbix com gerador de dados fictícios
- Documentar as medidas DAX principais em `/docs`

## Aviso de dados
Este repositório contém apenas a visualização do relatório. Todos os números são fictícios e os nomes de grupos e empresas são genéricos; nenhum dado real foi publicado.
