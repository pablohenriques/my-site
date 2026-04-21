# 🌍 Intercâmbio de Inglês — Comparativo de Destinos

Levantamento completo de custos para intercâmbio de inglês com foco em **brasileiros que trabalham remotamente**. Compara preços de cursos, passagens, custo de vida, regras de imigração e comprovação financeira entre diferentes países.

**[→ Acessar o site]([https://seuusuario.github.io/intercambio-ingles/](https://github.com/pablohenriques/my-site))**

---

## Países incluídos

| País | Gasto total (2m) | Visto | Inglês oficial | Destaque |
|------|-------------------|-------|----------------|----------|
| 🇵🇱 Polônia | ~R$ 25 mil | Não precisa (Schengen) | Não | Mais barato da Europa continental |
| 🇨🇦 Canadá | ~R$ 42 mil | Sim (CAD $185) | Sim | Até 6 meses, voo direto |
| 🇲🇹 Malta | ~R$ 24 mil | Não precisa (Schengen) | Sim (oficial) | Transporte grátis, visto nômade |
| 🇮🇪 Irlanda | ~R$ 30 mil | Não precisa | Sim (nativo) | Fora do Schengen, pode trabalhar |

---

## Como publicar no GitHub Pages

```bash
# 1. Clone ou crie o repositório
git clone https://github.com/seuusuario/intercambio-ingles.git
cd intercambio-ingles

# 2. Renomeie o arquivo principal
mv intercambio.html index.html

# 3. Commit e push
git add .
git commit -m "Publicação inicial do comparativo"
git push origin main

# 4. No GitHub: Settings → Pages → Source: main / root
# O site estará em: https://seuusuario.github.io/intercambio-ingles/
```

---

## Como adicionar um novo país

O site é um único arquivo HTML autossuficiente. Para adicionar um novo país você precisa alterar **3 partes** do `index.html`:

### Passo 1 — Defina a cor do país no CSS

Dentro do bloco `<style>`, na seção `:root`, adicione uma variável de cor:

```css
:root {
  /* ... cores existentes ... */
  --novopaís: #cor_hexadecimal;
}
```

E adicione a regra para o botão da tab ficar colorido quando ativo:

```css
.tab[data-c="novopaís"].active { background: var(--novopaís); color: #fff; }
```

### Passo 2 — Adicione o objeto de dados no JavaScript

No bloco `<script>`, dentro do objeto `countries`, adicione uma nova entrada. Cada país é definido assim:

```javascript
const EUR = 6.35;   // cotação Euro → Real
const PLN = 1.39;   // cotação Zloty → Real
const CAD = 3.64;   // cotação Dólar Canadense → Real
// Adicione a cotação da moeda do novo país se necessário

const countries = {
  // ... países existentes ...

  novopaís: {
    flag:      '🇽🇽',              // emoji da bandeira
    name:      'Nome do País',      // nome em português
    color:     'var(--novopaís)',    // referência à variável CSS
    passagem:  5000,                // passagem ida+volta em R$ (média)
    cursoMes:  800 * EUR,           // custo mensal do curso convertido para R$
    vidaMes:   1500 * EUR,          // custo de vida mensal convertido para R$ (sem curso)
    seguroDia: 12,                  // custo diário do seguro viagem em R$
    visto:     0,                   // custo do visto em R$ (0 se isento)
    fundosFn:  d => 100 * d * EUR,  // função: recebe dias (d), retorna comprovação em R$
    fuso:      '+3h',               // diferença de fuso em relação a Brasília
    inglês:    'Sim',               // o país fala inglês? 'Sim', 'Não', ou 'Sim ✦' (destaque)
    schengen:  'Sim',               // faz parte do Schengen? 'Sim', 'Não', ou 'Não ✦'
    transporte:'Pago',              // 'Pago' ou 'GRÁTIS ✦'
    limite:    '90 dias',           // limite de permanência como turista
    nomad:     'Não',               // tem visto nômade digital? 'Sim ✦' ou 'Não'
  },
};
```

Depois, inclua a chave do novo país no array `keys`:

```javascript
const keys = ['poland', 'canada', 'malta', 'ireland', 'novopaís'];
```

### Passo 3 — Adicione a aba e a seção HTML

**Aba de navegação** — dentro de `<nav class="tabs">`, adicione:

```html
<button class="tab" data-c="novopaís" onclick="show('novopaís')">
  <span class="flag">🇽🇽</span> Nome do País
</button>
```

**Seção de conteúdo** — antes do `</main>`, adicione uma nova `<section>`. Use a estrutura dos países existentes como modelo:

```html
<section class="country" id="sec-novopaís">

  <!-- IMIGRAÇÃO -->
  <div class="card">
    <div class="card-title" style="color:var(--novopaís)">🛂 Imigração</div>
    <h3>Resumo das regras de entrada</h3>
    <p>Descrição geral das regras...</p>

    <div class="chk-item">
      <span class="chk-badge obr">OBR</span>
      <div>
        <h4>Nome do documento obrigatório</h4>
        <p>Descrição e valores.</p>
      </div>
    </div>

    <div class="chk-item">
      <span class="chk-badge rec">REC</span>
      <div>
        <h4>Nome do documento recomendado</h4>
        <p>Descrição.</p>
      </div>
    </div>

    <div class="alert alert-info">
      <strong>Título do alerta:</strong> Informação complementar.
    </div>
  </div>

  <!-- CURSOS -->
  <div class="card">
    <div class="card-title" style="color:var(--novopaís)">📚 Cursos de Inglês</div>
    <div class="school">
      <div>
        <div class="school-name">Nome da Escola</div>
        <div class="school-type">Tipo do curso (ex: Intensivo 20h/sem)</div>
      </div>
      <div>
        <div class="school-price" style="color:var(--novopaís)">€XXX/mês</div>
        <div class="school-brl">≈ R$ XXX/mês</div>
      </div>
      <div class="school-note">Observação sobre a escola</div>
    </div>
  </div>

  <!-- CUSTO DE VIDA -->
  <div class="card">
    <div class="card-title" style="color:var(--novopaís)">🏠 Custo de Vida Mensal</div>
    <div class="data-row">
      <span class="label">Aluguel (1 quarto, centro)</span>
      <span class="value">€XXX–XXX · R$ XXX–XXX</span>
    </div>
    <!-- ... mais itens ... -->
  </div>

  <!-- PASSAGENS -->
  <div class="card">
    <div class="card-title" style="color:var(--novopaís)">✈️ Passagens & Seguro</div>
    <div class="data-row">
      <span class="label">Passagem ida e volta (média)</span>
      <span class="value">R$ X.XXX</span>
    </div>
  </div>

</section>
```

### Passo 4 — Adicione a coluna na tabela comparativa

No `<thead>` da tabela `#cmp-table`, adicione:

```html
<th><span class="flag">🇽🇽</span> Nome</th>
```

O JavaScript gera as linhas automaticamente a partir do objeto `countries`.

---

## Roteiro de pesquisa para um novo país

Para levantar os dados de um novo destino, pesquise as informações abaixo. Esse foi o roteiro usado para os 4 países já incluídos:

### 1. Imigração e visto

- Brasileiro precisa de visto prévio? Quanto custa?
- Qual o limite de permanência como turista?
- O país faz parte do Espaço Schengen?
- Existe visto de nômade digital? Quais os requisitos?
- Qual a comprovação financeira exigida na fronteira / no visto?
- Quais documentos o oficial de imigração pode exigir na chegada?

Fontes sugeridas: site oficial de imigração do país, Mundial Vistos, VisaHQ, gov.br (MRE).

### 2. Cursos de inglês

- Quais as principais escolas de inglês para estrangeiros?
- Preço por semana ou mês dos cursos intensivos (20–30h/semana)?
- Existem descontos para cursos longos (long-term)?
- Turmas são grandes ou pequenas?

Fontes sugeridas: LanguageCourse.net, Language International, sites das escolas.

### 3. Custo de vida mensal

- Aluguel de 1 quarto no centro e periferia (em moeda local e R$)
- Alimentação (supermercado, comer fora)
- Transporte público (passe mensal)
- Internet e celular
- Lazer e extras
- Utilidades (água, luz, gás)

Fontes sugeridas: Numbeo, Expatistan, blogs de intercambistas brasileiros.

### 4. Passagens aéreas

- Há voo direto do Brasil? De qual aeroporto?
- Preço médio ida e volta (alta e baixa temporada)
- Principais companhias aéreas e tempo de voo

Fontes sugeridas: KAYAK, Skyscanner, Mundi, Decolar.

### 5. Trabalho remoto

- Qual o fuso horário em relação a Brasília?
- Qualidade da internet no país
- Existem coworkings acessíveis?
- Restrições legais para trabalho remoto como turista?

### 6. Seguro viagem

- É obrigatório? Qual a cobertura mínima exigida?
- Preço médio por dia em R$

Fontes sugeridas: Seguros Promo, Assistente de Viagem.

### 7. Câmbio

- Qual a moeda local?
- Cotação atual em relação ao Real (R$)

Fontes sugeridas: Wise, Investing.com, Remessa Online.

---

## Estrutura de arquivos

```
intercambio-ingles/
├── index.html      ← site completo (arquivo único, sem dependências)
└── README.md       ← este arquivo
```

O site é intencionalmente um único arquivo HTML para simplificar a publicação e contribuição. Não há build, framework ou dependências além do Google Fonts.

---

## Classes CSS disponíveis

| Classe | Uso |
|--------|-----|
| `.card` | Container principal de seção |
| `.card-title` | Título de seção (caixa alta, espaçado) |
| `.data-row` | Linha de dado (label + valor) |
| `.school` | Card de escola de idiomas |
| `.chk-item` | Item de checklist (documento obrigatório/recomendado) |
| `.chk-badge.obr` | Badge vermelha "OBR" |
| `.chk-badge.rec` | Badge dourada "REC" |
| `.alert.alert-info` | Caixa azul informativa |
| `.alert.alert-warn` | Caixa amarela de atenção |
| `.alert.alert-danger` | Caixa vermelha de perigo |
| `.alert.alert-ok` | Caixa verde positiva |
| `.tip` | Dica com ícone |
| `.total-box` | Caixa de valor total destacado |
| `.cmp-table` | Tabela comparativa |
| `.flag` | Emoji de bandeira |

---

## Fórmulas de cálculo

Todas as estimativas seguem a mesma lógica:

```
Gasto total = passagem + (cursoMes × meses) + (vidaMes × meses) + (seguroDia × dias) + visto

Comprovação = fundosFn(dias)   ← varia por país, ver regra específica

Valor em conta = gasto total + comprovação + 1 mês reserva de emergência (vidaMes)
```

A comprovação financeira de cada país segue regras diferentes:

| País | Regra | Fórmula |
|------|-------|---------|
| 🇵🇱 Polônia | 75 zł/dia + 2.500 zł retorno | `(75 × dias + 2500) × PLN` |
| 🇨🇦 Canadá | ~CAD 2.500/mês de estadia | `2500 × meses × CAD` |
| 🇲🇹 Malta | ~€100/dia (padrão Schengen) | `100 × dias × EUR` |
| 🇮🇪 Irlanda | €500/semana | `500 × semanas × EUR` |

---

## Cotações utilizadas (abril/2026)

| Moeda | Câmbio |
|-------|--------|
| 1 EUR (Euro) | R$ 6,35 |
| 1 PLN (Zloty) | R$ 1,39 |
| 1 CAD (Dólar Canadense) | R$ 3,64 |

Ao adicionar um novo país com moeda diferente, defina a constante de câmbio no início do `<script>`.

---

## Contribuindo

1. Fork este repositório
2. Pesquise o novo país seguindo o roteiro acima
3. Edite o `index.html` seguindo os 4 passos da seção "Como adicionar um novo país"
4. Teste localmente abrindo o arquivo no navegador
5. Abra um Pull Request com as fontes das informações

Ao contribuir, inclua no PR as fontes utilizadas para cada dado (sites oficiais, Numbeo, escolas, etc.) e a data da pesquisa.

---

## Licença

Este projeto é de uso livre. Os dados são baseados em fontes públicas e sujeitos a alteração. Consulte sempre os sites oficiais de imigração antes de tomar decisões.

---

*Levantamento original realizado em abril de 2026.*
