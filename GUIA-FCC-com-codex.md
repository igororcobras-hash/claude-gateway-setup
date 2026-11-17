# FCC (Free Claude Code) com Claude Code e Codex no seu computador

Este guia instala o FCC (`alishahryar1/free-claude-code`) no seu computador, para usar Claude Code e Codex com provedores alternativos. Ele substitui o gateway anterior.

O FCC exige **Python 3.14.10 exatamente**. O `uv` instala essa versão para você, sem mexer no Python do sistema.

## 1. Pré-requisitos

- **Node.js 20+** (https://nodejs.org), para o Codex.
- **uv** (gerenciador do Python usado pelo FCC): https://docs.astral.sh/uv/getting-started/installation/

Instalar o `uv`:

Windows (PowerShell):
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

macOS/Linux:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Feche e reabra o terminal depois.

## 2. Instalar o Python 3.14.10

```bash
uv python install 3.14.10
```

## 3. Baixar e instalar o FCC

```bash
git clone https://github.com/alishahryar1/free-claude-code.git
cd free-claude-code
uv tool install --python 3.14.10 .
```

Isso instala os comandos `fcc-server`, `fcc-claude` e `fcc-codex`. **Não rode o `install.sh` completo**: ele instala cerca de doze ferramentas de terceiros que você não precisa.

## 4. Instalar o Codex (CLI da OpenAI)

```bash
npm install -g @openai/codex
```

## 5. Criar a chave do provedor (você faz)

Escolha um provedor e crie a chave. Não cole a chave no chat.

| Provedor | Onde criar |
|---|---|
| NVIDIA NIM (tem cota grátis) | https://build.nvidia.com/settings/api-keys |
| DeepSeek | https://platform.deepseek.com/api_keys |
| OpenRouter | https://openrouter.ai/keys |

## 6. Configurar o FCC

Depois de instalar, rode o servidor uma vez:

```bash
fcc-server
```

O FCC abre o painel admin no navegador. Em **Providers**, clique em **Add key**, cole a chave do provedor e clique em **Save**. Em **Model Router**, escolha o modelo. Clique em **Apply**.

Para proteger o painel com senha, ative **Proxy Authentication** no admin.

Deixe o terminal do `fcc-server` aberto.

## 7. Usar

Em outro terminal:

```bash
fcc-claude   # Claude Code
fcc-codex    # Codex
```

Os comandos usam o FCC automaticamente. Para voltar ao Claude oficial, use o comando `claude` direto, sem o prefixo `fcc-`.

## 8. Verificar a instalação

```bash
fcc-doctor
```

Se algum item falhar, copie a mensagem de erro e me envie.

## Privacidade

O que o Claude Code e o Codex leem passa a ir para o provedor escolhido. Para documentos de licitação, confirme se isso é permitido antes de usar.
