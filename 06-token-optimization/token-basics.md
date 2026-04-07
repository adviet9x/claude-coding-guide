# Hiểu Về Token

> Token là đơn vị "tính tiền" khi dùng Claude. Hiểu token = tiết kiệm chi phí.

---

## 1. Token Là Gì?

Token ≈ mảnh nhỏ của text. Không phải 1 từ = 1 token.

```
"Hello world"          → 2 tokens
"Hello, world!"        → 4 tokens  
"getUserById"          → 3 tokens
"get_user_by_id"       → 7 tokens
"const x = 42;"        → 5 tokens
"Xin chào thế giới"    → 8 tokens (tiếng Việt tốn hơn)
```

### Quy tắc ước lượng
| Loại text | Tokens / từ | Tokens / dòng |
|-----------|------------|---------------|
| Tiếng Anh | ~1.3 | ~10-15 |
| Tiếng Việt | ~2.5 | ~20-30 |
| Code (Python/JS) | ~1.5 | ~12-18 |
| JSON/YAML | ~1.5 | ~10-15 |
| Markdown | ~1.2 | ~8-12 |

---

## 2. Token Budget Trong 1 Session

```
Context Window: ~200K tokens (Claude 3.5+)

Chi phí mỗi phần:
┌─────────────────────────────────────┐
│ System Prompt        ~5K tokens     │ ← Cố định
│ CLAUDE.md + Rules    ~3-10K tokens  │ ← Tùy project
│ Memory (auto-load)   ~1-3K tokens   │ ← Tùy memory size
│                                     │
│ Input (your prompts) ~2-5K tokens   │ ← Mỗi message
│ Output (Claude)      ~3-10K tokens  │ ← Mỗi response
│ File reads           ~5-20K tokens  │ ← Code Claude đọc
│ Tool calls           ~2-5K tokens   │ ← Search, terminal
│                                     │
│ → Conversation ~50-100K tokens      │
│ → Remaining: 100-150K tokens        │
└─────────────────────────────────────┘
```

---

## 3. Chi Phí Token

### Pricing (tham khảo)
| Model | Input | Output |
|-------|-------|--------|
| Claude Sonnet | $3/M tokens | $15/M tokens |
| Claude Opus | $15/M tokens | $75/M tokens |
| GPT-4o | $5/M tokens | $15/M tokens |

> M = million tokens

### Ước tính chi phí 1 session
```
Session trung bình (15 messages):
- Input: ~20K tokens × $3/M = $0.06
- Output: ~30K tokens × $15/M = $0.45
- Total: ~$0.50 per session

Session dài (50 messages):
- Total: ~$2-5 per session
```

---

## 4. Cách Đếm Token

### Ước lượng nhanh
```
1 file ngắn (50 dòng)    ≈ 750 tokens
1 file trung bình (200 dòng) ≈ 3K tokens
1 file dài (500 dòng)     ≈ 7.5K tokens
1 file rất dài (1000 dòng) ≈ 15K tokens

1 message ngắn            ≈ 50 tokens
1 message trung bình      ≈ 200 tokens
1 message dài              ≈ 500+ tokens
```

### Công cụ đếm chính xác
- [Anthropic Tokenizer](https://docs.anthropic.com/en/docs/build-with-claude/token-counting)
- [OpenAI Tokenizer](https://platform.openai.com/tokenizer) (tương đồng)
- `tiktoken` library (Python)

---

## 5. Tại Sao Token Quan Trọng?

1. **Chi phí** — Càng nhiều token = càng tốn tiền
2. **Context limit** — Hết context = Claude quên
3. **Speed** — Ít token = response nhanh hơn
4. **Accuracy** — Context tập trung = output chính xác hơn

> Tiết kiệm token không chỉ tiết kiệm tiền mà còn giúp Claude làm tốt hơn.
