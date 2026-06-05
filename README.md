# Home Gym Tracker

Fichas de treino **full-body por perfil** para treinar em casa. Página única, sem dependências, sem build step — abre no navegador e funciona. Pensado para **halteres ajustáveis + peso do corpo**.

![stack](https://img.shields.io/badge/stack-HTML%20%C2%B7%20CSS%20%C2%B7%20JS%20vanilla-c6ff3a) ![sem build](https://img.shields.io/badge/build-nenhum-15181d) ![mobile first](https://img.shields.io/badge/mobile-first-3ad1ff)

## Features

- **2 perfis independentes**, cada um com a sua própria ficha e foco:
  - **Talys** — foco em **peito**
  - **Andressa** — foco em **glúteos**
  - Trocar de perfil troca a ficha inteira. Nomes editáveis (toque no ✎).
- **Split A/B + aquecimento** por perfil, com abas.
- Cada exercício mostra **grupo muscular**, **séries × reps**, **dica de execução** e botão **Vídeo** (busca no YouTube).
- **Marcação de séries** persistente: clique nos quadradinhos — fica salvo no aparelho.
- **Barra de progresso** por treino.
- **Concluir treino** registra a data no **histórico** (com calendário do mês, total, contagem do mês e dos últimos 7 dias) e zera as marcações pro próximo treino.
- **Timer de descanso** fixo com presets **60s / 90s / 2min** e **vibração** ao terminar (mobile).
- Visual **mobile-first**, tema escuro, tipografia [Anton](https://fonts.google.com/specimen/Anton) + [Manrope](https://fonts.google.com/specimen/Manrope).
- Conteúdo em **português**.

## Equipamento previsto

As fichas usam apenas **um par de halteres ajustáveis (30 kg)** e o **peso do corpo** — sem banco, barra fixa ou máquinas. Movimentos que normalmente pedem banco foram adaptados para o chão (floor press, crucifixo no chão) ou para apoio em sofá/cadeira (hip thrust, búlgaro, remada unilateral). Cardio sugerido: corrida ou natação.

## Persistência (importante)

Os dados (marcações e histórico) ficam no **`localStorage` do navegador de cada aparelho**, separados por perfil. Ou seja: o histórico do celular de uma pessoa **não** sincroniza automaticamente com o de outro aparelho. Os 2 perfis servem para quando o **mesmo** aparelho é usado pelos dois. Para sincronizar entre celulares no futuro, dá para plugar um backend (ex.: Supabase).

## Como rodar

Não há instalação:

```bash
open index.html        # macOS
xdg-open index.html    # Linux

# ou servidor local (útil para acessar de outro device na mesma rede)
python3 -m http.server 8000   # http://localhost:8000
```

Hospedado de graça via **GitHub Pages**.

## Deploy no GitHub Pages

1. `git push` para a branch `main`.
2. GitHub → **Settings → Pages** → **Source: Deploy from a branch** → branch **`main`**, pasta **`/ (root)`** → **Save**.
3. Em ~1 min: `https://<seu-usuario>.github.io/home-gym-tracker/`

No celular, abra o link e use **"Adicionar à Tela de Início"** para virar um ícone de app.

## Como customizar / montar uma ficha nova

Tudo é gerado a partir do objeto `PLANS` no final do `index.html`. Cada perfil tem `focus`, `labels` (subtítulo das abas) e `treinos` com as listas `A`, `B`. O aquecimento (`AQUECIMENTO`) é compartilhado.

```js
const PLANS = {
  u1: {
    focus: "Peito",
    labels: { A: "Peito + Empurrar", B: "Puxar + Pernas", warm: "Prepara o corpo" },
    treinos: {
      A: [
        { nome: "Supino no chão (floor press) com halteres",
          musculo: "Peito", series: 4, reps: "10",
          dica: "Deitado no chão, empurre até esticar e desça até o cotovelo tocar o chão." },
        // ...
      ],
      B: [ /* ... */ ]
    }
  },
  u2: { /* Andressa — Glúteos */ }
};
```

Campos de cada exercício:

| Campo     | Descrição                                            |
|-----------|------------------------------------------------------|
| `nome`    | Nome do exercício (também alimenta a busca do vídeo) |
| `musculo` | Grupo muscular trabalhado                            |
| `series`  | Número de séries (gera os quadradinhos clicáveis)    |
| `reps`    | Repetições por série (texto livre: `"12"`, `"10/perna"`, `"40s"`, `"máx"`) |
| `dica`    | Dica curta de execução                               |

### Receita para criar uma ficha com foco em outro músculo

1. **Escolha o músculo-alvo** (ex.: costas, ombro, pernas) e coloque **2–3 exercícios desse grupo no início do Treino A**, quando você está mais forte. É o "foco".
2. **Complete o resto do corpo** com 1 exercício por grupo grande (puxar, empurrar, pernas, core), pra não desequilibrar.
3. **Volume por grupo:** ~10–16 séries semanais no músculo-foco (somando A+B), ~6–10 nos demais. Reps: força 6–10, hipertrofia 10–15.
4. **Compostos antes de isoladores** (ex.: agachamento antes de cadeira; supino antes de crucifixo).
5. **Progrida** semana a semana: mais carga nos halteres, mais reps, ou descida mais lenta (tempo sob tensão).
6. Edite o `PLANS`, salve, `git push` — o site atualiza sozinho.

## Licença

[MIT](LICENSE) © 2026 Talys Cordeiro
