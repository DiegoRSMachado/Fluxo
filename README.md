# Fluxo — meu lucro real

PWA de controle financeiro diário para autônomo (Uber/99/InDrive + freelas). Registra renda
e despesa do dia, rateia os custos fixos mensais por dia rodado e mostra o **lucro líquido
real** — a conta que os apps de motorista escondem.

- 100% offline depois de instalado (service worker)
- Dados ficam **só no teu aparelho** (localStorage), nada vai pra servidor
- Backup/restauração em JSON e exportação CSV (Excel/Sheets)
- Sem dependência externa, sem conta, sem custo

## O que cada aba faz

| Aba | Função |
|-----|--------|
| **Hoje** | Lança renda/despesa, mostra líquido do dia, % de custo sobre o bruto e progresso da meta |
| **Mês** | Bruto, líquido real, dias rodados, custo/km, para onde vai o dinheiro, renda por fonte |
| **Fixos** | Custos fixos mensais + config (dias/mês, meta diária, custo manutenção por km) |
| **Backup** | Exporta/importa JSON, exporta CSV, apaga tudo |

## Como a conta funciona

```
Líquido do dia = Renda do dia − Despesas variáveis do dia − (Σ custos fixos ÷ dias rodados/mês)
Líquido do mês = Renda do mês − Despesas variáveis do mês − Σ custos fixos
```

## Deploy na GitHub Pages (grátis)

1. Cria um repositório novo, ex: `fluxo`.
2. Sobe **todos** estes arquivos na raiz:
   ```
   index.html  manifest.json  sw.js  icon-192.png  icon-512.png  icon-maskable.png
   ```
3. No repo: **Settings → Pages → Source: Deploy from a branch → Branch: `main` / `(root)` → Save**.
4. Aguarda ~1 min. A URL sai como `https://diegoRSmachado.github.io/fluxo/`.

> Precisa ser **HTTPS** (a GitHub Pages já é) pro service worker e a instalação funcionarem.

## Instalar no Android

1. Abre a URL no **Chrome**.
2. Menu **⋮ → Instalar app** (ou "Adicionar à tela inicial").
3. Abre pelo ícone — roda em tela cheia, offline, como app nativo.

## Backup (importante)

localStorage some se tu limpar os dados do navegador. Entra em **Backup → Exportar (.json)**
de vez em quando e guarda o arquivo. Pra restaurar em outro aparelho: **Importar (.json)**.

## Stack

HTML + CSS + JavaScript puro (vanilla), zero build, zero dependência. ~1 arquivo.
