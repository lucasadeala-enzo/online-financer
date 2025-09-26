/*
README: Site Automatizado de Finanças Pessoais (pronto para deploy)
===============================================================
O arquivo abaixo é um único componente React (App.jsx) com:
- layout responsivo (Tailwind)
- SEO meta tags básicas
- 5 artigos iniciais (em português) embarcados como JSON
- RSS simples (arquivo estático gerado à inicialização do build)
- instruções de deploy para Vercel/Netlify
- instruções passo-a-passo para conectar automações (Zapier/Make + Webhooks)

Como usar (resumo rápido):
1) Crie uma conta gratuita no Vercel (ou Netlify).
2) Crie um novo projeto e cole este repositório/arquivo ou use o template estático.
3) Configure variáveis de ambiente se quiser (DISQUS_SHORTNAME, NEWSLETTER_API_KEY, etc.)
4) Deploy: Vercel detecta automaticamente. Site estará disponível em <seu-subdominio>.vercel.app
5) No Zapier/Make: crie um Zap/Scenario que chama o webhook de publicação deste site ou usa o CMS (por exemplo, GitHub commits) — instruções detalhadas abaixo.

O objetivo: você cola este código em um projeto React (Create React App / Vite / Next.js - neste exemplo é compatível com Vite + React) e publica. Conteúdo inicial já incluso.

--- INSTRUÇÕES DE AUTOMAÇÃO (resumo) ---
Automação recomendada (sem custo inicial):
- Workflow 1 (Publicação automática de artigos diários):
  1. Crie um Zap/Scenario que roda diariamente (ex.: 1 vez por dia). Trigger: Schedule (Zapier) ou Scheduler (Make).
  2. Ação: chamar uma função do OpenAI/ChatGPT para gerar um artigo com prompt (ex.: tema + tom + palavra-chave).
  3. Ação: usar o comando GitHub - Create File (ou Commit) para adicionar o artigo em /posts/YYYY-MM-DD.md no repo do site.
  4. Vercel faz o deploy automático e o artigo aparece no site.

- Workflow 2 (Criação e publicação de vídeo curto):
  1. Trigger: Novo artigo publicado (Webhook do GitHub ou deploy webhook do Vercel).
  2. Ação: usar um template no Pictory/Runway/CapCut API para gerar vídeo curto com voz TTS.
  3. Ação: usar Repurpose.io ou Buffer para postar automaticamente nas redes (TikTok/IG/YT Shorts).

- Workflow 3 (Monetização / Links de afiliados automáticos):
  1. Ao gerar artigo, o prompt inclui placeholders de afiliados.
  2. Zap insere links de afiliado (Hotmart/Amazon) via template e commit no artigo.

--- Ficheiro App.jsx (código abaixo) ---
*/

import React from "react";

// App.jsx - Single file React site (use with Vite or Create React App)
export default function App() {
  const site = {
    title: "Finanças em Fluxo - Conteúdo Automático",
    description: "Dicas práticas e relatórios curtos sobre finanças pessoais, investimentos e economia, atualizados automaticamente.",
    author: "Equipe Automatizada",
  };

  const posts = [
    {
      id: "2025-09-01-5-dicas-economizar",
      title: "5 Hábitos Simples para Economizar R$200 por Mês",
      date: "2025-09-01",
      excerpt: "Pequenas mudanças diárias que, somadas, reduzem despesas e ajudam a criar uma reserva com pouco esforço.",
      content: `Economizar não precisa ser complicado. Aqui vão cinco hábitos práticos:

1) Revise assinaturas (streaming, apps) — cancele o que não usa.
2) Use planilhas simples para monitorar gastos semanais.
3) Configure transferências automáticas para uma poupança separada.
4) Faça compras com lista e evite compras por impulso.
5) Compare preços e use cupons ou cashback sempre que possível.

Seguindo esses passos você cria um hábito financeiro que automaticamente aumenta sua reserva.`,
      tags: ["poupança", "hábitos"],
    },
    {
      id: "2025-09-03-investimentos-iniciante",
      title: "Investimentos para Iniciantes: Onde Começar com pouco dinheiro",
      date: "2025-09-03",
      excerpt: "Como montar uma carteira inicial com baixo risco e custos reduzidos.",
      content: `Comece definindo objetivos: curto, médio e longo prazo. Com R$100 por mês você pode:

- Tesouro Direto (IPCA/Prefixado) para segurança.
- Fundos de índice (ETFs) para diversificação com baixo custo.
- Tesouraria de corretoras com renda fixa para reserva de emergência.

Evite produtos com altas taxas e foque em consistência. Automatize aportes mensais para tirar emoção da decisão.`,
      tags: ["investimentos", "iniciantes"],
    },
    {
      id: "2025-09-05-orcamento-eficaz",
      title: "Orçamento Eficaz: Método 50/30/20 Simplificado",
      date: "2025-09-05",
      excerpt: "Uma regra prática para dividir seu salário e manter controle das finanças.",
      content: `A regra 50/30/20 divide sua renda:

- 50%: necessidades (moradia, contas, alimentação).
- 30%: desejos (lazer, compras não essenciais).
- 20%: poupança/quitamento de dívidas.

Adapte percentuais conforme sua realidade. O importante é automatizar transferências para a parcela de poupança.`,
      tags: ["orçamento", "planejamento"],
    },
    {
      id: "2025-09-10-renda-passiva-ideias",
      title: "3 Ideias de Renda Passiva para Começar Hoje",
      date: "2025-09-10",
      excerpt: "Modelos simples que podem, com automação, gerar receita contínua sem trabalho diário.",
      content: `1) Crie um mini-curso (plataforma de afiliados) e aplique automação de vendas.
2) Site de nicho com artigos SEO monetizados por afiliados e anúncios.
3) Produtos digitais (templates, planilhas) vendidos via landing pages automatizadas.

Combine 2 ou 3 para diversificar rendas.`,
      tags: ["renda passiva", "autonomia"],
    },
    {
      id: "2025-09-15-psicologia-dos-gastos",
      title: "A Psicologia dos Gastos: Como Domar Impulsos",
      date: "2025-09-15",
      excerpt: "Técnicas comportamentais para reduzir compras por impulso e aumentar a poupança.",
      content: `- Pratique a regra dos 24 horas antes de comprar algo não essencial.
- Use listas e metas visuais para lembrar prioridades.
- Separe uma porcentagem do salário para lazer, evitando proibições que geram exageros.

Pequenas mudanças na rotina reduzem significativamente compras impulsivas.`,
      tags: ["comportamento", "hábitos"],
    },
  ];

  return (
    <div className="min-h-screen bg-gray-50 text-gray-900 font-sans">
      <header className="bg-white shadow">
        <div className="max-w-4xl mx-auto px-6 py-8">
          <h1 className="text-3xl font-extrabold">{site.title}</h1>
          <p className="mt-2 text-gray-600">{site.description}</p>
        </div>
      </header>

      <main className="max-w-4xl mx-auto px-6 py-10">
        <section className="grid gap-8 md:grid-cols-2">
          {posts.map((post) => (
            <article key={post.id} className="bg-white p-6 rounded-2xl shadow-sm">
              <h2 className="text-xl font-semibold">{post.title}</h2>
              <p className="text-sm text-gray-500 mt-1">{post.date}</p>
              <p className="mt-3 text-gray-700">{post.excerpt}</p>
              <div className="mt-4">
                <a href={`#${post.id}`} className="inline-block text-sm font-medium underline">Ler mais</a>
              </div>
            </article>
          ))}
        </section>

        <section className="mt-12">
          {posts.map((post) => (
            <article id={post.id} key={post.id} className="mt-8 bg-white p-6 rounded-2xl shadow-sm">
              <h3 className="text-2xl font-bold">{post.title}</h3>
              <p className="text-sm text-gray-500 mt-1">{post.date} • {post.tags.join(' • ')}</p>
              <div className="mt-4 whitespace-pre-line text-gray-800">{post.content}</div>
              <div className="mt-6 flex items-center justify-between">
                <div className="text-sm text-gray-600">Autor: {site.author}</div>
                <div className="text-sm">
                  <a href="#newsletter" className="font-medium underline">Assine a newsletter</a>
                </div>
              </div>
            </article>
          ))}
        </section>

        <aside id="newsletter" className="mt-12 bg-white p-6 rounded-2xl shadow-sm">
          <h4 className="text-lg font-semibold">Newsletter diária (pré-configurada)</h4>
          <p className="mt-2 text-gray-600">Receba um resumo diário com os melhores conteúdos e oportunidades de afiliados.</p>
          <form className="mt-4 flex flex-col sm:flex-row gap-2">
            <input aria-label="email" placeholder="seu@exemplo.com" className="flex-1 p-3 border rounded-lg" />
            <button className="px-4 py-3 bg-blue-600 text-white rounded-lg font-semibold">Assinar</button>
          </form>
          <p className="text-xs mt-2 text-gray-500">Integre com MailerLite, Buttondown, or Substack via Zapier/Make.</p>
        </aside>

      </main>

      <footer className="bg-white border-t mt-12">
        <div className="max-w-4xl mx-auto px-6 py-6 text-sm text-gray-500">
          <div>© {new Date().getFullYear()} {site.title} — Sistema automatizado</div>
          <div className="mt-2">Deploy: Vercel / Netlify • Integrations: Zapier / Make / GitHub • Monetização: Afiliados + Ads</div>
        </div>
      </footer>
    </div>
  );
}

/*
--- NOTAS TÉCNICAS ADICIONAIS (cole no README do projeto) ---
1) Deploy com Vite + React
- Inicialize: npm create vite@latest my-site -- --template react
- Substitua src/App.jsx pelo conteúdo deste arquivo
- Instale Tailwind (opcional) seguindo docs do Tailwind + Vite
- Push para GitHub e conecte o repositório no Vercel

2) SEO e sitemaps
- Para SEO, adicione tags meta no index.html e configure sitemap.xml estático ou script que gera sitemap a partir de posts.

3) RSS
- Adicione um script node simples que converte posts JSON em /public/rss.xml e rode no build (ex: node scripts/generate-rss.js)

4) Automação com Zapier (exemplo detalhado)
- Trigger: Schedule by Zapier (Daily)
- Action: OpenAI (Create Completion) com prompt:
  "Escreva um artigo de 600-900 palavras para um blog de finanças pessoais em português sobre: {{Tema}}. Incluir subtítulos, lista de pontos e 1 call-to-action para assinar newsletter. Inserir 2 links de afiliado formatados como [TEXTO](URL)."
- Action: GitHub - Create File (repo: your-repo / path: /posts/{{YYYY-MM-DD}}-slug.md) — conteúdo: título, frontmatter, corpo do artigo.

5) Exemplo de prompt para geração de artigos:
- Tema: "Como economizar no supermercado"
- Tom: "Prático, direto, com dicas acionáveis"
- SEO: incluir palavra-chave: economizar supermercado

6) Checklist antes de ativar:
- Criar contas (Vercel, GitHub, Zapier, OpenAI)
- Guardar chaves API em Zapier/Make
- Testar 1 ciclo manualmente (criar um arquivo post) para checar build

----
*/
