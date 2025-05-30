


> Written with [StackEdit中文版](https://stackedit.cn/).

# 油文智鉴——基于大模型的全球多语种油气行业文档自动标注开拓者
## <center>**目录**</center>
- **项目介绍**
- **系统框架**
- **业务场景**
- **运行测试**
## <center>**项目介绍**

基于与国外油气企业的合作和对国内外油气行业文档管理现状的调查，我们发现随着油气行业文档数量、类型与复杂程度的激增，现有管理体系效率和准确率较低，无法适应油气行业数字化转型的新趋势。因此，本项目拟研究基于人工智能的油气文档自动标注系统，以节约油气文档标签标注的时间成本，提高文档查找效率。

<div align="center">

[
![油气行业实图](https://github.com/Hongwuwu/PetroLingu/blob/main/image/油气行业实景图.png?raw=true)
](https://github.com/Hongwuwu/PetroLingu/blob/main/image/油气行业实景图.png?raw=true)


</div>

项目利用大语言模型、自然语言处理和文本提取等技术，分析文档内容，生成相应的标签。通过精准的标签化，用户可以简单、高效的查找指定主题的文档。本项目致力于将该创新方案应用于油气行业文档管理，通过实现数据的全面存储和分析，促进油气行业数字化转型和智能化发展。

通过此项目，我们希望将我们的专业技能和兴趣特长应用于油气领域，为推动该行业的数字化转型和智能化发展尽绵薄之力。同时，我们期待着油文智鉴走出国门，面向更加广大的世界油田，提供中国的文档自动标注方案。我们将利用先进的自然语言处理技术，自动化处理和分析大量的文档数据，从而提高工作效率和决策准确性。在此基础上，未来我们还计划开发一系列智能工具，帮助油气行业的从业者更好地管理和利用数据。这些工具将包括自动标注系统、智能搜索引擎、数据可视化平台等，旨在简化复杂的数据处理流程，提供更直观的分析结果，实现人工智能协同研究智能分析。我们相信，借助这个平台，我们能够将我们的技术创新转化为对社会有益的实际成果。

##  <center>**系统框架**
### 系统架构
<div align="center">

[![系统架构图](https://github.com/Hongwuwu/PetroLingu/blob/main/image/%E6%9E%B6%E6%9E%84.png?raw=true)](https://github.com/Hongwuwu/PetroLingu/blob/main/image/%E6%9E%B6%E6%9E%84.png?raw=true)


</div>

- **用户接入层**
可实现将请求精准导向目标服务器，把请求合理分配到后端，避免单个服务器负载过重，保障系统稳定、安全运行。

- **核心服务注册与配置层**
存储系统各类配置信息，包括大模型接口地址、文档存储路径等，可实时获取配置更新，实现动态配置调整，依据用户角色分配权限，保障系统安全。

- **业务服务集群层**
便捷集成大语言模型，可提取文档文本内容与元数据、向模型发送油气行业文档及标签，接收并处理标注结果，实现文档高效标注、检索、存储和标注结果展示。

- **消息与事务处理层**
异步处理任务，可实现更新索引、通知用户等后续操作，缓解系统高峰压力；分布式事务保障数据一致性与事务完整性。

- **数据存储层**
支持分布式存储与快速访问，数据库分库包括标签库、文档库、标注规则库、标注结果库等；缓存集群可缓存常用数据，如热门文档、高频标签等，减少数据库访问，提升系统响应速度。

- **监控与治理层**
追踪请求在各服务间调用链路，记录时间、参数等信息；收集系统各模块日志，存储后分析；弹性伸缩，依据负载自动调整服务实例数量，便于运维人员掌握系统状态、排查问题

- **后端运营管理**
涵盖权限管理、标注规则管理、模型参数管理、标注质量审核等功能，为系统运营提供管理支撑，确保系统有序运行.

### 系统模块
- #### 标签生成模块
[![pERhcTg.png](https://github.com/Hongwuwu/PetroLingu/blob/main/image/%E6%A8%A1%E5%9D%97.png?raw=true)](https://github.com/Hongwuwu/PetroLingu/blob/main/image/%E6%A8%A1%E5%9D%97.png?raw=true)

**文档标注步骤**
1. 接收来自用户的非空传入文档
2. 对文档中的PDF文件进行文本提取
3. 将整合的文本文档用于无监督学习
4. 聚类结果在去除重复和无意义字符后，可加入系统标签库。
- #### 文档自动标注模块
[![pERh2kQ.png](https://github.com/Hongwuwu/PetroLingu/blob/main/image/%E6%A8%A1%E5%9D%972.png?raw=true)](https://github.com/Hongwuwu/PetroLingu/blob/main/image/%E6%A8%A1%E5%9D%972.png?raw=true)

**文档标注步骤**
1. 提取文档文本信息
2. 将文本信息与标签库同时传入大模型进行匹配
3.  若匹配成功，则输出文档标注结果；若匹配失败，则由大模型依照标签体系格式生成适当标签
4. 输出标注结果并将新标签处理后整合入标签库中，实现标签体系自动更新。
### 系统功能
[![pERhRYj.png](https://github.com/Hongwuwu/PetroLingu/blob/main/image/%E5%8A%9F%E8%83%BD.png?raw=true)](https://github.com/Hongwuwu/PetroLingu/blob/main/image/%E5%8A%9F%E8%83%BD.png?raw=true)
- 网页端：文档输入、标签生成、自动标注、标签列表显示和输出标注结果；
- 后台端：调整数据处理和标注规则、无监督学习参数调节和大模型服务质量评估。

## <center>**业务场景**

**勘探报告著能解析与标注**
针对地质勘探报告、地震数据文档等，自动识别并标注地层结构、油气储量、钻探风险等信息，辅助工程师快速提取有效信息，减少人工查阅时间。

**钻井工程日志自动化标注**
自动解析钻井日志中的井深、钻速、泥浆参数等结构化数据，标注异常事件（如井漏、卡钻），为后续钻井优化提供数据支持。

**设备维护记录分类与知识抽取**
从设备维护文档中自动标注故障类型、维修部件、维护周期等信息，构建设备健康档案，支持预测性维护决策。

**安全文档审核**
识别安全规程、事故报告中的合规性条款，标注潜在违规风险（如未达HSE标准），提升合规审查效率。

**采油工艺文档知识图谱构建**
从采油工艺手册中抽取注水参数、增产措施等技术术语及关联关系，构建行业知识图谱，支持技术经验传承。

**环境评估报告摘要生成**
对环境影响评估报告中的污染指标、生态保护措施进行标注，并生成可视化摘要，便于管理层快速决策。

**多语言文档跨语言对齐**
针对跨国项目中的多语言技术文档（如英文钻井规范、中文设备手册），自动标注语义对齐内容，支持跨团队协作。 

## <center>**运行测试**

- ### 关联性分析
对TopK关键词与经验标签的关联性评价，有如下两个方法：由LLM对TopK个经验标签进行描述再判该描述与经验标签描述的关联性 。

#### <center>Llama基于经验标签打标结果示例</center>

<div align="center">

| 文档序号 | 标签                                                                                                 |
|----------|:--------------------------------------------------------------------------------------------------:|
| 6        | - Quality Assurance Audit Report<br>- Quality Assurance Certificate<br>- Quality Assurance General Technical Note<br>- Quality Assurance General Work Instruction<br>- Quality Assurance Manual |
| 26       | Telecommunication Block Diagram Facility                                                         |
| 31       | - Telecommunication Block Diagram<br>- Telecommunication Certificate Approval<br>- Well Engineering Plan Drilling |
| 58       | - Telecommunication Block Diagram<br>- Telecommunication Certificate<br>- Telecommunication Datasheet<br>- Telecommunication Specification |

</div>

- ### 文档标注

#### <center>清洗后的基于Deepseek的标注结果示例</center>

<div align="center">

[![pER5V54.jpg](https://github.com/Hongwuwu/PetroLingu/blob/main/image/results.png?raw=true)](https://github.com/Hongwuwu/PetroLingu/blob/main/image/results.png?raw=true)

</div>






