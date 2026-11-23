# RentSmart — Sistema de Orçamento de Locação (R.M Imóveis)

Aplicação em Python (Programação Orientada a Objetos) que recebe as características da locação, aplica as regras comerciais da R.M Imóveis, calcula o aluguel mensal, mostra a taxa contratual separadamente e gera um CSV com a projeção dos 12 primeiros meses.

## Como executar

Requisitos: Python 3.8 ou superior (usa apenas a biblioteca padrão, não precisa instalar nada).

```bash
python rentsmart.py
```

O programa pergunta nome do cliente, tipo de imóvel, quartos, garagem, crianças (apenas apartamento) e parcelamento da taxa. Ao final, exibe o orçamento e cria o arquivo `projecao_12_meses.csv` na mesma pasta.

## Regras implementadas

| Item | Regra |
|---|---|
| Apartamento 1 quarto | R$ 700,00 (2 quartos: +R$ 200,00) |
| Casa 1 quarto | R$ 900,00 (2 quartos: +R$ 250,00) |
| Estúdio | R$ 1.200,00 |
| Garagem (casa/apto) | +R$ 300,00 (1 vaga) |
| Estacionamento estúdio | Pacote de 2 vagas R$ 250,00 + R$ 60,00 por vaga extra |
| Desconto | 5% para apartamento sem crianças, sobre o aluguel já com adicionais |
| Taxa contratual | R$ 2.000,00 em 1 a 5 parcelas, cobrada separada do aluguel |

### Decisões de interpretação
- O desconto de 5% incide sobre base + adicionais (2º quarto e garagem).
- No estúdio, o estacionamento é opcional; se contratado, vale o pacote de 2 vagas, com extras a R$ 60,00 cada.
- A taxa é dividida igualmente; a última parcela absorve a diferença de centavos.
- A taxa é paga nos primeiros meses (uma parcela por mês) e aparece em coluna própria no CSV.

## Estrutura de classes

- `Imovel` (classe base): atributos `quartos`, `vagas`; métodos `adicionais()`, `desconto()`, `valor_mensal()`.
- `Apartamento`, `Casa`, `Estudio`: herdam de `Imovel` e implementam suas próprias regras (polimorfismo).
- `Orcamento`: agrega imóvel + taxa + parcelas; métodos `resumo()`, `valores_parcelas()`, `projecao_12_meses()`, `exportar_csv()`.

## Arquivo CSV
Separador `;` e codificação UTF-8 com BOM (abre direto no Excel em português). Colunas: Mês, Aluguel, Parcela da taxa contratual, Total do mês, Total acumulado.

## Exemplo de saída
Veja `projecao_12_meses.csv` (apartamento 2 quartos, com garagem, sem crianças, taxa em 3x).
