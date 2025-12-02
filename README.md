# Análise de Dados Imobiliários - São Paulo (2019-2024)

Este projeto realiza análises abrangentes sobre o mercado imobiliário da cidade de São Paulo utilizando dados de IPTU (Imposto Predial e Territorial Urbano) e ITBI (Imposto sobre Transmissão de Bens Imóveis) para o período de 2019 a 2024.

## 📋 Visão Geral

O projeto tem como objetivo principal:
- Calcular o **Valor Venal** dos imóveis utilizando fórmulas complexas da Prefeitura de São Paulo
- Analisar padrões espaço-temporais de valorização imobiliária
- Comparar valores estimados (IPTU) com valores reais de transações (ITBI)
- Identificar taxas de valorização por tipo de uso e localização
- Realizar análises exploratórias dos dados

## 📁 Estrutura do Projeto

```
papers/real_estate_saopaulo/
├── 1. Data praparation.ipynb          # Preparação e processamento inicial dos dados
├── 2.Timespace analysis.ipynb         # Análise espaço-temporal de valorização
├── 3. Analise IPTU vs ITBI.ipynb      # Comparação entre valores IPTU e ITBI
├── 4. Exploratory Data Analysis.ipynb # Análise exploratória de dados
├── 5. Valorizacao por Tipo de Uso.ipynb # Análise de valorização por tipo de uso
├── data/
│   ├── IPTU_2019_2024.csv            # Dataset consolidado de IPTU
│   ├── ITBI_2019_2024.csv           # Dataset consolidado de ITBI
│   ├── IPTU_2019.csv ... IPTU_2024.csv  # Dados anuais de IPTU
│   ├── ITBI_2019.csv ... ITBI_2024.csv  # Dados anuais de ITBI
│   └── xlsx/                          # Arquivos Excel originais
└── README.md                          # Este arquivo
```

## 🔄 Fluxo de Trabalho

Os notebooks devem ser executados na seguinte ordem:

1. **1. Data praparation.ipynb**: Preparação inicial dos dados
   - Processa arquivos Excel de IPTU e ITBI
   - Calcula Valor Venal usando fórmulas da Prefeitura
   - Gera os arquivos CSV consolidados

2. **2.Timespace analysis.ipynb**: Análise espaço-temporal
   - Calcula taxas de valorização por setor fiscal
   - Identifica padrões temporais e espaciais

3. **3. Analise IPTU vs ITBI.ipynb**: Comparação de valores
   - Compara Valor Venal (IPTU) com valores reais (ITBI)
   - Identifica discrepâncias e padrões

4. **4. Exploratory Data Analysis.ipynb**: Análise exploratória
   - Estatísticas descritivas
   - Identificação de padrões e outliers

5. **5. Valorizacao por Tipo de Uso.ipynb**: Análise por tipo de uso
   - Calcula taxas de valorização anual por tipo de uso
   - Aplica critérios estatísticos rigorosos

## 📊 Arquivos de Dados

### IPTU_2019_2024.csv

Dataset consolidado contendo dados de IPTU processados para o período de 2019 a 2024.

**Colunas principais:**
- `NUMERO DO CONTRIBUINTE`: Identificador único do imóvel (11 dígitos)
- `ANO DO EXERCICIO`: Ano de referência do exercício fiscal (2019-2024)
- `NOME DE LOGRADOURO DO IMOVEL`: Nome da rua/logradouro
- `NUMERO DO IMOVEL`: Número do imóvel
- `AREA DO TERRENO`: Área do terreno em m²
- `AREA CONSTRUIDA`: Área construída em m²
- `AREA OCUPADA`: Área ocupada em m²
- `VALOR DO M2 DO TERRENO`: Valor do metro quadrado do terreno (R$)
- `VALOR DO M2 DE CONSTRUCAO`: Valor do metro quadrado de construção (R$)
- `TIPO DE USO DO IMOVEL`: Categoria de uso (Residencial, Comercial, etc.)
- `TIPO DE PADRAO DA CONSTRUCAO`: Padrão construtivo
- `BAIRRO DO IMOVEL`: Bairro onde está localizado o imóvel
- `CEP DO IMOVEL`: CEP do imóvel
- `VALOR VENAL`: **Valor Venal calculado** (R$) - resultado principal do processamento
- `setor`: Setor fiscal (3 dígitos)
- `quadra`: Quadra fiscal
- `lote`: Lote fiscal
- `bairro`: Bairro normalizado

**Estatísticas:**
- Aproximadamente 21.3 milhões de registros
- 18 colunas
- Período: 2019-2024

**Cálculo do Valor Venal:**
O Valor Venal é calculado através de uma função complexa (`calcula_vv()`) que considera:
- Valor da construção (área construída × valor m² × fator de obsolescência)
- Valor do terreno incorporado (com ajustes por profundidade, tipo de terreno, esquina)
- Valor do excesso de área do terreno
- Fatores de condomínio para imóveis verticais
- Fração ideal do imóvel
- Zona Fiscal (ZF) e fatores de correção associados

### ITBI_2019_2024.csv

Dataset consolidado contendo dados de transações imobiliárias (ITBI) para o período de 2019 a 2024.

**Colunas principais:**
- `N° do Cadastro (SQL)`: Número do cadastro SQL (identificador do imóvel)
- `Natureza de Transação`: Tipo de transação (ex: "1.Compra e venda")
- `Valor de Transação (declarado pelo contribuinte)`: Valor declarado na transação (R$)
- `Data de Transação`: Data da transação (formato DD/MM/YYYY)
- `Valor Venal de Referência`: Valor venal de referência usado pela Prefeitura (R$)
- `Proporção Transmitida (%)`: Percentual da propriedade transmitida (0-100%)
- `Valor Venal de Referência (proporcional)`: Valor venal proporcional à transação (R$)
- `Base de Cálculo adotada`: Base de cálculo do imposto (R$)
- `Tipo de Financiamento`: Tipo de financiamento utilizado
- `Valor Financiado`: Valor financiado na transação (R$)
- `Situação do SQL`: Situação do cadastro (ex: "Ativo Predial")
- `Área do Terreno (m2)`: Área do terreno em m²
- `Área Construída (m2)`: Área construída em m²
- `Ano da Transacao`: Ano da transação (2019-2024)
- `Mes da Transacao`: Mês da transação (1-12)
- `Ano/Mes da Transacao`: Ano e mês no formato YYYY/MM
- `setor`: Setor fiscal (3 dígitos)
- `quadra`: Quadra fiscal
- `lote`: Lote fiscal
- `bairro`: Bairro normalizado

**Características:**
- Dados de transações imobiliárias reais
- Valores declarados pelos contribuintes
- Informações geográficas (setor, quadra, lote, bairro)
- Dados temporais (ano, mês)

**Filtros aplicados nas análises:**
- Transações com 100% de proporção transmitida (transações completas)
- Valores de transação acima de R$ 1.000 (remover valores inconsistentes)
- Remoção de duplicatas baseadas em cadastro SQL e data

## 🔧 Dependências

As principais bibliotecas Python utilizadas:
- `pandas`: Manipulação e análise de dados
- `numpy`: Operações numéricas
- `matplotlib`: Visualizações
- `seaborn`: Visualizações estatísticas

## 📝 Notas Importantes

1. **Encoding**: Os arquivos CSV podem conter caracteres especiais. Alguns notebooks tentam diferentes encodings (`utf-8`, `latin-1`).

2. **Memória**: Os datasets são grandes (21+ milhões de registros). Certifique-se de ter memória RAM suficiente ou use processamento em chunks.

3. **Dados Originais**: Os arquivos Excel originais estão na pasta `data/xlsx/` e são processados no notebook de preparação de dados.

4. **Zona Fiscal**: O cálculo do Valor Venal utiliza a Zona Fiscal (ZF) extraída dos primeiros 3 dígitos do número do contribuinte, com fatores de correção específicos para cada zona.

5. **Validação**: As análises aplicam filtros rigorosos para garantir qualidade dos dados, incluindo remoção de outliers e validação de consistência.

## 🎯 Objetivos de Pesquisa

Este projeto permite investigar:
- Precisão das avaliações imobiliárias da Prefeitura
- Padrões de valorização imobiliária em São Paulo
- Diferenças entre valores estimados e valores de mercado
- Comportamento temporal e espacial do mercado imobiliário
- Impacto do tipo de uso na valorização dos imóveis

## 📚 Referências

Os dados utilizados são públicos e disponibilizados pela Prefeitura de São Paulo através dos sistemas de IPTU e ITBI. As fórmulas de cálculo do Valor Venal seguem a legislação tributária municipal.

---

**Última atualização**: 2024

