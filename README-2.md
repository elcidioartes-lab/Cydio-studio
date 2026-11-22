# CYDIO STUDIO — versão inicial

Painel administrativo demonstrativo para **CYDIO — HISTÓRIAS EM MÚSICA**.

## O que está incluído

- Interface responsiva em Next.js + TypeScript.
- Dashboard do CYDIO STUDIO.
- Catálogo inicial com as sete músicas indicadas.
- Gestão demonstrativa de músicas: adicionar, editar, pesquisar e remover da interface.
- Formulários para história, letra e interpretação.
- Estrutura de cliente Supabase para browser e servidor.
- Middleware base para atualização da sessão Supabase.
- Esquema SQL inicial com RLS para Supabase.
- Exemplo de variáveis de ambiente.

## Importante: estado desta versão

Esta entrega é um **starter funcional de interface**, não uma loja publicada.
As alterações feitas no painel ainda ficam apenas no estado do navegador e desaparecem ao atualizar a página. Autenticação, gravação persistente, upload real de MP3, Stripe, emissão de faturas e publicação pública ainda precisam de configuração e implementação.

Não introduzas chaves secretas neste projeto. Nunca coloques a chave `service_role` do Supabase no browser.

## Requisitos

- Node.js 20.9 ou superior
- npm
- Conta Supabase para a fase de ligação à base de dados

## Instalação local

```bash
npm install
cp .env.example .env.local
npm run dev
```

Abre `http://localhost:3000`.

O painel pode ser explorado sem Supabase, em modo de demonstração. As funções reais de autenticação e dados só devem ser ativadas depois de configurar as variáveis e concluir as políticas de acesso.

## Ligar Supabase

1. Cria um projeto no Supabase.
2. Copia a Project URL e a chave anon/publishable.
3. Coloca-as em `.env.local`.
4. Abre o SQL Editor do Supabase e executa `supabase/schema.sql`.
5. Cria o utilizador administrador em Supabase Auth.
6. Atribui `app_metadata.role = admin` ao utilizador através de um processo confiável no servidor ou Supabase Dashboard. Nunca permitas que o utilizador altere a própria função.
7. Cria o bucket privado `cydio-audio`.
8. Configura políticas de Storage para que apenas o administrador possa carregar e apenas utilizadores autorizados possam obter áudio completo.

O SQL inclui políticas de leitura e administração das tabelas, mas não cria automaticamente todas as políticas de Storage.

## Estrutura

```text
cydio-studio/
├── src/
│   ├── app/
│   │   ├── globals.css
│   │   ├── layout.tsx
│   │   └── page.tsx
│   ├── components/
│   │   └── Studio.tsx
│   ├── lib/
│   │   └── supabase/
│   │       ├── client.ts
│   │       └── server.ts
│   └── middleware.ts
├── supabase/
│   └── schema.sql
├── .env.example
├── package.json
├── postcss.config.mjs
└── README.md
```

## Próximas entregas técnicas

1. Autenticação de administrador e proteção real de `/studio`.
2. CRUD persistente de histórias e músicas.
3. Upload de capas, MP3 completos e prévias.
4. Leitor de áudio com URLs assinados.
5. Loja, checkout Stripe e webhook de confirmação.
6. Área de cliente e biblioteca de compras.
7. Domínio, publicação, privacidade, faturação e testes.

## Marca e domínio

Marca pública: `CYDIO ARTISTA`  
Produto: `CYDIO — HISTÓRIAS EM MÚSICA`  
Domínio pretendido: `cydio.com` (disponibilidade e registo por confirmar).
