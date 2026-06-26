# Hermes Agent - Memory Vault Index

> **Vault principal do Agente Hermes** — Camada de memória escalonável no Google Drive
> Pasta raiz: `HermesAgent` (ID: `1H4Ruo5tCllUXOVhXUWZNvtnXYYOX_Gwf`)

---

## 📁 Estrutura do Vault

```
HermesAgent/
├── 00_Inbox/              # Captura rápida, triagem posterior
├── 10_Projects/           # Projetos ativos com início/fim definidos
├── 20_Areas/              # Áreas de responsabilidade contínua
├── 30_Resources/          # Referências, pesquisa, material de apoio
├── 40_Archive/            # Projetos/áreas concluídos ou inativos
├── Templates/             # Modelos de notas reutilizáveis
├── Attachments/           # Imagens, PDFs, arquivos anexados
└── Hermes_Agent_Memory/   # Memória persistente do agente
```

---

## 🤖 Hermes_Agent_Memory — Memória do Agente

Esta pasta armazena a **memória de longo prazo** do Hermes entre sessões:

| Arquivo | Propósito |
|---------|-----------|
| `agent-profile.md` | Identidade, capacidades, preferências do agente |
| `user-profile.md` | Perfil do usuário, preferências, contexto pessoal |
| `project-registry.md` | Registro de projetos ativos/históricos |
| `skills-learned.md` | Skills criadas, adaptadas, lições aprendidas |
| `conversation-index.md` | Índice de conversas importantes por tópico |
| `decisions-log.md` | Log de decisões arquiteturais e escolhas técnicas |
| `api-keys-ref.md` | Referências a chaves/segredos (valores no secret manager) |

---

## 🔗 Links Rápidos

- [[Templates/Daily Note]]
- [[Templates/Project Note]]
- [[Templates/Meeting Note]]
- [[Templates/Research Note]]
- [[Hermes_Agent_Memory/agent-profile]]
- [[Hermes_Agent_Memory/user-profile]]

---

## 📋 Convenções

- **Nomes de arquivos:** `kebab-case` (ex: `project-alpha.md`)
- **Títulos:** `# Título Principal` (H1 único por nota)
- **Datas:** ISO 8601 `YYYY-MM-DD` em frontmatter e nomes
- **Tags:** `#tag` no corpo ou `tags: [tag1, tag2]` no frontmatter
- **Links:** `[[WikiLink]]` para notas internas, `[texto](url)` para externos

---

## 🔄 Sincronização

- **Fonte da verdade:** Google Drive (`HermesAgent` folder)
- **Obsidian:** Abre a pasta do Drive como vault local
- **Hermes:** Acessa via Google Drive API (OAuth configurado)
- **Backup:** Automático via Google Drive sync

---

*Última atualização: {{date:YYYY-MM-DD}}*
*Criado pelo Hermes Agent durante setup inicial*