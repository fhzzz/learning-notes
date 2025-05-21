# 阅读列表
👋这里是带有少量笔记的新意图检测任务的论文阅读列表~

👉笔者是一个刚接触该方向的菜鸡研一，但在努力学习了（虽然也总是摆烂）。如果你和我的研究方向接近，欢迎来call我！邮箱: z13230021028@outlook.com

- **新意图检测**是什么？

	新意图检测(New Intent Discovery, NID)任务是指在识别已知意图的同时检测新意图并聚类，NID任务更符合现实世界的开放场景。
	
- 本列表的论文可分为两大类：深度聚类方法、结合LLMs的方法

- [这里](https://github.com/thuiar/OKD-Reading-List)是另一个关于意图识别的论文阅读列表，该列表不仅包含文本领域的意图识别，还包含CV领域的通用品类发现等多个相似任务，但作者好久没更新了，也没有LLM相关的论文

- 笔记均为个人阅读学习记录，如有错误还请指正~

- 该仓库下的其他文件夹说明在本文最后

## Content
- [深度聚类方法](#深度聚类方法)
	- [新意图检测](#新意图检测)
	- [意图识别其他细分方向](#意图识别其他细分方向)
	- [深度聚类综述](#深度聚类综述)
- [结合LLMs的方法](#结合llms的方法)
- [其他文件夹说明](#其他文件夹说明)

## 深度聚类方法
### 新意图检测
新意图检测任务本质上是文本分类任务，属于聚类问题的范畴，因此许多论文的方法其实依托于深度聚类，将深度聚类算法应用到新意图检测这一具体任务上，并针对该任务作出针对性改进。

- Ting-En Lin, Hua Xu and Hanlei Zhang. 2020. **Discovering New Intents via Constrained Deep Adaptive Clustering with Cluster Refinement**. In _Proceedings of AAAI 2020_. [[paper](https://arxiv.org/pdf/1911.08891.pdf)] [[code](https://github.com/thuiar/CDAC-plus)]
	- 解决问题：如何利用监督信息指导聚类过程
	- 方法：计算相似度矩阵作为监督信息优化模型 + KDL散度约束微调
	- 是端到端的半监督聚类方法，和深度聚类方法[DEC](https://arxiv.org/pdf/1511.06335)本质上无区别

- Hanlei Zhang, Hua Xu, Ting-En Lin and Rui Lyu. 2021. **Discovering New Intents with Deep Aligned Clustering**. In _Proceedings of AAAI 2021_.[[paper](https://arxiv.org/pdf/2012.08987.pdf)] [[code](https://github.com/thuiar/DeepAligned-Clustering)]
	- 解决问题：意图类别数量估计 / 聚类中心不一致
	- 方法：使用置信度筛选估计类别数量 / 提出深度对齐算法
		- 初始化：使用标记数据预训练PLM，估计K
		- （迭代）提取意图表示 -> K-means聚类 -> 对齐算法获取最终伪标签 -> 自监督学习更新参数
	- 半监督预训练+自监督学习（伪标签），在深度聚类方法[DeepCluster](https://arxiv.org/pdf/1807.05520)基础上提出对齐算法

- Hanlei Zhang, Hua Xu, Xin Wang, Fei Long, Kai Gao. 2023. **A Clustering Framework for Unsupervised and Semi-supervised New Intent Discovery**. _IEEE Transactions on Knowledge and Data Engineering_. [[paper](https://ieeexplore.ieee.org/document/10349963)] [[code](https://github.com/thuiar/TEXTOIR)]
	- 与前两篇论文为同一作者团队，更像是之前方法的集大成之作

- Yuwei Zhang, Haode Zhang, Li-Ming Zhan, Xiao-Ming Wu, Albert Y.S. Lam. 2022. **New intent discovery with pre-training and contrastive learning**. In _Proceedings of ACL 2022_. [[paper](https://aclanthology.org/2022.acl-long.21/)] [[code](https://github.com/fanolabs/NID_ACLARR2022)]
	- 解决问题：如何更好的提取语义信息、意图表示 / 如何更好地聚类话语
	- 本文方法
		- 多任务预训练（无标签数据和外部标记数据）
		- CLNN（正类样本中增加邻近样本）
	- 无监督训练，对比实验也都是无监督方法

- Z. Hu, Y. Xu, L. He and F. Nie, "Interactive Supervision for New Intent Discovery," in _IEEE Signal Processing Letters_, vol. 31, pp. 1680-1684, 2024, doi: 10.1109/LSP.2024.3416882.[[paper](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10564149)] [[code](https://github.com/Tarrius/INS/tree/main)]
- Rajat Kumar, Mayur Patidar, Vaibhav Varshney, Lovekesh Vig, and Gautam Shroff. 2022. [Intent Detection and Discovery from User Logs via Deep Semi-Supervised Contrastive Clustering](https://aclanthology.org/2022.naacl-main.134/). In _Proceedings of the 2022 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies_, pages 1836–1853, Seattle, United States. Association for Computational Linguistics.
- Xiang Shen, Yinge Sun, Yao Zhang, and Mani Najmabadi. 2021. [Semi-supervised Intent Discovery with Contrastive Learning](https://aclanthology.org/2021.nlp4convai-1.12/). In _Proceedings of the 3rd Workshop on Natural Language Processing for Conversational AI_, pages 120–129, Online. Association for Computational Linguistics. 
- Yunhua Zhou, Guofeng Quan, and Xipeng Qiu. 2023. [A Probabilistic Framework for Discovering New Intents](https://aclanthology.org/2023.acl-long.209/). In _Proceedings of the 61st Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)_, pages 3771–3784, Toronto, Canada. Association for Computational Linguistics. [[code](https://github.com/zyh190507/Probabilistic-discovery-new-intents)]
- Shun Zhang, Yan Chaoran, Jian Yang, Jiaheng Liu, Ying Mo, Jiaqi Bai, Tongliang Li, and Zhoujun Li. 2024. [Towards Real-world Scenario: Imbalanced New Intent Discovery](https://aclanthology.org/2024.acl-long.217/). In _Proceedings of the 62nd Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)_, pages 3949–3963, Bangkok, Thailand. Association for Computational Linguistics.
### 意图识别其他细分方向
- Haode Zhang, Yuwei Zhang, Li-Ming Zhan, Jiaxin Chen, Guangyuan Shi, Albert Y.S. Lam, and Xiao-Ming Wu. 2021. [Effectiveness of Pre-training for Few-shot Intent Classification](https://aclanthology.org/2021.findings-emnlp.96/). In _Findings of the Association for Computational Linguistics: EMNLP 2021_, pages 1114–1120, Punta Cana, Dominican Republic. Association for Computational Linguistics. [[code](https://github.com/fanolabs/IntentBert)]
	- 少样本意图检测
- Zhang, H., Xu, H., & Lin, T.-E. (2021). Deep Open Intent Classification with Adaptive Decision Boundary. _Proceedings of the AAAI Conference on Artificial Intelligence_, _35_(16), 14374-14382. [[paper](https://arxiv.org/pdf/2012.10209)] [[code](https://github.com/thuiar/Adaptive-Decision-Boundary)]
	- 开放意图检测
### 深度聚类综述
- Lu Y, Li H, Li Y, et al. A survey on deep clustering: from the prior perspective[J]. Vicinagearth, 2024, 1(1): 4. [[paper](https://arxiv.org/pdf/2406.19602)]
- Y. Ren _et al_., "Deep Clustering: A Comprehensive Survey," in _IEEE Transactions on Neural Networks and Learning Systems_, vol. 36, no. 4, pp. 5858-5878, April 2025, doi: 10.1109/TNNLS.2024.3403155. [[paper](https://arxiv.org/pdf/2210.04142)]

## 结合LLMs的方法
大型语言模型强大的语义理解能力、各种下游任务的优秀表现大家都有目共睹，因此近年来越来越多的论文尝试利用LLM的语义理解能力帮助解决新意图检测任务的痛点问题（比如更关注用户话语的语义信息）。

- Maarten De Raedt, Fréderic Godin, Thomas Demeester, and Chris Develder. 2023. [IDAS: Intent Discovery with Abstractive Summarization](https://aclanthology.org/2023.nlp4convai-1.7/). In _Proceedings of the 5th Workshop on NLP for Conversational AI (NLP4ConvAI 2023)_, pages 71–88, Toronto, Canada. Association for Computational Linguistics. [[code](https://github.com/maarten-deraedt/IDAS-intent-discovery-with-abstract-summarization)]
	- IDAS；选择原型样本后LLM生成摘要总结；ICL；平滑处理

- Jinggui Liang, Lizi Liao, Hao Fei, and Jing Jiang. 2024. [Synergizing Large Language Models and Pre-Trained Smaller Models for Conversational Intent Discovery](https://aclanthology.org/2024.findings-acl.840.pdf). In _Findings of the Association for Computational Linguistics: ACL 2024_, pages 14133–14147, Bangkok, Thailand. Association for Computational Linguistics.
	- SyCID；LLM优化话语和标签；对比学习

- Jinggui Liang, Lizi Liao, Hao Fei, Bobo Li, and Jing Jiang. 2024. [Actively Learn from LLMs with Uncertainty Propagation for Generalized Category Discovery](https://aclanthology.org/2024.naacl-long.434/). In _Proceedings of the 2024 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies (Volume 1: Long Papers)_, pages 7845–7858, Mexico City, Mexico. Association for Computational Linguistics. [[code](https://github.com/liangjinggui/ALUP)]
	- ALUP；高不确定性区域应用LLM；对比学习

- Jinggui Liang and Lizi Liao. 2023. [ClusterPrompt: Cluster Semantic Enhanced Prompt Learning for New Intent Discovery](https://aclanthology.org/2023.findings-emnlp.702/). In _Findings of the Association for Computational Linguistics: EMNLP 2023_, pages 10468–10481, Singapore. Association for Computational Linguistics.
	- CsePL；离散提示和软提示；对比学习

- Lu Fan, Jiashu Pu, Rongsheng Zhang, and Xiao-Ming Wu. 2024. [LANID: LLM-assisted New Intent Discovery](https://aclanthology.org/2024.lrec-main.883/). In _Proceedings of the 2024 Joint International Conference on Computational Linguistics, Language Resources and Evaluation (LREC-COLING 2024)_, pages 10110–10116, Torino, Italia. ELRA and ICCL. [[code](https://github.com/floatSDSDS/LANID)]
	- LaNID；数据采样后LLM判断样本对类别是否相同；对比学习

- Hong, M., “Dial-In LLM: Human-Aligned LLM-in-the-loop Intent Clustering for Customer Service Dialogues”, <i>arXiv e-prints</i>, Art. no. arXiv:2412.09049, 2024. doi:10.48550/arXiv.2412.09049. [[paper](https://arxiv.org/pdf/2412.09049)] [[code](https://anonymous.4open.science/r/Dial-in-LLM-0410/README.md)]
	-  Dial-in LLM；中文数据集；LLM动态评估语义一致性
- Rodriguez J A, Botzer N, Vazquez D, et al. IntentGPT: Few-shot Intent Discovery with Large Language Models[C]//ICLR 2024 Workshop on Large Language Model (LLM) Agents. [[paper](https://arxiv.org/pdf/2411.10670)]
## 其他文件夹说明
这原本是为督促本文学习而建的仓库，原打算将知识按周整理，但是后来发现这样对整理笔记太不友好了，所以第三周及之后全部变成了学习情况，而不再是知识、论文的整理，是非常私人化的记录，不过考虑到目前没什么人看到，所以懒得整理了，等之后会统一整理。

前段时间看到类似阅读列表的仓库，觉得制作这样一个列表挺好的，自己之后查找也更方便。再加上这只是一件重复、可以不带脑子做的事情（不过比想象中费事），所以做了这样一个列表，列表中的论文都是近段时间读过的文章，大部分都是ACL文章，质量应该还行。
