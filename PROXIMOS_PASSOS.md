# Pr�ximos Passos � NeuroGame Platform

Com backend, admin e launcher funcionando, os pr�ximos passos recomendados focam em qualidade, opera��o e evolu��o do produto.

## 1. Qualidade e testes

- [ ] Adicionar testes unit�rios no backend (Jest + Supertest)
- [ ] Criar su�te end-to-end (Playwright ou Cypress) cobrindo login, gest�o no admin e execu��o de jogo no launcher
- [ ] Configurar verifica��o autom�tica de lint/format (ESLint + Prettier)

## 2. Observabilidade

- [ ] Integrar logs estruturados no backend (pino/winston)
- [ ] Adicionar monitoramento (Logflare/Sentry) para admin e launcher
- [ ] Configurar m�tricas b�sicas (requests/min, erros, lat�ncia)

## 3. Deploy e infra

- [ ] Publicar backend em servi�o gerenciado (Render, Railway, Fly.io)
- [ ] Publicar admin (Vercel/Netlify) apontando para a API p�blica
- [ ] Empacotar launcher (`npm run build && npm run build:win` etc.)
- [ ] Automatizar releases com GitHub Actions (build + upload artefatos)

## 4. Produto

- [ ] Implementar fluxo de atualiza��o autom�tica no launcher (`check-for-updates`)
- [ ] Integrar pagamentos/assinaturas (ex.: Stripe) para planos Basic/Premium
- [ ] Criar p�gina p�blica apresentando a plataforma (landing page)
- [ ] Planejar novos jogos e conte�do

## 5. Seguran�a

- [ ] Rotacionar periodicamente as chaves do Supabase (anon/service)
- [ ] Habilitar 2FA nas contas administrativas
- [ ] Revisar pol�ticas RLS e permiss�es na tabela `users`
- [ ] Implementar auditoria de a��es cr�ticas no backend

## 6. Documenta��o cont�nua

- [ ] Registrar changelog por release
- [ ] Adicionar diagramas atualizados de arquitetura
- [ ] Documentar endpoints no Swagger/OpenAPI
- [ ] Criar manual de opera��o para suporte

## 7. Roadmap sugerido (30-60 dias)

1. Semana 1-2: testes automatizados + pipeline CI/CD
2. Semana 3-4: deploy p�blico + observabilidade
3. Semana 5-6: pagamento e melhorias no launcher
4. Semana 7-8: novos jogos, landing page e documenta��o extra

Com esses passos, o projeto evolui de um MVP funcional para um produto pronto para escala e manuten��o cont�nua.
