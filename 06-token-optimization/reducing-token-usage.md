# Giảm Tiêu Thụ Token

> Các kỹ thuật thực tế để giảm token usage mà không giảm chất lượng output.

---

## 1. Tối Ưu Input (Prompts)

### Prompt ngắn, chính xác
```
# ❌ ~150 tokens
"Tôi muốn nhờ bạn giúp tôi tạo một endpoint API 
mới để cho phép người dùng có thể lấy danh sách 
tất cả users trong hệ thống, có hỗ trợ phân trang
với 2 query parameters là page và limit..."

# ✅ ~30 tokens
"Tạo GET /api/users — phân trang (?page, ?limit).
Theo api-conventions.md."
```
**Tiết kiệm: ~120 tokens/prompt × 15 messages = 1,800 tokens/session**

### Reference rules thay vì giải thích
```
# ❌ Giải thích convention mỗi lần
"Dùng camelCase cho biến, PascalCase cho class,
UPPER_SNAKE cho constants, kebab-case cho files..."

# ✅ Reference rule file
"Follow code-style.md"
```

### Dùng abbreviations khi rõ nghĩa
```
# ❌ Dài
"Tạo unit tests cho file agents/agent_pipeline.py"

# ✅ Ngắn (Claude hiểu)
"Tests cho agents/agent_pipeline.py"
```

---

## 2. Tối Ưu Output

### Yêu cầu format ngắn
```
"Code only, không giải thích"
"Tóm tắt 3 dòng"
"Trả lời ngắn gọn"
"Chỉ liệt kê file names"
```

### Giới hạn scope
```
# ❌ Output dài
"Review toàn bộ codebase"  → Claude trả 2000+ tokens

# ✅ Output vừa
"Review file X — chỉ security issues"  → Claude trả 300 tokens
```

---

## 3. Tối Ưu File Reads

### FILE_MAP thay cho scan
```
# ❌ Claude scan 50 files (50 × list_dir + read_file)
"Tìm file xử lý authentication"

# ✅ Claude đọc FILE_MAP (1 read)
# (có FILE_MAP.md trong repo memory)
"Authentication code ở đâu?" → Claude tra memory → biết ngay
```
**Tiết kiệm: ~10,000+ tokens**

### Chỉ đọc file cần thiết
```
# ❌ Claude đọc 5 files để hiểu
"Sửa bug trong pipeline"

# ✅ Chỉ ra file cụ thể
"agents/agent_pipeline.py dòng 230: fix KeyError"
```

### Đọc range thay vì cả file
```
# ❌ Claude đọc toàn bộ file 1000 dòng
"Đọc agent_pipeline.py"

# ✅ Chỉ đọc phần cần
"Đọc agent_pipeline.py dòng 200-250"
```

---

## 4. Tối Ưu Conversation

### Session ngắn, tập trung
```
# ❌ 1 session 50 messages (context overflow)
Session 1: Refactor + Test + Deploy + Debug = 50 messages

# ✅ Nhiều sessions ngắn
Session 1: Refactor (10 messages) → save memory
Session 2: Test (8 messages) → save memory
Session 3: Deploy (5 messages)
```
**Tiết kiệm: ~30-50% tokens total**

### Không hỏi lại thứ đã biết
```
# ❌ Hỏi lại
Message 1: "Giải thích kiến trúc dự án"
Message 5: "Nhắc lại kiến trúc dự án"  ← tốn token lặp

# ✅ Lưu vào memory
Message 1: "Giải thích kiến trúc, lưu vào repo memory"
Message 5: "Đọc repo memory/architecture" ← ít token hơn
```

---

## 5. Tối Ưu CLAUDE.md & Rules

### CLAUDE.md tối ưu
```
# ❌ 500 dòng = ~4,000 tokens MỖI MESSAGE
→ 15 messages × 4,000 = 60,000 tokens bị lãng phí

# ✅ 150 dòng = ~1,200 tokens MỖI MESSAGE
→ 15 messages × 1,200 = 18,000 tokens
→ Tiết kiệm: 42,000 tokens/session
```

### Rules tối ưu
```
# ❌ 10 rule files × 200 dòng = 2,000 dòng = ~16K tokens
→ Loaded MỖI MESSAGE

# ✅ 10 rule files × 50 dòng = 500 dòng = ~4K tokens
→ Tiết kiệm: ~12K tokens × 15 messages = 180K tokens/session
```

---

## 6. Bảng Tóm Tắt

| Kỹ thuật | Tiết kiệm ước tính |
|----------|-------------------|
| Prompt ngắn | ~2K tokens/session |
| FILE_MAP thay cho scan | ~10K tokens/session |
| Output format ngắn | ~5K tokens/session |
| Sessions ngắn | ~30% total |
| CLAUDE.md tối ưu | ~40K tokens/session |
| Rules tối ưu | ~100K+ tokens/session |
| Memory thay cho repeat | ~5K tokens/session |

> **Tổng tiết kiệm tiềm năng: 50-70% token usage**
