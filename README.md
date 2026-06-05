# Home Gym Tracker

Ficha de treino **full-body A/B** interativa para treinar em casa. Página única, sem dependências, sem build step — abre no navegador e funciona.

![stack](https://img.shields.io/badge/stack-HTML%20%C2%B7%20CSS%20%C2%B7%20JS%20vanilla-c6ff3a) ![sem build](https://img.shields.io/badge/build-nenhum-15181d) ![mobile first](https://img.shields.io/badge/mobile-first-3ad1ff)

## Features

- **Split A/B full-body** + aba de **aquecimento**
  - **Treino A** — empurrar + quadríceps
  - **Treino B** — puxar + posterior
- Cada exercício mostra **grupo muscular**, esquema de **séries × reps**, uma **dica de execução** e um botão **Vídeo** que abre uma busca no YouTube.
- **Marcação de séries**: clique nos quadradinhos para marcar cada série concluída.
- **Barra de progresso** por treino, atualizada conforme você marca as séries.
- **Timer de descanso** fixo no rodapé com presets **60s / 90s / 2min** e **vibração** ao terminar (em dispositivos móveis compatíveis).
- Visual **mobile-first**, tema escuro com cor de destaque, tipografia [Anton](https://fonts.google.com/specimen/Anton) + [Manrope](https://fonts.google.com/specimen/Manrope).
- Conteúdo em **português**.

> O estado das séries fica **apenas em memória** — ao recarregar a página, a ficha volta limpa para o próximo treino.

## Como rodar

Não há instalação. Escolha uma das opções:

```bash
# Opção 1 — abrir direto
open index.html        # macOS
xdg-open index.html    # Linux

# Opção 2 — servidor local (recomendado em mobile na mesma rede)
python3 -m http.server 8000
# depois acesse http://localhost:8000
```

## Deploy no GitHub Pages

1. Faça push do projeto para a branch `main`.
2. No GitHub: **Settings → Pages**.
3. Em **Source**, selecione **Deploy from a branch**.
4. Escolha a branch **`main`** e a pasta **`/ (root)`**, e clique em **Save**.
5. Em ~1 minuto o app fica disponível em:
   `https://<seu-usuario>.github.io/home-gym-tracker/`

Pelo terminal, com o [GitHub CLI](https://cli.github.com/):

```bash
gh api -X POST repos/<seu-usuario>/home-gym-tracker/pages \
  -f "source[branch]=main" -f "source[path]=/"
```

## Como customizar

Toda a ficha é gerada a partir de um objeto de dados no final do `index.html`. Para alterar exercícios, edite o objeto `TREINOS`:

```js
const TREINOS = {
  A: [
    { nome: "Agachamento Goblet", musculo: "Quadríceps / Glúteo", series: 4, reps: "12",
      dica: "Desça com o peito erguido e os joelhos alinhados aos pés." },
    // ...adicione, remova ou edite exercícios à vontade
  ],
  B: [ /* ... */ ],
  warm: [ /* aquecimento */ ]
};
```

Campos de cada exercício:

| Campo     | Descrição                                            |
|-----------|------------------------------------------------------|
| `nome`    | Nome do exercício (também alimenta a busca do vídeo) |
| `musculo` | Grupo muscular trabalhado                            |
| `series`  | Número de séries (gera os quadradinhos clicáveis)    |
| `reps`    | Repetições por série (texto livre: `"12"`, `"10/perna"`, `"40s"`) |
| `dica`    | Dica curta de execução                               |

As cores do tema ficam nas variáveis CSS em `:root` (`--accent`, `--a-color`, `--b-color`, `--warm-color`).

## Licença

[MIT](LICENSE) © 2026 Talys Cordeiro
