# HermesAgent + Obsidian + Google Drive

> **Camada de memória escalonável, persistente e compartilhável** para o [Hermes Agent](https://github.com/NousResearch/hermes-agent) usando Obsidian como interface e Google Drive como backend de armazenamento.

---

## 🎯 Visão Geral

Este repositório contém a **estrutura versionável** do vault Obsidian usado pelo Hermes Agent como memória de longo prazo. O Google Drive serve como *single source of truth* (fonte única da verdade), sincronizando automaticamente entre máquinas via Google Drive for Desktop.

```
┌─────────────────────────────────────────────────────────────┐
│                    GOOGLE DRIVE (Cloud)                     │
│  Pasta: HermesAgent (ID: 1H4Ruo5tCllUXOVhXUWZNvtnXYYOX_Gwf) │
└─────────────────────┬───────────────────────────────────────┘
                      │ Sync bidirecional
                      ▼
┌─────────────────────────────────────────────────────────────┐
│              GOOGLE DRIVE FOR DESKTOP (Local)               │
│  Caminho: G:\Meu Drive\DO NOT DELETE\HermesAgent           │
└─────────────────────┬───────────────────────────────────────┘
                      │ Abre como vault
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                        OBSIDIAN                             │
│  Interface visual • Plugins • Templates • Graph view       │
└─────────────────────┬───────────────────────────────────────┘
                      │ File tools (read/write/search)
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                      HERMES AGENT                           │
│  OAuth Google Workspace • Skills • Memory • Delegation     │
└─────────────────────────────────────────────────────────────┘
```

---

## 📁 Estrutura do Vault (Método PARA)

```
HermesAgent/
├── 00_Inbox/              # 📥 Captura rápida → triagem semanal
├── 10_Projects/           # 🎯 Projetos ativos (início/fim definidos)
├── 20_Areas/              # 🔄 Áreas de responsabilidade contínua
├── 30_Resources/          # 📚 Referências, pesquisa, material de apoio
├── 40_Archive/            # 📦 Projetos/áreas concluídos ou inativos
├── Templates/             # 📋 Modelos reutilizáveis (ver abaixo)
├── Attachments/           # 📎 Imagens, PDFs, arquivos (só no Drive)
├── Hermes_Agent_Memory/   # 🤖 Memória persistente do agente (privado)
│   ├── agent-profile.md
│   ├── user-profile.md
│   ├── project-registry.md
│   ├── skills-learned.md
│   ├── decisions-log.md
│   ├── conversation-index.md
│   └── api-keys-ref.md
└── Vault Index.md         # 📍 Índice principal e convenções
```

> **Baseado no método PARA** de Tiago Forte (Projects, Areas, Resources, Archives) + Inbox + Templates.

---

## 📋 Templates Disponíveis

| Template | Uso | Frontmatter |
|----------|-----|-------------|
| `Templates/Daily Note.md` | Journal diário, foco, inbox, reflexão | `tags: [daily, journal]`, `date`, `week`, `month` |
| `Templates/Project Note.md` | Projetos com escopo, entregáveis, tasks, ADRs | `tags: [project, active]`, `status`, `priority`, `start_date` |
| `Templates/Meeting Note.md` | Reuniões com agenda, decisões, action items | `tags: [meeting, type]`, `date`, `time`, `duration`, `attendees` |
| `Templates/Research Note.md` | Investigação estruturada com fontes, findings, síntese | `tags: [research, topic]`, `status`, `source_count`, `confidence` |

### Como usar no Obsidian
1. Instale o plugin **Templater** (não o core Templates)
2. Configure pasta de templates: `Templates/`
3. Use `Ctrl+T` (ou atalho configurado) para inserir template

---

## 🤖 Integração com Hermes Agent

### Configuração Ativa
- ✅ **Google Workspace OAuth** — Gmail, Calendar, Drive, Sheets, Docs, Contacts
- ✅ **Obsidian Vault** — `OBSIDIAN_VAULT_PATH=G:\Meu Drive\DO NOT DELETE\HermesAgent`
- 🔲 GitHub — configure com `gh auth login` se necessário

### Operações do Hermes no Vault
```python
# Ler nota
read_file(r"G:\Meu Drive\DO NOT DELETE\HermesAgent\10_Projects\meu-projeto\notes.md")

# Buscar no vault
search_files("termo", target="content", 
             path=r"G:\Meu Drive\DO NOT DELETE\HermesAgent", 
             file_glob="*.md")

# Criar nota
write_file(r"G:\Meu Drive\DO NOT DELETE\HermesAgent\00_Inbox\nova-ideia.md", 
           "# Nova Ideia\n...")

# Editar nota
patch(r"G:\Meu Drive\DO NOT DELETE\HermesAgent\...", "texto antigo", "texto novo")
```

### Via Google Drive API (programático)
```bash
# Buscar arquivos
python google_api.py drive search "termo" --max 10

# Upload
python google_api.py drive upload /local/file.pdf --parent FOLDER_ID

# Criar pasta
python google_api.py drive create-folder "Novo Projeto" --parent 1H4Ruo5tCllUXOVhXUWZNvtnXYYOX_Gwf
```

---

## 🔐 O que NÃO está neste repo (ficam só no Drive)

| Pasta/Arquivo | Motivo |
|---------------|--------|
| `.obsidian/` | Config local da máquina (plugins, tema, workspace) |
| `Hermes_Agent_Memory/` | Memória privada do agente (perfil, decisões, skills) |
| `00_Inbox/` | Captura bruta antes de triagem |
| `Attachments/*` | Arquivos grandes (PDFs, imagens, vídeos) |
| `*.tmp`, `*.temp/` | Arquivos temporários |

> **Regra:** O GitHub versiona **estrutura + templates + docs compartilháveis**. O Drive sincroniza **tudo** (incluindo privado).

---

## 🚀 Como Começar

### Pré-requisitos
- [Google Drive for Desktop](https://www.google.com/drive/download/) instalado e logado
- [Obsidian](https://obsidian.md/download) instalado
- [Hermes Agent](https://github.com/NousResearch/hermes-agent) configurado

### 1. Clone este repo (opcional, para contribuições)
```bash
git clone https://github.com/walterfavaronjr/HermesAgent_Obsidian.git
```

### 2. Abra no Obsidian
1. Obsidian → **Open folder as vault**
2. Selecione a pasta sincronizada localmente:  
   `G:\Meu Drive\DO NOT DELETE\HermesAgent` (ou seu caminho equivalente)

### 3. Configure Hermes Agent
```bash
# Já configurado se seguiu o setup:
hermes config set env.OBSIDIAN_VAULT_PATH "G:\Meu Drive\DO NOT DELETE\HermesAgent"
```

### 4. Instale plugins recomendados no Obsidian
| Plugin | Para que serve |
|--------|----------------|
| **Templater** | Usar templates da pasta `Templates/` |
| **Dataview** | Queries dinâmicas sobre projects, tasks, metadata |
| **Excalidraw** | Diagramas hand-drawn (compatível com skill `excalidraw`) |
| **Kanban** | Boards visuais para projects |
| **Git** | Versionamento extra (opcional) |

---

## 🔄 Workflow Diário

### Manhã
1. Abra Obsidian → `00_Inbox/` → capture ideias, tarefas, links
2. Crie *Daily Note* via template (`Templates/Daily Note.md`)
3. Defina 3 prioridades do dia

### Durante o dia
- Novas reuniões → `Templates/Meeting Note.md` em `10_Projects/` ou `20_Areas/`
- Pesquisa → `Templates/Research Note.md` em `30_Resources/`
- Novos projetos → `Templates/Project Note.md` em `10_Projects/` + registre em `Hermes_Agent_Memory/project-registry.md`

### Fim do dia / Semana
1. Triagem `00_Inbox/` → mova para `10_Projects/`, `20_Areas/`, `30_Resources/` ou `40_Archive/`
2. Atualize `project-registry.md` com status dos projetos
3. Registre decisões técnicas em `decisions-log.md` (formato ADR leve)
4. Reflexão na *Daily Note*

---

## 📝 Decisões Arquiteturais (ADRs)

Registradas em `Hermes_Agent_Memory/decisions-log.md`:

| ADR | Título | Status |
|-----|--------|--------|
| 001 | Google Drive como Single Source of Truth | ✅ Aceito |
| 002 | Estrutura PARA + Inbox + Templates | ✅ Aceito |
| 003 | OAuth Desktop App para Google Workspace | ✅ Aceito |
| 004 | Hermes Memory em pasta dedicada | ✅ Aceito |
| 005 | Templates como .md no Drive (não plugin) | ✅ Aceito |

> Formato: `## ADR-XXX: Título` + Data + Status + Contexto + Decisão + Consequências + Alternativas

---

## 🛠️ Scripts Úteis

### Verificar sync status
```bash
# No Hermes
python -c "
from google_api import drive
files = drive.search('trashed=false', raw_query=True, max=5)
print(f'Arquivos no Drive: {len(files)}')
"
```

### Backup manual para GitHub
```bash
cd /path/to/local/repo
git add -A
git commit -m "chore: sync vault structure $(date +%Y-%m-%d)"
git push
```

---

## 📚 Referências

- [Hermes Agent Docs](https://hermes-agent.nousresearch.com/docs)
- [Método PARA (Tiago Forte)](https://fortelabs.com/blog/para/)
- [Obsidian Templater Plugin](https://silentvoid13.github.io/Templater/)
- [Google Drive API](https://developers.google.com/drive/api)
- [Google Workspace Skill](https://github.com/NousResearch/hermes-agent/tree/main/skills/productivity/google-workspace)

---

## 🤝 Contribuindo

1. Fork o repo
2. Crie branch: `git checkout -b feature/nova-estrutura`
3. Commit: `git commit -m "feat: adiciona X"`
4. Push: `git push origin feature/nova-estrutura`
5. Abra Pull Request

---

## 📄 Licença

MIT — Livre para uso, modificação e distribuição.

---

## 🔗 Links Rápidos

- **Vault no Drive:** https://drive.google.com/drive/folders/1H4Ruo5tCllUXOVhXUWZNvtnXYYOX_Gwf
- **Hermes Agent:** https://github.com/NousResearch/hermes-agent
- **Issues deste repo:** https://github.com/walterfavaronjr/HermesAgent_Obsidian/issues

---

*Última atualização: 2026-06-26 — Mantido pelo Hermes Agent + Usuário*