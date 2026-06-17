# Fluxo — meu lucro real

PWA de controle financeiro para motorista de app e autônomo. Lança a renda **por dia de
trabalho** (não corrida a corrida), gerencia **contas a pagar** com vencimento, e mostra o
**lucro líquido real** depois de todos os custos — incluindo o rateio das contas, que os apps
de motorista escondem.

- 100% offline depois de instalado · funciona em **Android e iPhone**
- Dados ficam **só no seu aparelho** (localStorage) — nada vai pra servidor
- Backup por JSON (restaura tudo), envio direto pro Drive/e-mail, e exportação CSV
- PIN de acesso opcional · sem conta, sem custo, sem dependências externas

## Telas

| Aba | O que faz |
|-----|-----------|
| **Hoje** | Lança renda do dia e despesas; mostra líquido real, % de custo sobre o bruto, progresso da meta e quanto precisa tirar por dia pra pagar as contas |
| **Contas** | Contas fixas e variáveis com vencimento; marca como paga; conta vencida e não paga fica em destaque; suporta "repete todo mês" |
| **Relatório** | Bruto, líquido, saldo livre, reserva do Leão, R$/km (ganho, custo, líquido), ponto de equilíbrio, projeção de fechamento, custo do dia parado, pizza de gastos e renda por fonte |
| **Ajustes** | Dias rodados/mês, meta diária, custo de manutenção/km, % de reserva pro imposto, PIN e backup |

## Como as contas funcionam

```
Líquido do dia  = renda do dia − despesas do dia − (total das contas do mês ÷ dias rodados)
Precisa/dia     = contas em aberto ÷ dias de trabalho restantes no mês
Líquido do mês  = renda do mês − despesas variáveis − contas do mês
Saldo livre     = (renda − gasto − contas pagas) − contas em aberto − reserva do Leão
Custo por km    = custo total do mês ÷ km total do mês   (média do mês, não do dia)
```

> **Por que o R$/km é do mês, não do dia:** o combustível é lançado só quando abastece, mas
> os km são lançados todo dia. Num dia sem abastecer, o custo do dia daria "zero" e o R$/km
> sairia mentirosamente alto. A média mensal (combustível do mês ÷ km do mês) é o número real.

## Rotina de uso

1. **Fim do dia:** lance em **Renda** o total que caiu da Uber/bico naquele dia, e os km rodados.
2. **Ao abastecer:** lance em **Despesa → Combustível** o valor (não precisa de horário certo).
3. **Contas:** cadastre uma vez em **Contas** (aluguel do carro, seguro, celular…). Marque "Paguei" quando pagar. As mensais reaparecem automaticamente no mês seguinte.
4. **De vez em quando:** **Ajustes → Enviar backup** (manda pro Drive). O app avisa quando faz tempo.

## Deploy na GitHub Pages (grátis)

Suba **todos** os arquivos na raiz do repositório:

```
index.html  manifest.json  sw.js  icon-192.png  icon-512.png  icon-maskable.png
```

Depois: **Settings → Pages → Deploy from a branch → main / (root) → Save**.
Em ~1 min sai a URL: `https://SEU-USUARIO.github.io/Fluxo/` (respeite maiúsculas/minúsculas do nome do repo).

> Requer HTTPS (a GitHub Pages já é) pro service worker e a instalação funcionarem.

## Instalar como app

**Android (Chrome):** abra a URL → menu **⋮ → Instalar aplicativo**.

**iPhone (Safari):** abra a URL no **Safari** → botão **Compartilhar** → **Adicionar à Tela de Início**.
No iPhone não há botão automático; o próprio app mostra esse lembrete. O iOS pode limpar o
cache quando o aparelho fica sem espaço, então no iPhone o backup periódico é ainda mais importante.

## Privacidade e segurança

O código é público (é só a lógica do app), mas **nenhum dado financeiro vai pro GitHub**.
Tudo é processado e guardado no navegador do próprio aparelho. Quem abre o link recebe o app
zerado, com o próprio armazenamento local. Indicar pra outra pessoa não expõe seus dados.
O PIN é uma barreira de tela (não criptografia) — protege de olhares, complementando o
bloqueio do celular.

## Stack

HTML + CSS + JavaScript puro (vanilla). Zero build, zero dependência, um único `index.html`
com a lógica. Service worker para offline. Armazenamento via `localStorage` com fallback em
memória.
