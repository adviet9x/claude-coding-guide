# Cài Đặt Môi Trường

> Hướng dẫn cài đặt và cấu hình môi trường để làm việc với Claude AI.

---

## 1. VS Code + GitHub Copilot (Khuyên dùng)

### Cài đặt
1. Cài [VS Code](https://code.visualstudio.com/)
2. Cài extension **GitHub Copilot** + **GitHub Copilot Chat**
3. Đăng nhập GitHub (cần subscription Copilot Pro/Business)
4. Chọn model **Claude** trong Copilot Chat settings

### Cấu hình VS Code
```json
// settings.json
{
  // Copilot sử dụng Claude
  "github.copilot.chat.languageModel": "claude-sonnet-4",

  // Cho phép Copilot đọc workspace
  "github.copilot.chat.experimental.codeGeneration.allowFiles": true,

  // Terminal integration
  "github.copilot.chat.terminalAccess": true
}
```

### Extensions bổ trợ
| Extension | Mục đích |
|-----------|----------|
| GitHub Copilot | Code completion + Chat |
| GitLens | Git blame, history |
| Error Lens | Hiển thị lỗi inline |
| Thunder Client | Test API |
| Markdown Preview | Xem preview .md files |

---

## 2. Claude Code (CLI)

### Cài đặt
```bash
# macOS / Linux
curl -fsSL https://claude.ai/install.sh | sh

# Hoặc dùng npm
npm install -g @anthropic-ai/claude-code
```

### Cấu hình
```bash
# Đăng nhập
claude login

# Kiểm tra
claude --version

# Chạy trong dự án
cd /path/to/project
claude
```

### Claude Code vs VS Code Copilot

| Tiêu chí | VS Code + Copilot | Claude Code (CLI) |
|----------|-------------------|-------------------|
| Giao diện | GUI trong IDE | Terminal |
| Context | Tự động đọc workspace | Tự động đọc workspace |
| File editing | Visual diff | Terminal diff |
| Multi-file | Tốt | Rất tốt |
| Phù hợp | Frontend, visual tasks | Backend, refactoring lớn |

---

## 3. Cấu Trúc Folder Bắt Buộc

Mọi dự án muốn làm việc tốt với Claude cần có:

```
project-root/
├── CLAUDE.md              # ← File quan trọng nhất
├── .claude/               # ← Folder cấu hình Claude
│   ├── rules/             # Quy tắc bắt buộc
│   ├── skills/            # Kỹ năng chuyên biệt
│   ├── agents/            # Sub-agent definitions
│   ├── commands/          # Lệnh tái sử dụng
│   ├── CLAUDE.md          # Instructions cho .claude scope
│   └── settings.json      # Cấu hình project-level
└── docs/                  # Tài liệu dự án
    ├── PROJECT.md         # Tổng quan dự án cho AI
    ├── FILE_MAP.md        # Bản đồ file
    └── ARCHITECTURE.md    # Kiến trúc hệ thống
```

---

## 4. Kiểm Tra Cài Đặt

### Checklist
- [ ] VS Code hoặc Claude Code đã cài
- [ ] Claude model đã chọn và hoạt động
- [ ] Dự án có `CLAUDE.md` ở root
- [ ] Folder `.claude/` đã tạo
- [ ] Ít nhất 1 rule file trong `.claude/rules/`
- [ ] Claude có thể đọc file và chạy terminal

### Test nhanh
Mở Claude Chat và hỏi:
```
Hãy liệt kê cấu trúc thư mục của dự án này
```
Nếu Claude trả lời đúng → cài đặt thành công ✅

---

## 5. IDE Alternatives

| IDE | Claude Support | Ghi chú |
|-----|---------------|---------|
| VS Code | ✅ Tốt nhất | GitHub Copilot + Claude |
| Cursor | ✅ Tích hợp sẵn | Có thể chọn Claude model |
| Windsurf | ✅ Tích hợp | Cascade agent |
| JetBrains | ⚠️ Hạn chế | Qua plugin Copilot |
| Neovim | ⚠️ Hạn chế | Qua copilot.vim |

> **Khuyến nghị**: VS Code + GitHub Copilot cho đa số trường hợp. Claude Code CLI cho refactoring lớn.
