# /prompt-criativo

Skill do Claude Code (iConvert) que monta o prompt de geração de imagem (GPT por padrão; serve para Nano Banana e Midjourney) de um criativo estático a partir de copy já aprovada, da identidade visual do cliente e da foto fornecida. Não escreve copy.

## Instalar

Copiar a pasta `prompt-criativo/` para `~/.claude/skills/` (global) ou para `.claude/skills/` do projeto. Depois é só chamar `/prompt-criativo` no Claude Code.

## Como funciona

1. Lê o `contexto.md` do cliente e a pasta `identidade-visual/` (hex, fonte, logo).
2. Recebe a copy pronta: gancho (até ~9 palavras), apoio (até 12 ou nenhum), rodapé, botão.
3. Define regime da foto (intocada, composição livre, sem foto) e formato (4:5, 9:16, 1:1).
4. Monta o prompt em inglês com o texto em português verbatim, compliance do nicho e canto livre para o logo.
5. Registra o prompt em `clientes/<cliente>/criativos/PROMPTS-<campanha>.md`.

Regras de copy que a skill exige (vêm da `/roteiro-anuncio` e da `/limpa-ia`): zero travessão, sem termos de IA, sem promessa de resultado, linha Bastidores obrigatória.

Origem: estáticos da masterclass do Thomáz (R+), 07/09/2026. Limite de texto na imagem definido em 08/09/2026.
