# Hybrid RAG：BM25 + 向量检索 + RRF融合 + 重排
基于混合检索的检索增强生成（RAG）项目，面向知识库问答，解决单一检索方式召回不足的问题。

## 系统架构
```mermaid
flowchart LR
    A[用户Query] --> B[双路检索]
    B --> B1[BM25稀疏检索]
    B --> B2[向量稠密检索]
    B1 & B2 --> C[RRF融合<br/>rrf_k=60]
    C --> D[重排模块<br/>bge-reranker-base]
    D --> E[筛选TopN相关文档]
    E --> F[Prompt组装]
    F --> G[LLM生成回答]
    G --> H[输出答案+引用来源]
