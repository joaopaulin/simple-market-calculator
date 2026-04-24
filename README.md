# SMC — Calculadora de Mercado Simples (Simple Market Calculator)

Esta é uma calculadora de mercado minimalista projetada para registrar itens durante suas compras e acompanhar o valor total em tempo real, diretamente no seu celular.

A ferramenta foca na rapidez de inserção, utilizando um sistema inteligente que identifica automaticamente preços e quantidades sem a necessidade de alternar entre campos.

## 🚀 Acessar a aplicação

A calculadora está disponível em: [https://joaopaulin.github.io/smc](https://joaopaulin.github.io/smc)

---

## 📖 Manual de Uso

O segredo do **SMC** é a simplicidade. Você não precisa preencher vários campos; basta digitar e confirmar.

### Como adicionar itens

O sistema reconhece o tipo de entrada com base na quantidade de casas decimais que você digita.

#### 1. Item unitário
Quando você quer adicionar apenas um item pelo seu preço.
*   **Como fazer:** Digite o preço com **duas casas decimais**.
*   **Exemplo:** 1 pacote de macarrão que custa R$ 4,29.
    *   Digite: `4,29` e pressione `[ENTER]`

#### 2. Múltiplas unidades
Quando você leva mais de uma unidade de um produto com preço fixo.
*   **Como fazer:** Digite a quantidade (número inteiro) e o preço (duas casas decimais), separados por um espaço. A ordem não importa.
*   **Exemplo:** 2 unidades de feijão que custam R$ 5,64 cada.
    *   Digite: `2 5,64` ou `5,64 2` e pressione `[ENTER]`

#### 3. Produtos por peso (Hortifruti/Açougue)
Ideal para itens pesados na balança.
*   **Como fazer:** Digite o peso (com três casas decimais) e o preço por quilo (com duas casas decimais), separados por um espaço.
*   **Exemplo:** 0,634 kg de banana a R$ 6,48 o quilo.
    *   Digite: `0,634 6,48` ou `6,48 0,634` e pressione `[ENTER]`

---

## 🛒 Na prática: Exemplo de uma compra

Imagine que você está no corredor do supermercado. Veja como seria o preenchimento da sua lista:

1.  **Pegou um pacote de macarrão (R$ 4,29):**
    *   No teclado do app, você digita apenas `4,29` e aperta `ENTER`.
    *   *O sistema já entende que é 1 unidade e o total vira R$ 4,29.*

2.  **Chegou nos grãos e pegou 2 pacotes de feijão (R$ 5,64 cada):**
    *   Você digita `2 5,64` e aperta `ENTER`.
    *   *O sistema calcula 2x R$ 5,64 e o total da compra sobe para R$ 15,57.*

3.  **Na balança, pesou um cacho de bananas (0,634 kg a R$ 6,48/kg):**
    *   Você olha o adesivo da balança e digita `0,634 6,48` e aperta `ENTER`.
    *   *O sistema calcula o peso exato e o total acumulado sobe para R$ 19,68.*

---

### 💡 Dicas Importantes

*   **Reconhecimento Automático:** Para o sistema entender o que é preço, use sempre **duas casas decimais** (ex: `5,00` em vez de `5`). Para pesos, use sempre **três casas decimais** (ex: `0,500`).
*   **Total Instantâneo:** O valor total da sua compra é atualizado no rodapé da tela assim que você adiciona um item.
*   **Remover Itens:** Errou algo? Clique no ícone da **Lixeira** ao lado do item e confirme a exclusão.
*   **Limpar Lista:** Para começar uma nova compra, clique em **"RESETAR COMPRA"** no final da página.
*   **Não perde os dados:** Você pode fechar o navegador ou sair da página. Sua lista fica salva automaticamente no armazenamento local do seu celular e estará lá quando você abrir o app novamente.

---

## 🛠 Tecnologias
- HTML5, CSS3 (Bootstrap 5) e JavaScript Puro.
- Persistência via `localStorage`.
- Interface otimizada para dispositivos móveis.

