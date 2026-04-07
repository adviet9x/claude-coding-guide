# FAQ — Câu Hỏi Thường Gặp

---

## Tổng Quan

### Claude là gì? Khác gì ChatGPT?
Claude là AI model của Anthropic. Trong VS Code, Claude chạy qua GitHub Copilot.
Khác ChatGPT: Claude mạnh hơn ở code reasoning, follow instructions, và xử lý context dài.

### Claude có thể làm gì trong VS Code?
- Đọc, tạo, sửa file
- Chạy terminal commands
- Search code
- Chạy tests
- Phân tích và debug code
- Tương tác với Git

### Claude có thể access internet không?
Không trực tiếp. Claude có tool `fetch_webpage` để đọc URL cụ thể, nhưng không "browse" internet tự do.

---

## Setup

### Cần trả tiền không?
- **VS Code Copilot**: Cần GitHub Copilot subscription ($10-19/month)
- **Claude Code CLI**: Cần Anthropic API key (pay-per-use)
- **Claude.ai web**: Free tier có giới hạn, Pro $20/month

### Dự án nào cũng dùng Claude được không?
Có. Claude làm việc với mọi ngôn ngữ: Python, JavaScript, TypeScript, Java, Go, Rust, C#, PHP, Ruby, và nhiều ngữ khác.

### Team nhiều người dùng chung rules được không?
Có. Commit `.claude/rules/`, `.claude/skills/`, `.claude/agents/` vào Git.
Mỗi team member sẽ có cùng rules.
File cá nhân (`.claude/settings.local.json`, `CLAUDE.local.md`) thì gitignore.

---

## Sử Dụng

### Nên dùng tiếng Việt hay tiếng Anh?
- **Giao tiếp**: Tiếng Việt OK, Claude hiểu tốt
- **Rules, CLAUDE.md**: Tiếng Anh khuyên dùng (chuẩn hơn)
- **Code**: Luôn tiếng Anh (biến, comments, docs)
- **Thuật ngữ kỹ thuật**: Giữ nguyên tiếng Anh

### Bao nhiêu messages thì nên bắt đầu session mới?
- **< 15 messages**: Bình thường
- **15-30 messages**: Cân nhắc lưu memory
- **> 30 messages**: Nên bắt đầu session mới

### Claude có nhớ session trước không?
Không tự động. Phải dùng memory system:
- Session memory: trong 1 conversation
- Repo memory: xuyên sessions, 1 dự án
- User memory: xuyên sessions, mọi dự án

### Claude sửa sai thì rollback thế nào?
- **VS Code**: Ctrl+Z (undo) trong file
- **Git**: `git checkout -- [file]` hoặc `git stash`
- **Terminal**: Claude thường không làm gì destructive

---

## Tối Ưu

### Cách nào tiết kiệm token nhất?
1. CLAUDE.md ngắn gọn (< 200 dòng)
2. Rules ngắn gọn (mỗi file < 100 dòng)
3. Prompt ngắn, chính xác
4. FILE_MAP.md thay cho scan dự án
5. Sessions ngắn (10-15 messages)
6. "Code only" khi chỉ cần code

### Claude có thể tự chạy test không?
Có. Claude có tool `run_in_terminal` để chạy bất kỳ command nào:
```
"Chạy pytest tests/ -v"
"Chạy npm test"
```

### Claude có thể commit/push code không?
Có thể nhưng **không nên** cho auto. Claude sẽ hỏi confirm trước khi:
- `git push`
- `git reset --hard`
- Delete files
- Modify production config

---

## Troubleshooting

### Claude chạy chậm / timeout?
- File quá lớn → đọc range cụ thể
- Command chạy lâu → set timeout
- Context quá nhiều → session mới

### Claude tạo code lỗi syntax?
- Yêu cầu: "Chạy linter sau khi tạo"
- Có rules code-style → giảm lỗi syntax
- Review output trước khi accept

### Claude không access được file?
- Kiểm tra file path (absolute vs relative)
- File binary không đọc được (images, PDFs)
- File trong .gitignore → cần flag `includeIgnoredFiles`
- File quá lớn (>10MB) → chia nhỏ hoặc đọc range

### Tại sao Claude trả lời khác nhau mỗi lần?
Temperature > 0 = có randomness. Để kết quả nhất quán:
- Set temperature = 0 trong settings
- Prompt càng cụ thể → output càng giống nhau
- Cùng context → output tương tự

---

## Best Practices Summary

| Nguyên tắc | Chi tiết |
|-----------|---------|
| Đầu tư vào setup | CLAUDE.md + rules + FILE_MAP → ROI cao |
| Prompt ngắn gọn | Chính xác > dài dòng |
| Review mọi thứ | Tin nhưng verify |
| Test thường xuyên | Sau mỗi thay đổi |
| Lưu memory | Insights quan trọng |
| Sessions ngắn | 10-15 messages tối ưu |
| Cập nhật docs | Sau mỗi thay đổi lớn |
