---
title: "GFF3 文件详解：以 Argiope bruennichi 基因组注释为例"
summary: "理解GFF文件的格式内容对比较基因组学研究是很重要的。本文基于 qiwen3 详细解释了 GFF3 格式的内容和结构。"
categories: ["Post","Blog",]
tags: ["生物学","基因组","GFF"]
#externalUrl: ""
#showSummary: true
date: 2025-10-30
draft: false
---
# GFF3 文件详解：以 Argiope bruennichi 基因组注释为例

## 基本信息
- **文件来源**：NCBI RefSeq 注释文件（Assembly: GCF_947563725.1）
- **物种**：Argiope bruennichi（十字园蛛）
- **Taxonomy ID**：[94029](https://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi?id=94029)

---

    ##gff-version 3
    #!gff-spec-version 1.21
    #!processor NCBI annotwriter
    #!genome-build qqArgBrue1.1
    #!genome-build-accession NCBI_Assembly:GCF_947563725.1
    #!annotation-date 05/10/2023
    #!annotation-source NCBI RefSeq GCF_947563725.1-RS_2023_05
    ##sequence-region NC_079151.1 1 151336912
    ##species https://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi?id=94029
    NC_079151.1	RefSeq	region	1	151336912	.	+	.	ID=NC_079151.1:1..151336912;Dbxref=taxon:94029;Name=1;chromosome=1;gbkey=Src;genome=chromosome;mol_type=genomic DNA
    NC_079151.1	Gnomon	gene	475717	485371	.	-	.	ID=gene-LOC129970836;Dbxref=GeneID:129970836;Name=LOC129970836;description=sterol O-acyltransferase 1-like;gbkey=Gene;gene=LOC129970836;gene_biotype=protein_coding
    NC_079151.1	Gnomon	mRNA	475717	485371	.	-	.	ID=rna-XM_056084492.1;Parent=gene-LOC129970836;Dbxref=GeneID:129970836,GenBank:XM_056084492.1;Name=XM_056084492.1;gbkey=mRNA;gene=LOC129970836;product=sterol O-acyltransferase 1-like;transcript_id=XM_056084492.1
    NC_079151.1	Gnomon	exon	484890	485371	.	-	.	ID=exon-XM_056084492.1-1;Parent=rna-XM_056084492.1;Dbxref=GeneID:129970836,GenBank:XM_056084492.1;gbkey=mRNA;gene=LOC129970836;product=sterol O-acyltransferase 1-like;transcript_id=XM_056084492.1


## 一、什么是 GFF3？

GFF3（General Feature Format version 3）是一种标准的文本格式，用于描述基因组上的功能特征（如基因、mRNA、外显子等）。它被广泛应用于基因组注释、生物信息学分析和可视化工具中。

### GFF3 的 9 个字段

| 列 | 字段名 | 说明 |
|---|---|---|
| 1 | seqid | 参考序列 ID（如染色体、scaffold） |
| 2 | source | 注释来源或预测方法（如 RefSeq, Gnomon） |
| 3 | type | 特征类型（gene, mRNA, exon, CDS 等） |
| 4 | start | 起始位置（1-based 坐标） |
| 5 | end | 结束位置 |
| 6 | score | 分数（可为空，用 . 表示） |
| 7 | strand | 链方向：+ 正链，- 负链，. 未知 |
| 8 | phase | 阅读框（仅对 CDS 有效）：0,1,2 或 . |
| 9 | attributes | 分号分隔的键值对，包含 ID、Parent 等元数据 |

## 二、文件头信息解析


    ##gff-version 3
    #!gff-spec-version 1.21
    #!processor NCBI annotwriter
    #!genome-build qqArgBrue1.1
    #!genome-build-accession NCBI_Assembly:GCF_947563725.1
    #!annotation-date 05/10/2023
    #!annotation-source NCBI RefSeq GCF_947563725.1-RS_2023_05
    ##sequence-region NC_079151.1 1 151336912
    ##species https://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi?id=94029


### 文件头说明

| 行 | 含义 |
|---|---|
| `##gff-version 3` | 使用 GFF3 格式 |
| `#!gff-spec-version 1.21` | 遵循 GMOD GFF3 规范 1.21 版本 |
| `#!processor NCBI annotwriter` | 由 NCBI 的 annotwriter 程序生成 |
| `#!genome-build qqArgBrue1.1` | 基因组组装名称 |
| `#!genome-build-accession` | 组装编号：[GCF_947563725.1](https://www.ncbi.nlm.nih.gov/assembly/GCF_947563725.1/) |
| `#!annotation-date` | 注释日期：2023年5月10日 |
| `#!annotation-source` | 来自 NCBI RefSeq 数据库 |
| `##sequence-region` | 定义序列 NC_079151.1 的范围为 1–151,336,912 bp |
| `##species` | 物种 Taxonomy ID 为 94029 |


## 三、数据行解析

### 1. 染色体区域定义

**原始数据**：

    NC_079151.1 RefSeq region 1 151336912 . + . ID=NC_079151.1:1..151336912;Dbxref=taxon:94029;Name=1;chromosome=1;gbkey=Src;genome=chromosome;mol_type=genomic DNA


**解析**：
- **seqid**: NC_079151.1 → 第 1 号染色体
- **source**: RefSeq → 来自 RefSeq 数据库
- **type**: region → 表示这是一个基因组区域（整条染色体）
- **坐标**: 1 到 151,336,912 bp
- **strand**: + → 正链（线性表示）

**属性说明**：
- `Name=1`：染色体编号为 1
- `chromosome=1`：明确是第 1 号染色体
- `mol_type=genomic DNA`：分子类型
- `Dbxref=taxon:94029`：物种分类引用

> 💡 此行为元数据，不参与基因结构构建。

### 2. 基因（gene）特征

**原始数据**：

    NC_079151.1 Gnomon gene 475717 485371 . - . ID=gene-LOC129970836;Dbxref=GeneID:129970836;Name=LOC129970836;description=sterol O-acyltransferase 1-like;gbkey=Gene;gene=LOC129970836;gene_biotype=protein_coding


**解析**：
- **type**: gene → 编码基因
- **坐标**: 475,717 – 485,371
- **strand**: - → 位于负链（反义链）

**属性说明**：
- `ID=gene-LOC129970836`：该基因的唯一标识符
- `Name=LOC129970836`：临时基因名（"LOC" 表示 "like a gene"）
- `description=...`：功能描述为"类似甾醇O-酰基转移酶1"
- `gene_biotype=protein_coding`：蛋白编码基因
- `Dbxref=GeneID:129970836`：可在 [NCBI Gene](https://www.ncbi.nlm.nih.gov/gene/129970836) 查询详情

> 🔍 该基因可能参与脂质代谢相关通路。

### 3. mRNA 转录本

**原始数据**：

    NC_079151.1 Gnomon mRNA 475717 485371 . - . ID=rna-XM_056084492.1;Parent=gene-LOC129970836;Dbxref=GeneID:129970836,GenBank:XM_056084492.1;Name=XM_056084492.1;gbkey=mRNA;gene=LOC129970836;product=sterol O-acyltransferase 1-like;transcript_id=XM_056084492.1

**解析**：
- **type**: mRNA → 成熟信使RNA
- **坐标**: 与 gene 相同 → 表示这是主转录本的跨度
- **Parent**: gene-LOC129970836 → 隶属于上述基因

**属性说明**：
- `ID=rna-XM_056084492.1`：mRNA 唯一 ID
- `transcript_id=XM_056084492.1`：GenBank 转录本编号
- `product=...`：翻译产物名称
- `Dbxref=GenBank:XM_...`：可在 GenBank 查看序列

> 🧫 该转录本由 Gnomon（NCBI 的基因预测程序）预测。

### 4. 外显子（exon）

**原始数据**：

    NC_079151.1 Gnomon exon 484890 485371 . - . ID=exon-XM_056084492.1-1;Parent=rna-XM_056084492.1;Dbxref=GeneID:129970836,GenBank:XM_056084492.1;gbkey=mRNA;gene=LOC129970836;product=sterol O-acyltransferase 1-like;transcript_id=XM_056084492.1


**解析**：
- **type**: exon → 外显子（剪接后保留在 mRNA 中的部分）
- **坐标**: 484,890 – 485,371 → 位于基因的 3' 端
- **Parent**: rna-XM_056084492.1 → 属于该 mRNA

> 🔗 多个 exon 行共同构成一个 mRNA 的结构。

## 四、GFF3 的层级结构

GFF3 使用 ID 和 Parent 字段建立树状结构：

    gene (ID=gene-LOC129970836) 
    └── mRNA (ID=rna-XM_056084492.1, Parent=gene-...) 
        ├── exon (ID=exon-..., Parent=rna-...) 
        ├── CDS (...) 
        └── five_prime_UTR / three_prime_UTR (...)


**层级规则**：
- 所有子特征必须通过 Parent= 指向其父特征
- ID 必须在整个文件中唯一
- mRNA 是连接 gene 和 exon/CDS 的桥梁

## 五、常见 feature 类型说明

| 类型 | 含义 | 备注 |
|---|---|---|
| gene | 基因区域 | 包含所有转录本 |
| mRNA | 转录本 | 可有多个剪接异构体 |
| exon | 外显子 | 构成成熟 mRNA |
| CDS | 编码序列 | 从起始密码子到终止密码子 |
| five_prime_UTR | 5' 非翻译区 | 翻译调控区 |
| three_prime_UTR | 3' 非翻译区 | 影响 mRNA 稳定性 |
| intron | 内含子 | 通常不显式列出 |
| start_codon, stop_codon | 起始/终止密码子 | 精确定位翻译边界 |

> ⚠️ 并非所有 GFF3 文件都包含 UTR 或 CDS，取决于注释完整性。

## 六、如何查看完整基因结构？

### 方法 1：使用基因组浏览器
- [IGV](https://software.broadinstitute.org/software/igv/)
- [JBrowse](https://jbrowse.org/)
- [UCSC Genome Browser](https://genome.ucsc.edu/)

导入 GFF3 和 FASTA 文件即可可视化。
