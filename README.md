# ALTUSMED Faturamento — PWA

App de faturamento da NGM/ALTUSMED: cadastro de médicos, lançamento de voos
(com trechos terrestres), regulações e geração dos relatórios de pagamento em
PDF no padrão visual ALTUSMED — tudo no navegador, sem servidor. Os dados ficam
salvos no próprio aparelho (localStorage) e o app funciona offline após o
primeiro acesso.

## Arquivos

| Arquivo | Função |
|---|---|
| `index.html` | O app inteiro (interface + dados seed + geração de PDF) |
| `jspdf.umd.min.js` | Biblioteca de PDF (local, funciona offline) |
| `manifest.webmanifest` | Manifesto PWA (nome, ícones, cores) |
| `sw.js` | Service worker (cache para uso offline) |
| `icon-192.png` / `icon-512.png` / `apple-touch-icon.png` | Ícones |

## Publicar no GitHub Pages (uma vez só)

1. Crie um repositório no GitHub (ex.: `altusmed-faturamento`). Pode ser
   **privado? Não** — para GitHub Pages no plano gratuito o repositório
   precisa ser **público**. Como o app não contém dados de pacientes no
   código (só os dados seed de competências já faturadas e chaves Pix que
   já circulam nos seus relatórios), avalie se prefere remover o seed antes
   de publicar — veja "Privacidade" abaixo.
2. Envie os arquivos desta pasta para o repositório (botão **Add file →
   Upload files** no site do GitHub resolve, sem precisar de git).
3. No repositório: **Settings → Pages → Build and deployment →
   Source: Deploy from a branch → Branch: `main` / `(root)` → Save**.
4. Em 1–2 minutos o app estará em
   `https://SEU-USUARIO.github.io/altusmed-faturamento/`.

## Instalar na tela do iPhone

1. Abra o endereço acima no **Safari**.
2. Toque no botão **Compartilhar** (quadrado com seta para cima).
3. Toque em **Adicionar à Tela de Início** → **Adicionar**.
4. O ícone ALTUSMED aparece como um app; abre em tela cheia e funciona
   offline.

## Como usar

- **Médicos** — cadastro completo (nome, CRM, CPF, chave Pix, banco/agência/
  conta, contato) e a marcação **"Indicado por mim"**, que gera a comissão
  configurável (15% por padrão) sobre o total de cada missão (aéreo +
  terrestre) daquele médico.
- **Voos** — data, origem/destino (com opção ida-e-volta), km, paciente,
  valor do voo e, se houver, trechos terrestres com quantidade e valor.
- **Regulações** — data/hora, origem, destino, paciente e valor (padrão
  R$ 180,00, configurável).
- **Relatório** — escolha a competência e gere:
  1. **Honorários Médicos** — voos do mês + cards Pix por médico (para a
     AeroTop pagar aos profissionais);
  2. **Cobrança NGM** — indicações (15%) + regulações, com Pix/banco da NGM
     e o cartão CNPJ como Anexo I.
- **Ajustes** — percentual de comissão, valor da regulação, dados bancários,
  assinatura, e **backup** (exportar/importar JSON).

## Dados e privacidade

- Os lançamentos ficam **apenas no aparelho** (localStorage do navegador).
  Nada é enviado a servidor algum.
- Por isso, **exporte o backup JSON de vez em quando** (Ajustes → Exportar).
  Se o iPhone limpar os dados do Safari, o backup restaura tudo.
- O `index.html` traz pré-carregados os dados já faturados (JUN e OUT/2026)
  e os dados Pix dos médicos. Se não quiser isso num repositório público,
  me peça uma versão com o seed vazio — os dados podem ser importados depois
  pelo backup JSON no próprio aparelho.

## Limitações conhecidas (até o AERIS assumir)

- Sem multiusuário/nuvem: cada aparelho tem seus próprios dados.
- O nº do documento é gerado como `REL-PAG-AAAA-MM/BEL-01` e `/NGM-01`
  (sempre `-01`; se emitir dois relatórios no mesmo mês, renomeie o PDF).
- O voo de 27/10/2026 veio do relatório anterior sem médico definido —
  aparece como "sem médico definido" na aba Voos; edite e atribua quando
  souber.
