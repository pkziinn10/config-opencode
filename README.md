# Configuração global do OpenCode

Configuração global exportada de `~/.config/opencode`. Repositório não contém `node_modules`, estados, logs, backups ou credenciais.

## Instalação em outra máquina

Execute os comandos abaixo:

```bash
# 1. Faça backup da configuração existente
mv ~/.config/opencode ~/.config/opencode.backup.$(date +%Y%m%d-%H%M%S) 2>/dev/null || true
mkdir -p ~/.config/opencode

# 2. Clone este repositório
git clone https://github.com/pkziinn10/config-opencode.git /tmp/config-opencode

# 3. Copie conteúdo, incluindo arquivos ocultos, sem copiar .git
rsync -a --exclude='.git' /tmp/config-opencode/ ~/.config/opencode/
cd ~/.config/opencode

# 4. Instale dependências exatamente pelo lockfile
npm ci
```

## GitHub Copilot

Depois de instalar OpenCode e dependências, configure autenticação:

```bash
opencode auth login
```

Selecione `GitHub Copilot` e conclua o fluxo de autenticação no navegador. Não salve token em arquivos deste repositório.

## MCP cavemem

`opencode.jsonc` preserva configuração funcional local, mas caminho atual aponta para `/home/pk/.local/share/cavemem-fix`. Em outra máquina, escolha uma opção:

1. Instale/configure cavemem nesse mesmo caminho; ou
2. Instale cavemem de modo que `cavemem` esteja no `PATH` e altere o bloco `mcp.cavemem.command` para:

```jsonc
["cavemem", "mcp"]
```

3. Remova completamente `mcp.cavemem` de `opencode.jsonc` se não for usar esse MCP.

Valide a configuração iniciando `opencode` após escolher uma opção. Credenciais devem ser configuradas por login/ambiente local, nunca commitadas.
