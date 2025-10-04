# Guia de Implementa��o � Dashboard Admin (React + Vite)

Resumo da estrutura atual do painel administrativo NeuroGame.

## Estrutura de diret�rios

```
neurogame-admin/
+- src/
�  +- App.jsx
�  +- main.jsx
�  +- assets/
�  +- components/
�  �  +- GameCard.jsx
�  �  +- GameForm.jsx
�  �  +- Header.jsx
�  �  +- Layout.jsx
�  �  +- PlanCard.jsx
�  �  +- PlanForm.jsx
�  �  +- Sidebar.jsx
�  �  +- UserForm.jsx
�  �  +- UserTable.jsx
�  +- contexts/
�  �  +- AuthContext.jsx
�  +- pages/
�  �  +- Dashboard.jsx
�  �  +- Games.jsx
�  �  +- Login.jsx
�  �  +- Subscriptions.jsx
�  �  +- Users.jsx
�  +- services/
�  �  +- api.js
�  +- utils/
�     +- auth.js
+- vite.config.js
+- package.json
+- .env (opcional)
```

## Fluxo principal (`App.jsx`)

- Estado global (`user`, `setUser`) armazenado pelo `AuthContext`.
- `useEffect` inicial busca `localStorage` via `getUser()`.
- Componente `ProtectedRoute` � definido dentro de `App.jsx` e verifica:
  1. `loading` (exibe spinner);
  2. exist�ncia de usu�rio logado;
  3. flag `is_admin`.
- Rotas:
  - `/login` ? `pages/Login.jsx`
  - `/` (dentro do `Layout`) ? `Dashboard`, `Games`, `Users`, `Subscriptions`.

## Autentica��o

- `pages/Login.jsx` chama `authAPI.login` (em `services/api.js`).
- Resposta populada com `token`, `refreshToken` e `user`.
- Persist�ncia feita por `utils/auth` (`setAuthData` usa `localStorage`).
- Interceptor Axios renova tokens via `/api/v1/auth/refresh-token` quando recebe 401.

## Servi�os (`services/api.js`)

- `API_BASE_URL` vem de `import.meta.env.VITE_API_URL` (por padr�o `http://localhost:3000/api/v1`).
- Interceptores cuidam de anexar `Authorization: Bearer <token>` e tentam refresh autom�tico.
- Objetos helpers (`authAPI`, `usersAPI`, `gamesAPI`, `subscriptionsAPI`) normalizam respostas do Supabase para a UI (campos como `isAdmin`, `folderPath`, `durationDays`).

## Componentes-chave

- `Layout.jsx`: combina `Sidebar`, `Header` e `Outlet` do React Router.
- `Sidebar.jsx`: navega��o entre se��es, destaca rota ativa.
- `Header.jsx`: exibe usu�rio logado e bot�o de logout (limpa storage e redireciona para `/login`).
- `GameForm.jsx`, `PlanForm.jsx`, `UserForm.jsx`: formul�rios com valida��o b�sica para CRUD.
- `UserTable.jsx`: tabela de usu�rios com pagina��o e a��es.

## P�ginas

- `Dashboard.jsx`: m�tricas resumidas (usu�rios ativos, jogos, planos, etc.).
- `Games.jsx`: listagem com filtros, modal de cria��o/edi��o, acionando `gamesAPI`.
- `Users.jsx`: gerenciamento de usu�rios e concess�o de acesso individual.
- `Subscriptions.jsx`: CRUD de planos + associa��o de jogos ao plano.
- `Login.jsx`: tela estilizada com MUI, �cones e toggles de visibilidade de senha.

## Ambiente e scripts

- Copiar `.env.example` ? `.env` para definir `VITE_API_URL` e `VITE_API_TIMEOUT`.
- Scripts (`package.json`):
  - `npm run dev` � Vite em `http://localhost:3001`
  - `npm run build` � build produ��o em `dist/`
  - `npm run preview` � serve build gerado

## Integra��o com backend

- Depende do backend Express/Supabase em `http://localhost:3000`.
- Necess�rio que CORS inclua `http://localhost:3001`.
- Dados devem coincidir com as tabelas do Supabase (`games`, `subscription_plans`, etc.)

## Fluxo de logout

1. `Header` ? `logout` (fun��o em `utils/auth`).
2. Remove `token`, `refreshToken` e `user` do `localStorage`.
3. Limpa dados extras no backend (`electronAPI` n�o � usado aqui) e redireciona para `/login`.

## Pontos de aten��o

- O dashboard assume que os campos retornados pelo Supabase seguem os nomes utilizados na normaliza��o (`full_name`, `folder_path`, `is_active`).
- Atualize `VITE_API_URL` ao publicar o backend em outro host.
- Tokens gravados em `localStorage`; considere cookies HttpOnly em produ��o se necess�rio.

## Execu��o t�pica

```bash
# Instalar depend�ncias
npm install

# Desenvolvimento
npm run dev

# Build
npm run build
```

Abra `http://localhost:3001`, fa�a login com `admin / Admin@123456` (criado via seeds do Supabase) e gerencie usu�rios, jogos e planos.
