# NeuroGame Platform

Plataforma completa para distribui��o e execu��o de jogos educacionais composta por tr�s aplica��es:

1. **Backend API** � Node.js/Express conectado ao Supabase (PostgreSQL gerenciado)
2. **Dashboard Admin** � React + Vite para gest�o de usu�rios, jogos e planos
3. **Launcher Desktop** � Electron + React para os jogadores acessarem a biblioteca

A pasta `Jogos/` cont�m os jogos HTML5 executados pelo launcher.

## Vis�o geral da arquitetura

```
[Launcher (Electron/React)] <-- REST --> [Backend API (Express)] <---> [Supabase]
             ^
             |
   [Admin Dashboard (React)]
```

- Backend exp�e `/api/v1` com autentica��o JWT e guarda estado no Supabase
- Admin dashboard consome a API para CRUD de jogos, usu�rios e assinaturas
- Launcher consome a mesma API e carrega os jogos HTML5 da pasta local `Jogos/`

## Requisitos

- Node.js 18+
- Conta Supabase (Free tier suficiente)
- Git / npm

## Passo a passo r�pido

1. **Clonar o reposit�rio**
   ```bash
   git clone <repo>
   cd NeuroGame
   ```

2. **Configurar Supabase**
   - Criar projeto no Supabase
   - Executar `supabase-schema.sql` e `supabase-seeds.sql` via SQL Editor
   - Copiar `SUPABASE_URL`, `SUPABASE_ANON_KEY`, `SUPABASE_SERVICE_KEY`

3. **Backend** (`neurogame-backend`)
   ```bash
   cp .env.example .env
   # Preencher credenciais Supabase + chaves JWT
   npm install
   npm run dev
   ```
   - API: `http://localhost:3000/api/v1`
   - Jogos est�ticos: `http://localhost:3000/games/<pasta>`

4. **Admin** (`neurogame-admin`)
   ```bash
   cp .env.example .env   # API base default j� aponta para http://localhost:3000/api/v1
   npm install
   npm run dev
   ```
   - Interface: `http://localhost:3001`
   - Login padr�o: `admin / Admin@123456`

5. **Launcher** (`neurogame-launcher`)
   ```bash
   npm install
   npm run dev
   ```
   - Renderer em `http://localhost:5174`
   - Janela Electron abre automaticamente
   - Login padr�o: `demo / Demo@123456`
   - Jogos esperados em `../Jogos/<folder>/index.html`

## Estrutura do reposit�rio

```
NeuroGame/
+- neurogame-backend/
�  +- src/
�  +- supabase-schema.sql
�  +- supabase-seeds.sql
+- neurogame-admin/
�  +- src/
+- neurogame-launcher/
�  +- src/
+- Jogos/
�  +- autorama/
�  +- balao/
�  +- ... (14 jogos)
+- docs (*.md)
```

## Documenta��o �til

- `SUPABASE_SETUP.md` � passo a passo completo de configura��o do Supabase
- `IMPLEMENTACAO_ADMIN.md` � descri��o do dashboard admin
- `IMPLEMENTACAO_LAUNCHER.md` � descri��o do launcher Electron
- `INICIO_RAPIDO.md` � vis�o geral do fluxo de inicializa��o
- `SOLUCAO_LAUNCHER.md` e `INICIAR_LAUNCHER_COMPLETO.md` � troubleshooting do launcher

## Pr�ximos passos sugeridos

- Configurar CI/CD para publicar o backend e o dashboard
- Adicionar testes automatizados (unit�rios e end-to-end)
- Implementar rotina de auto-update no launcher
- Integrar pagamentos para planos de assinatura

## Licen�a

MIT
