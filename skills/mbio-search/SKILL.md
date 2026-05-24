---
name: bio-search
description: >-
  微生物学与生命科学文献的多源搜索、引文验证、MeSH检索策略、引文文件管理
  (.nbib/.ris/.bib转换)和参考文献管理。通过MCP工具(PubMed, CrossRef, bioRxiv)
  进行协调的多步骤文献工作流。当用户需要超越单一MCP调用的复杂文献检索时使用。
---

# Bio-Search

微生物学与生命科学文献的多源搜索、引文验证和参考文献管理。

## MCP Tools

### Core Search

| Tool | Source | Best For |
|------|--------|----------|
| `pubmed_search_articles` | PubMed MCP | 微生物学、MeSH、病原菌、耐药性 |
| `search_crossref` | paper-search MCP | 跨学科、交叉领域、引用计数 |
| `search_biorxiv` | paper-search MCP | 生物学预印本(微生物组、基因组) |

### Extended Search

| Tool | Source | Best For |
|------|--------|----------|
| `search_google_scholar` | paper-search MCP | 广泛的学术搜索 |
| `search_semantic_scholar` | paper-search MCP | 引用图、影响力评估 |
| `search_medrxiv` | paper-search MCP | 临床微生物学预印本 |

### PubMed Utilities

| Tool | Purpose |
|------|---------|
| `pubmed_fetch_articles` | 通过PMID获取完整元数据 |
| `pubmed_find_related` | 相关文章发现 |
| `pubmed_format_citations` | APA/MLA/BibTeX/RIS格式 |
| `pubmed_convert_ids` | DOI ↔ PMID ↔ PMCID转换 |
| `pubmed_lookup_mesh` | MeSH术语探索和层级 |
| `pubmed_lookup_citation` | 文献信息→PMID查找 |

## Source Routing

See [Source Tiers & Reliability](references/source-tiers.md) for complete classification.

Quick guide:

| User need | Primary (T1) | Secondary (T2) | Last Resort (T3) |
|-----------|-------------|-----------------|-------------------|
| 微生物学/病原菌 | PubMed | Semantic Scholar | Google Scholar |
| 预印本/微生物组 | bioRxiv | medRxiv | — |
| 跨学科/生信 | CrossRef | Semantic Scholar | — |
| 抗生素耐药 | PubMed | Semantic Scholar | Google Scholar |
| 病毒学 | PubMed + bioRxiv | medRxiv | — |
| 中文文献 | — | — | CNKI (手动) |

## Workflows

| # | Workflow | Reference |
|---|----------|-----------|
| 1 | Multi-Source Literature Search | [wf1](references/workflows/wf1-multi-source-search.md) |
| 2 | Citation Verification | [wf2](references/workflows/wf2-citation-verification.md) |
| 3 | MeSH Search Strategy | [wf3](references/workflows/wf3-mesh-strategy.md) |
| 4 | Citation File Management | [wf4](references/workflows/wf4-citation-file-mgmt.md) |
| 5 | Reference Management | [wf5](references/workflows/wf5-reference-mgmt.md) |

## Shared Modules

| Module | Purpose |
|--------|---------|
| [Dedup Engine](references/dedup-engine.md) | 多源结果去重 (WFs 1, 2) |
| [Citation Parser](references/citation-parser.md) | 从文档提取引文 (WF 2) |
| [Search Strategy](references/search-strategy.md) | 查询构建、源选择、排序 |
| [RIS/BibTeX Format](references/ris-bibtex-format.md) | 格式规范和字段映射 |

## Environment Setup

### API Keys (optional but recommended)

| Service | Env Var | Register At | Free Tier |
|---------|---------|-------------|-----------|
| Semantic Scholar | `SEMANTIC_SCHOLAR_API_KEY` | [api.semanticscholar.org](https://api.semanticscholar.org/) | 100 req/s with key (1/s without) |
| NCBI E-utilities | `NCBI_API_KEY` | [ncbi.nlm.nih.gov/account](https://www.ncbi.nlm.nih.gov/account/) | 10 req/s with key (3/s without) |

Set via `export` or `.env` file.

### Proxy (if behind firewall)

```bash
export http_proxy=http://127.0.0.1:7890
export https_proxy=http://127.0.0.1:7890
