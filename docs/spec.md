# 01 — overview.md

## Visão geral do sistema

```md
# SDD — Calculadora de Compras de Supermercado

## 1. Objetivo

Criar uma aplicação web extremamente simples que permita ao usuário
somar o valor das compras enquanto percorre o supermercado.

O usuário digita os valores dos produtos e o sistema calcula
automaticamente o total da compra.

A aplicação deve ser otimizada para uso em dispositivos móveis.

## 2. Tecnologias

A aplicação deve consistir em apenas um arquivo:

index.html

Tecnologias permitidas:

- HTML5
- CSS3
- Bootstrap 5
- JavaScript puro (Vanilla JS)

Nenhum backend deve existir.

## 3. Persistência de dados

Os dados da compra devem ser armazenados no:

localStorage do navegador.

Isso garante que:

- ao atualizar a página
- ao fechar o navegador
- ao sair e voltar

os dados ainda estarão disponíveis.

## 4. Estrutura da aplicação

A aplicação é composta por:

1 página única:

index.html

Componentes da página:

- Campo de entrada de valores
- Botão "Adicionar"
- Tabela de itens
- Total da compra (fixo no rodapé)
- Botão "Resetar compra"
- Teclado numérico simplificado (caso necessário)

## 5. Usuário alvo

Consumidor usando smartphone durante compras no supermercado.

## 6. Requisitos principais

O usuário deve poder digitar entradas no formato:

quantidade valor

ou

valor quantidade

ou

peso valor

ou

valor peso

O sistema deve interpretar automaticamente os números e calcular:

quantidade × preço unitário
```

---

# 02 — ui-layout.md

## Layout e experiência mobile

```md
# UI Layout

## 1. Layout geral

A interface deve ser otimizada para mobile.

Mesmo em desktop, o layout deve ficar centralizado
em uma coluna estreita (estilo "mobile preview").

Largura máxima da coluna:

400px

Centralizada horizontalmente.

## 2. Estrutura da tela

Topo da tela:

[ input texto ][ botão adicionar ]

Abaixo:

Tabela de itens

Rodapé fixo:

Preço total da compra

Abaixo do total:

Botão resetar

## 3. Tabela de itens

Colunas:

ID | Quantidade | Preço Unitário | Preço Total

Exemplo:

1 | 2 | 14,99 | 29,98

## 4. Rodapé fixo

O total da compra deve ficar sempre visível.

Exemplo:

Preço total: R$ 59,67

Esse elemento deve ser:

position: fixed
bottom: 0

## 5. Teclado numérico

Caso o teclado do dispositivo não apresente
os caracteres necessários (números, espaço, vírgula),
deve existir um teclado virtual.

Esse teclado deve ficar logo acima do total.

Botões obrigatórios:

0 1 2 3 4 5 6 7 8 9
,
espaço
backspace
enter (que tem o mesmo efeito do botão adicionar)

Ao implementar esse teclado numérido virtual, o campo input text nao deve exibir o teclado do dispositivo ao ser clicado, mas sim acatar a entrada desse teclado virtual.
```

---

# 03 — input-parsing.md

Este é o **arquivo mais importante**, porque orienta a IA a entender a lógica.

```md
# Parsing de Entrada

## 1. Formato da entrada

O usuário deve digitar **dois números separados por espaço**.

Exemplos válidos:

2 14,99
14,99 2
0,678 6,99
6,99 0,678

Cada entrada representa:

quantidade/peso e preço unitário.

A ordem pode ser invertida.

---

## 2. Normalização

Antes de processar os dados, o sistema deve:

1. Remover espaços extras no início e no fim da string.
2. Substituir vírgula por ponto para permitir cálculo numérico.

Exemplo:

Entrada do usuário:

0,678 6,99

Após normalização:

0.678 6.99

---

## 3. Separação dos valores

A string deve ser dividida pelo espaço:

valor1
valor2

Exemplo:

entrada:

2 14,99

resultado:

valor1 = 2
valor2 = 14.99

---

## 4. Identificação dos campos

A identificação entre **quantidade/peso** e **preço unitário** deve ser feita com base **no formato do número**.

### Regra

* Números **inteiros** ou com **3 casas decimais** representam **quantidade ou peso**.
* Números com **2 casas decimais** representam **preço unitário**.
* Se ambos os números tiverem 2 casas decimais, considerar a entrada inválida.

### Exemplos

Entrada:

2 14,99

interpretação:

quantidade = 2
preço_unitario = 14.99

---

Entrada:

14,99 2

interpretação:

quantidade = 2
preço_unitario = 14.99

---

Entrada:

0,678 6,99

interpretação:

quantidade = 0.678
preço_unitario = 6.99

---

Entrada:

6,99 0,678

interpretação:

quantidade = 0.678
preço_unitario = 6.99

---

## 5. Cálculo

O cálculo deve ser realizado da seguinte forma:

preço_total = quantidade × preço_unitario

---

## 6. Arredondamento

O resultado deve ser arredondado para **2 casas decimais** utilizando arredondamento padrão.

Exemplo:

0.678 × 6.99 = 4.73922

Resultado exibido:

4.74

---

## 7. Validação

A entrada deve ser considerada válida apenas se:

* houver **exatamente dois números**
* um deles tiver **2 casas decimais**
* o outro for **inteiro ou tiver 3 casas decimais**

Entradas inválidas devem ser ignoradas.

---

# 04 — data-storage.md

```md
# Persistência de Dados

## 1. Armazenamento

Os dados devem ser armazenados no localStorage.

Chave utilizada:

supermarket_calculator

## 2. Estrutura

JSON array:

[
  {
    id: 1,
    quantidade: 2,
    preco_unitario: 14.99,
    preco_total: 29.98
  }
]

## 3. Comportamento

Sempre que um item é adicionado:

1. carregar array do localStorage
2. adicionar item
3. salvar novamente

## 4. Carregamento inicial

Ao carregar a página:

- verificar localStorage
- reconstruir tabela
- recalcular total

## 5. Reset

O botão "Resetar compra" deve:

1. apagar localStorage
2. limpar tabela
3. zerar total
```

---

# 05 — business-rules.md

```md
# Regras de Negócio

## 1. IDs

Os IDs devem ser sequenciais.

1,2,3,4...

## 2. Total geral

O total da compra deve ser calculado somando:

preco_total de cada item

## 3. Formatação monetária

Valores exibidos devem usar formato brasileiro:

R$ 29,98

## 4. Precisão

Internamente usar ponto decimal:

14.99

Na interface usar vírgula:

14,99

## 5. Validação

Entradas inválidas devem ser ignoradas.

Exemplos inválidos:

texto
apenas um número
mais de dois números

## 6. Performance

A aplicação deve funcionar instantaneamente,
sem dependência de rede.
```

# 06 — implementation-rules.md

* código deve ser claro
* usar funções pequenas
* evitar duplicação
* comentar parsing
