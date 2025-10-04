# Solu��o � Launcher Desktop NeuroGame

## Situa��o atual

- Scripts `npm run dev` e `npm start` utilizam `wait-on`, `cross-env` e `npx electron` para garantir que o processo correto seja iniciado em Windows, macOS e Linux.
- `main.js` detecta `ELECTRON_RUN_AS_NODE` e relan�a o bin�rio do Electron quando necess�rio, evitando o erro `app.whenReady is not a function`.
- Logs adicionais (`[launcher] isDev�` e handlers `did-fail-load` / `console-message`) ajudam a diagnosticar problemas de build ou de carregamento de jogos.

## Checklist de sa�de do launcher

1. **Depend�ncias instaladas** � `npm install`
2. **Frontend em modo dev** � porta `5174` livre
3. **Backend rodando** � `http://localhost:3000`
4. **CORS** � `CORS_ORIGIN` inclui `http://localhost:5174`
5. **Pasta `Jogos/`** � cont�m subpastas com `index.html`
6. **Credenciais v�lidas** � login `demo/Demo@123456` dispon�vel

## Fluxo recomendado

```bash
# Backend
cd neurogame-backend
npm run dev

# Admin dashboard
cd ../neurogame-admin
npm run dev

# Launcher
cd ../neurogame-launcher
npm run dev
```

## Troubleshooting r�pido

| Sintoma | A��o |
|--------|------|
| Terminal mostra `Failed to load dist/index.html` ao usar `npm start` | Rode `npm run build` antes de `npm start` |
| Login falha com erro CORS | Ajuste `CORS_ORIGIN` no backend para incluir a origem do launcher |
| WebView exibe mensagem de erro | Verifique se `Jogos/<folder>/index.html` existe e se `folder_path` no Supabase corresponde |
| Nada acontece ao rodar `npm run dev` | Confirme instala��o de depend�ncias e se `wait-on`/`cross-env` est�o presentes em `devDependencies` |

## Refer�ncia r�pida de arquivos importantes

- `main.js` � janela principal, fix `ELECTRON_RUN_AS_NODE`, IPCs
- `preload.js` � API exposta ao renderer
- `src/services/api.js` � cliente Axios com leitura das configura��es em `electron-store`
- `src/services/storage.js` � persist�ncia de token/usu�rio/configura��o
- `src/pages/GameDetail.jsx` � valida��o de acesso e montagem do caminho local do jogo

## Pr�ximos passos sugeridos

- Automatizar update de CORS e vari�veis via documenta��o atualizada
- Implementar rotina de auto-update (placeholder no IPC `check-for-updates`)
- Adicionar testes end-to-end (ex.: Playwright) para validar login e abertura de jogos

Com essas corre��es o launcher est� funcional e alinhado ao backend Supabase e ao dashboard admin.
