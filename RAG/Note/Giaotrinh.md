# 📘 RAG Learning Roadmap — From Zero to Production

## 🎯 Tổng quan lộ trình (8–10 tuần)

Lộ trình này được thiết kế dành cho developer muốn:
- Hiểu sâu về RAG (Retrieval-Augmented Generation)
- Xây dựng hệ thống thực tế
- Tối ưu và triển khai production

### Các giai đoạn:

| Phase | Nội dung | Mục tiêu |
|------|--------|---------|
| Phase 0 | Foundation | Hiểu LLM + Embedding |
| Phase 1 | Core RAG | Xây pipeline cơ bản |
| Phase 2 | Advanced RAG | Tối ưu retrieval |
| Phase 3 | Production RAG | Deploy thực tế |
| Phase 4 | Research RAG | Hiểu sâu & mở rộng |

---

# 🧠 PHASE 0 — FOUNDATION (Tuần 1–2)

## 🎯 Mục tiêu
Hiểu:
- LLM hoạt động như thế nào
- Vì sao RAG tồn tại
- Embedding là nền tảng của retrieval

---

## 0.1 LLM hoạt động như thế nào

### Transformer cơ bản
- Token → Embedding → Attention → Output
- Attention giúp model hiểu ngữ cảnh

### Prompt → Completion
- Input: Prompt
- Output: Text generation
- Không có kiến thức thật → chỉ dự đoán token tiếp theo

### Hallucination
- LLM có thể "bịa" thông tin
- Không có khả năng truy xuất dữ liệu ngoài
- Đây chính là lý do RAG ra đời

---

## 0.2 Embedding là gì

### Vector space
- Text → vector (dạng số)
- Các vector gần nhau → nghĩa gần nhau

### Semantic similarity
- So sánh ý nghĩa thay vì từ vựng

### Cosine similarity

Công thức:

cos(a, b) = (a · b) / (||a|| ||b||)

- Giá trị gần 1 → giống nhau
- Giá trị gần 0 → khác nhau

---

## 0.3 Các thành phần cơ bản

### Tokenization
- Chia text thành token

### Context window
- Giới hạn số token model xử lý

### Chunking
- Chia tài liệu thành đoạn nhỏ
- Ảnh hưởng trực tiếp đến chất lượng RAG

---

## 📌 Bài tập

1. Encode văn bản bằng `sentence-transformers`
2. Tính similarity giữa các câu:
   - "Tôi thích AI"
   - "Tôi yêu machine learning"
   - "Hôm nay trời đẹp"

---

# 🔎 PHASE 1 — CORE RAG (Tuần 3–4)

## 🎯 Mục tiêu
Xây dựng pipeline RAG đơn giản

---

## 1.1 Kiến trúc RAG cơ bản

Pipeline:

User Query  
→ Embedding  
→ Retrieve documents  
→ Inject vào prompt  
→ LLM generate answer  

---

## 1.2 Vector Database

### FAISS (bắt buộc)
- Thư viện của Meta
- Tìm kiếm vector cực nhanh

### So sánh:

| Tool | Ưu điểm | Nhược điểm |
|------|--------|-----------|
| FAISS | Nhanh, local | Khó scale |
| Chroma | Dễ dùng | Chậm hơn |
| Pinecone | Managed | Tốn tiền |

---

## 1.3 Chunking strategies

### Fixed chunk
- Chia đều theo số token

### Sliding window
- Có overlap giữa các chunk

### Semantic chunking
- Chia theo ý nghĩa

---

## 1.4 Prompt Engineering cho RAG

### Context injection
- Đưa tài liệu vào prompt

### Instruction tuning
- Hướng dẫn model cách trả lời

### Few-shot
- Thêm ví dụ vào prompt

---

## 📌 Project 1 — RAG từ PDF

### Mục tiêu
Xây chatbot hỏi đáp từ tài liệu

### Pipeline

1. Load PDF
2. Chunk text
3. Encode embedding
4. Lưu vào FAISS
5. Query → retrieve → generate

### Tech stack
- sentence-transformers
- FAISS
- LLM (OpenAI hoặc local)

---

# ⚡ PHASE 2 — ADVANCED RAG (Tuần 5–6)

## 🎯 Mục tiêu
Cải thiện chất lượng retrieval

---

## 2.1 Retrieval nâng cao

### Sparse retrieval (BM25)
- Dựa trên keyword

### Dense retrieval
- Dựa trên embedding

### Hybrid retrieval
- Kết hợp BM25 + vector

---

## 2.2 Reranking (CỰC QUAN TRỌNG)

### Vấn đề
Retriever lấy nhiều document nhưng chưa chính xác

### Giải pháp
- Dùng Cross-Encoder để chấm điểm lại

### Các lựa chọn
- Cross-Encoder (HuggingFace)
- BGE reranker
- Cohere rerank

---

## 2.3 Query Understanding

### Query rewriting
- Viết lại câu hỏi

### Multi-query
- Tạo nhiều query

### HyDE
- Sinh document giả → embed → search

---

## 2.4 Multi-hop RAG

### Query decomposition
- Chia câu hỏi phức tạp

### Chain-of-thought retrieval
- Retrieve từng bước

---

## 📌 Project 2 — Improve RAG

Nâng cấp Project 1:

- Thêm BM25
- Thêm reranker
- So sánh:
  - Recall
  - Accuracy

---

# 🏗️ PHASE 3 — PRODUCTION RAG (Tuần 7–8)

## 🎯 Mục tiêu
Đưa hệ thống vào production

---

## 3.1 System Design

### Offline pipeline
- Data ingestion
- Cleaning
- Chunking
- Embedding
- Indexing

### Online pipeline
- Query processing
- Retrieval
- Rerank
- LLM inference

---

## 3.2 Scaling

### ANN search
- HNSW
- IVF

### Techniques
- Sharding index
- Distributed search

### Caching
- Cache query
- Cache embedding

---

## 3.3 Optimization

### Reduce latency
- Batch embedding
- Async pipeline

### Reduce cost
- Cache LLM response
- Limit context

### Context compression
- Summarization
- Token pruning

---

## 3.4 Guardrails

### Hallucination reduction
- Chỉ trả lời từ context

### Source citation
- Trích nguồn

### Safety
- Filter nội dung nguy hiểm

---

## 📌 Project 3 — Production Chatbot

### Xây hệ thống hoàn chỉnh:

- Backend: FastAPI
- Frontend: Streamlit
- Logging:
  - Query
  - Response
  - Latency

---

# 🧪 PHASE 4 — RESEARCH LEVEL (Tuần 9–10)

## 🎯 Mục tiêu
Hiểu sâu và nâng cao

---

## 4.1 Evaluation

### Metrics

- Recall@k
- MRR
- Faithfulness
- Answer correctness

---

## 4.2 Advanced Techniques

### Self-RAG
- Model tự đánh giá context

### Graph RAG
- Knowledge graph

### Agentic RAG
- RAG + Agent

---

## 4.3 Long Context vs RAG

### Long context
- Input toàn bộ document

### RAG
- Retrieve thông minh

### Trade-off
| Long Context | RAG |
|-------------|----|
| Đơn giản | Phức tạp |
| Tốn cost | Tiết kiệm |

---

## 4.4 Fine-tuning vs RAG

### Khi dùng Fine-tune
- Style cố định
- Task cố định

### Khi dùng RAG
- Dữ liệu thay đổi liên tục
- Cần cập nhật realtime

---