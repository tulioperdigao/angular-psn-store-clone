# Angular PSN Store (Projeto Acadêmico)

Clone educacional da vitrine da PlayStation™ Store desenvolvido com **Angular** para praticar conceitos fundamentais do framework (componentes, rotas, serviços, comunicação entre componentes, organização de pastas e boas práticas).

> **Aviso legal**: Marcas, nomes, imagens e ícones relacionados a PlayStation™ e/ou Sony pertencem aos seus respectivos detentores e são usados aqui apenas para fins educativos/didáticos.

---

## 📚 Sumário

- [Objetivos de Aprendizado](#-objetivos-de-aprendizado)
- [Stack & Requisitos](#-stack--requisitos)
- [Como Rodar Localmente](#-como-rodar-localmente)
- [Scripts Disponíveis](#-scripts-disponíveis)
- [Estrutura de Pastas](#-estrutura-de-pastas)
- [Arquitetura & Padrões](#-arquitetura--padrões)
- [Rotas (Router)](#-rotas-router)
- [Estilo & Qualidade de Código](#-estilo--qualidade-de-código)
- [Como Contribuir](#-como-contribuir)
- [Roadmap Sugerido (Acadêmico)](#-roadmap-sugerido-acadêmico)
- [Licença](#-licença)
- [Créditos](#-créditos)

---

## 🎯 Objetivos de Aprendizado

- Consolidar a base do **Angular** (componentes, templates, data binding, diretivas, pipes).
- Organizar um app em **módulos/feature folders** com **rotas** e **componentização**.
- Simular uma **vitrine** (listagem) e **páginas de detalhe** usando dados estáticos ou mockados.
- Aplicar **boas práticas** de estrutura, nomeação e separação de responsabilidades.

---

## 🧰 Stack & Requisitos

- **Node.js** (LTS recomendado)
- **npm** ou **pnpm**/**yarn**
- **Angular CLI** (instalação global recomendada)

> Verifique a versão instalada do Angular CLI:
>
> ```bash
> ng version
> ```

---

## 🚀 Como Rodar Localmente

1. **Clonar** o repositório e entrar na pasta do app:

   ```bash
   git clone https://github.com/tulioperdigao/angular-psn-store-clone.git
   cd angular-psn-store-clone/store
  ```
2. **Instalar** dependências:

```bash
npm install
# ou
pnpm install
```

3. **Subir** o servidor de desenvolvimento:

```bash
npm start
# ou
ng serve
```

4. **Acessar** no navegador:

```
http://localhost:4200
```

---

📦 Scripts Disponíveis
----------------------

> Os comandos abaixo seguem a convenção padrão do Angular CLI. Caso o `package.json` do projeto tenha variações, ajuste conforme necessário.

- **`npm start`** → `ng serve` com recarregamento automático.
- **`npm run build`** → build de produção em `dist/`.
- **`npm test`** → executa testes unitários (se configurados).
- **`npm run lint`** → roda o linter (se configurado).
- **`npm run format`** → formata o código (se configurado).

Build de produção manual:

```bash
ng build --configuration production
```

---

🗂️ Estrutura de Pastas
-----------------------

> Estrutura típica para apps Angular em formato de **feature folders**. Adapte aos nomes reais do seu projeto — a ideia é manter claro onde ficam “núcleo”, “compartilhado” e “features”.

```text
store/
├─ src/
│  ├─ app/
│  │  ├─ core/                # Serviços globais, guards, interceptors (sem dependência de componentes)
│  │  ├─ shared/              # Componentes, pipes e diretivas reutilizáveis (sem estado de negócio)
│  │  ├─ features/
│  │  │  ├─ home/             # Página inicial (vitrine/listagem)
│  │  │  ├─ search/           # Página de busca/resultado (opcional)
│  │  │  └─ not-found/        # Página 404
│  │  ├─ app-routing.module.ts
│  │  ├─ app.component.(ts|html|scss)
│  │  └─ app.config.(ts)      # ou app.module.ts, conforme versão/estilo do projeto
│  ├─ assets/                 # Imagens, ícones, fontes estáticas
│  ├─ environments/           # environment.ts e environment.prod.ts (se aplicável)
│  ├─ index.html
│  └─ styles.(scss|css)
├─ angular.json
├─ package.json
├─ tsconfig*.json
└─ README.md
```

---

🧱 Arquitetura & Padrões
------------------------

- **Componentização**: páginas (features) e componentes compartilhados em `shared/`.
- **Serviços (Services)**: acesso a dados (mock/JSON local) e lógica de negócio leve ficam em `core/` ou dentro da pasta da feature.
- **Modelos/Interfaces**: defina `Game`, `Platform`, etc. para tipagem forte com **TypeScript**.
- **Detecção de mudanças** (opcional): `ChangeDetectionStrategy.OnPush` para componentes de lista/detalhe com dados imutáveis.
- **Comunicação**: `@Input()`/`@Output()` entre componentes pais/filhos; serviços para estado compartilhado simples.
- **Mocks de dados**: JSONs em `assets/` e serviços que simulam chamadas HTTP (útil no contexto acadêmico).

Exemplo de interface:

```ts
export interface Game {
  id: string;
  title: string;
  price: number;
  platform: 'PS4' | 'PS5' | 'PS4/PS5';
  coverUrl: string;
  tags?: string[];
}
```

---

🧭 Rotas (Router)
-----------------

Rotas típicas para a vitrine:

```ts
export const routes = [
  { path: '', pathMatch: 'full', redirectTo: 'home' },
  { path: 'home', loadComponent: () => import('./features/home/home.component') },
  { path: 'search', loadComponent: () => import('./features/search/search.component') },
  { path: '**', loadComponent: () => import('./features/not-found/not-found.component') },
];
```

- **Home**: lista cards dos jogos (nome, plataforma, preço, “saiba mais”).
- **Search** (opcional): filtra jogos por termo (query param) e exibe contagem.
- **404**: página de “não encontrado” com link de retorno.

> Dica: use **query params** (`ActivatedRoute`) para busca sem perder o histórico do navegador.

---

🎨 Estilo & Qualidade de Código
-------------------------------

- **Prettier/ESLint** (recomendado): padronizam formatação e boas práticas.
- **Aliases de import** (opcional): configure no `tsconfig.json` (`paths`) para imports claros:

```json
{
  "compilerOptions": {
    "baseUrl": "src",
    "paths": {
      "@core/*": ["app/core/*"],
      "@shared/*": ["app/shared/*"],
      "@features/*": ["app/features/*"]
    }
  }
}
```

- **Acessibilidade**: texto alternativo em imagens, ordem de tabulação e contraste de cores.

---

🤝 Como Contribuir
------------------

1. Faça um **fork** do repositório.
2. Crie uma **branch** de feature:

```bash
git checkout -b feat/minha-feature
```

3. Commit claro seguindo **Conventional Commits** (sugerido):

```text
feat(home): adiciona destaque de jogos gratuitos
fix(search): corrige filtro por plataforma
docs(readme): atualiza instruções de setup
```

4. **Pull Request** explicando o que mudou e como testar.

---

🗺️ Roadmap Sugerido (Acadêmico)
--------------------------------

- [ ] **Busca** por título/plataforma com `queryParams`.
- [ ] **Pipes** para preço/formatação e filtros simples.
- [ ] **Paginação** (client-side) para a vitrine.
- [ ] **Estado** leve em serviço (favoritos, carrinho fake).
- [ ] **Guards** para rotas “privadas” (simulação didática).
- [ ] **Interceptors** para simular latência de rede e headers.
- [ ] **Testes** unitários (Jasmine/Karma) de componentes puros/pipes.
- [ ] **Build** e deploy estático (GitHub Pages, Vercel, Netlify).

---

📄 Licença
----------

Consulte o arquivo `LICENSE` na raiz do repositório (se presente). Em ausência de licença explícita, trate o código como **uso acadêmico/pessoal** apenas.

---

🙏 Créditos
-----------

- **PlayStation™ / Sony** — propriedade intelectual e identidade visual originais.
- Este projeto é **não-oficial** e com **propósito educacional**.
