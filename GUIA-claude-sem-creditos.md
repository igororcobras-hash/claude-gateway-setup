# Claude Code com provedor alternativo (quando os créditos acabarem)

Este guia usa o gateway `Free-Claude-Code-Gateway` (https://github.com/rajakumar865465/Free-Claude-Code-Gateway), rodando no seu computador. Ele aceita **um provedor de cada vez**. Para trocar de provedor, use o painel admin ou o `.env`.

**Limites**
- O NVIDIA NIM não é suportado por este gateway (só pelo projeto `alishahryar1/free-claude-code`).
- O proxy não troca de provedor sozinho quando os créditos acabam. Você abre o Claude Code com as variáveis da seção 4.

## 1. Criar as chaves de API (você faz)

| Provedor | Onde criar | Uso |
|---|---|---|
| DeepSeek | https://platform.deepseek.com/api_keys | `BLUESMINDS_API_KEY` no `.env` |
| OpenRouter | https://openrouter.ai/keys | `BLUESMINDS_API_KEY` no `.env` |
| Kimi (Moonshot) | https://platform.moonshot.cn/console/api-keys | `BLUESMINDS_API_KEY` no `.env` |
| GLM (Z.ai) | https://z.ai/manage-apikey/apikey-list | `BLUESMINDS_API_KEY` no `.env` |

Não cole as chaves em nenhum arquivo deste repositório.

## 2. Instalar o gateway (no seu computador)

Pré-requisito: Node.js 20+ (https://nodejs.org).

```bash
git clone https://github.com/rajakumar865465/Free-Claude-Code-Gateway.git
cd Free-Claude-Code-Gateway
npm install
cp .env.example .env
npm run build
```

## 3. Configurar o provedor (arquivo `.env`)

Use o modelo `env.example.txt` deste repositório como referência. Exemplo para DeepSeek:

```env
BLUESMINDS_API_KEY=sua-chave-aqui
BLUESMINDS_BASE_URL=https://api.deepseek.com/v1
PORT=8787
DEFAULT_MODEL=deepseek-chat
```

**Atenção:** se `BLUESMINDS_BASE_URL` não for definido, o gateway usa um endereço padrão (`api.bluesminds.com`) que não é de nenhum dos provedores acima. Sempre defina essa variável.

| Provedor | BLUESMINDS_BASE_URL | DEFAULT_MODEL |
|---|---|---|
| DeepSeek | `https://api.deepseek.com/v1` | `deepseek-chat` |
| OpenRouter | `https://openrouter.ai/api/v1` | ex.: `deepseek/deepseek-chat` |
| Kimi | `https://api.moonshot.cn/v1` | `kimi-k2` |
| GLM (Z.ai) | `https://api.z.ai/api/paas/v4` | `glm-5.1` |

Inicie com `npm start` e deixe o terminal aberto. O gateway fica em `http://localhost:8787`.

## 4. Apontar o Claude Code para o gateway

Em outro terminal:

macOS/Linux:
```bash
export ANTHROPIC_BASE_URL=http://localhost:8787
export ANTHROPIC_AUTH_TOKEN=qualquer-coisa
claude
```

Windows (PowerShell):
```powershell
$env:ANTHROPIC_BASE_URL="http://localhost:8787"
$env:ANTHROPIC_AUTH_TOKEN="qualquer-coisa"
claude
```

Para voltar ao Claude oficial, abra um terminal novo sem essas variáveis.

## 5. Trocar de provedor

- **Painel admin:** `http://localhost:8787/admin` → **Settings** (vale na hora, sem reiniciar).
- **Arquivo `.env`:** troque as linhas da seção 3 e reinicie com `npm start`.

## 6. Testar

```bash
curl http://localhost:8787/v1/models
```

Se aparecer uma lista de modelos, o gateway está no ar.

## Segurança e privacidade

- O gateway roda em `localhost`, sem exposição na internet.
- Defina `ADMIN_PASSWORD` para proteger o painel.
- O que o Claude Code lê passa a ir para o provedor escolhido. Para documentos de licitação, confirme se isso é permitido.
