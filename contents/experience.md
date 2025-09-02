### **Agent Development Intern**

**November 2024 – February 2025 | Beijing Zhongchuang Carbon Investment Technology Co., Ltd.**

Built a fully automated “ESG report upload → LLM metric extraction → rule-driven scoring → API callback” pipeline for the China Alcoholic Drinks Association, reducing per-report processing time from 2–3 days to < 1 minute and supporting the first-round quantitative scoring for the industry’s 2025 ESG White Paper.

#### Key Contributions:

* **LLM Metric Extraction:** Designed a few-shot prompt + JSON Schema validation workflow; called Moonshot GPT to extract and parse 102 E/S/G metrics and cleaned them into structured JSON.
* **Rule-driven Scoring Engine:** Unified extracted results with the business unit’s scoring tables, invoked GPT models to generate scores, and normalized the scoring outputs.
* **Excel ↔ JSON Bidirectional Mapping Tool:** Implemented a Mapping DSL with Pandas + openpyxl; supported versioning of scoring rules and JSON→Excel write-back to ensure consistent round-tripping.
* **FastAPI Microservice Design:** Encapsulated business logic and exposed endpoints for backend integration.
* **Cross-team Data Format Alignment:** Co-defined a data dictionary with ESG researchers (field names, enumerations, missing-value policies) and established version control.


---

### **Agent开发实习生**  
**2024年11月 – 2025年2月 | 北京中创碳投科技有限公司**  

负责为中国酒业协会构建 “ESG 报告上传 → LLM 指标抽取 → 规则化打分 → API 回传” 全自动流水线，将单份报告处理周期从 2-3 天压缩至 < 1 分钟，支撑 2025 行业 ESG 白皮书的首轮量化评分。

#### 主要贡献:  
- LLM 指标抽取：设计 Few-shot Prompt + JSON Schema 校验流程，调用 Moonshot GPT 抽取并解析 102 项 E/S/G 指标，清洗为结构化 JSON。
- 规则化打分引擎：将抽取结果与业务部门的评分表整合为统一格式，调用GPT模型进行评分，并规范化评分结果。
- Excel ↔ JSON 双向映射工具：使用 Pandas + openpyxl 编写 Mapping DSL，支持评分规则版本化 & JSON→Excel 回写，保障数据轮转一致。
- FastAPI 微服务接口设计：将业务进行封装，支持后端调用。
- 跨部门数据格式协同：与 ESG 研究员共同定义 数据字典（字段命名、枚举值、缺失值策略），并建立版本控制。

#### 流程图简介：

![Alt text](../static/assets/img/agentFlowChart.jpg)

---

### **End-to-End NLP Model Comparison & Deployment Project**

**March 2025 – June 2025 | Course Design Project**

Built an end-to-end NLP system for a flight-query scenario covering the full pipeline: “intent & slot recognition → template classification → response generation.” Leveraged PyTorch, HuggingFace Transformers, SentenceTransformers, LangChain, and FAISS to implement 7 models ranging from linear baselines to RAG-LLM, completing training, evaluation, inference, and deployment.

#### Key Contributions:

* **Joint Transformer Model (Slot Tagging + Template Classification):** Designed and implemented a unified pipeline from data preprocessing → training → inference → strict-accuracy evaluation. Built a data processing workflow (variable expansion; generation of “question → SQL template + BIO tags”; unified splits and mappings) to consistently produce best weights and error lists, improving NL→SQL stability and reproducibility.
* **T5-based NL→SQL Generation Pipeline:** Implemented mixed precision, early stopping, and learning-rate scheduling; paired raw queries with filled, standard SQL to create directly trainable samples; performed strict-match evaluation on the test set and archived the best checkpoint with visualized examples for rapid error localization and experiment reproducibility.
* **RAG Integration (SentenceTransformers + FAISS + LangChain):** Integrated retrieval-augmented generation to substantially reduce irrelevant/incorrect outputs and improve response controllability in zero-shot settings (≈15–20% improvement based on internal project evaluation).

---

### **NLP 全流程模型对比与部署项目**  
**2025年3月 – 2025年6月 | 课程设计项目**  

负责构建面向航班查询场景的端到端 NLP 系统，涵盖“意图与槽位识别 → 模板分类 → 回复生成”完整流程。项目采用 PyTorch、HuggingFace Transformers、SentenceTransformers、LangChain 与 FAISS，覆盖从线性基线到 RAG-LLM 的 7 种模型，完成训练、评测、推理及部署。

#### 主要贡献:  
- 设计并实现基于 Transformer 的联合学习模型（槽位序列标注 + 模板分类），并在领域语料上微调主干模型（BERT/RoBERTa）；打通数据预处理→训练→推理→严格准确率评测的一体化链路，稳定产出最优权重与误差清单，提升 NL→SQL 的稳定性与可复现性。

- 构建以 T5 为核心的 NL→SQL 生成流水线，在项目语料上微调 T5-base（混合精度训练、早停与 ReduceLROnPlateau 调度），于测试集进行 strict-match 准确率评测，并沉淀最优 checkpoint 与可视化样例用于快速定位错误与回归验证。

- 集成 SentenceTransformers + FAISS 与 LangChain 的检索增强生成（RAG），在零样本场景显著降低无关/错误生成比例并提升回答可控性（基于项目内部评测，约 15–20%）。

---

### **AWS Serverless Image Upload & Auto-Captioning System**

**March 2025 – June 2025 | Course Design Project**

Implemented an end-to-end serverless pipeline on AWS—“image upload → automatic thumbnail generation → caption creation → frontend display”—so each upload immediately yields display-ready content. Adopted least-privilege and layered-security design with elasticity and observability (ALB/ASG, S3, Lambda, RDS, Secrets Manager, CloudWatch).

#### Key Contributions:

* **Serverless Event Chain Delivery:** Designed an S3 → EventBridge → Lambda “upload-to-process” flow. New objects under `uploads/` trigger two branches (Annotation and Thumbnail) to auto-generate captions and 128×128 thumbnails, then write back to storage/database.
* **AI Capability & Secret Governance:** `AnnotationFunction` reads the original image and invokes Google Gemini to generate captions; `(image key, caption)` is persisted to RDS. Gemini/RDS credentials are centralized in Secrets Manager and injected at runtime to avoid plaintext and hardcoding.
* **Elasticity & High Availability Engineering:** Configured ASG desired capacity and scaling, with \~60% CPU as the threshold for scale-out/in; ALB distributes traffic across AZs; VPC public/private subnets plus NAT/Bastion secure egress and operations.
* **Performance & Elasticity Validation:** Used ApacheBench to stress `/upload` with 20 concurrent × 500 requests—100% success, \~41 ms average latency, 484 req/s throughput; CloudWatch metrics showed CPU spikes and recovery, validating ALB distribution and ASG autoscaling.

---

### **AWS Serverless 图像上传与自动描述系统**  
**2025年3月 – 2025年6月 | 课程设计项目**  

在 AWS 上实现「图片上传 → 自动生成缩略图 → 生成图片描述 → 前端展示」的端到端 Serverless 流水线，做到上传即产出可展示内容。整体采用最小权限与分层安全设计，支持弹性伸缩与可观测性（ALB/ASG、S3、Lambda、RDS、Secrets Manager、CloudWatch）。

#### 主要贡献:  
- Serverless 事件链落地：设计 S3→EventBridge→Lambda 的“上传即处理”链路，uploads/ 下新对象分别触发 Annotation 与 Thumbnail 两支函数，自动生成 caption 与 128×128 缩略图并回写存储/数据库。

- AI 能力与密钥治理：AnnotationFunction 读取原图并调用 Google Gemini 生成描述，(image key, caption) 落库到 RDS；Gemini/RDS 凭据统一放入 Secrets Manager，运行期注入，避免明文与硬编码。

- 弹性与高可用工程化：配置 ASG 期望实例、伸缩，并以 ~60% CPU 为阈值触发扩缩容；ALB 跨可用区分发流量，VPC 公/私子网 + NAT/Bastion 保障出网与运维安全。

- 性能与弹性验证：使用 ApacheBench 对 /upload 做 20 并发×500 请求压测，100% 成功、平均 41 ms、吞吐 484 req/s；CloudWatch 指标出现 CPU 峰值与回落，验证 ALB 分流与 ASG 扩缩容的有效性。