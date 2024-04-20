# 全同态加密（FHE）在区块链上的应用

## 1.FHE链上应用概述

FHE（Fully Homomorphic Encryption，全同态加密）是一种特殊的加密技术，允许在加密状态下执行计算，并在密文中直接进行操作，而无需解密数据。FHE在链上的应用可以解决一系列安全问题，它可以保护隐私数据交换（可应用于AI领域）、安全智能合约、隐私保护身份验证（类似暗池等）。尽管FHE技术在理论上为这些应用提供了解决方案，但在实际应用中仍然需要克服一些挑战，例如计算效率、密文大小膨胀等问题。此外，FHE的实现和集成也需要考虑到区块链的特殊性，如分布式环境和共识算法等。由于近些年实际技术的发展，FHE的实际应用已经不是遥不可及，FHE在区块链上的应用还是一块亟待发掘的热土。

## 2.Sunscreen

### 2.1项目介绍

基本信息：Sunscreen 是一个隐私引擎，旨在使工程师可以访问高级隐私技术（如 FHE），以便他们可以轻松构建和部署私有应用程序。

主页：https://sunscreen.tech/

blog：[Sunscreen](https://blog.sunscreen.tech/)

文档：https://docs.sunscreen.tech/

### 2.2解决的问题

#### 2.2.1FHE编译器

[SNARK 如何满足 FHE 的要求 (sunscreen.tech)](https://blog.sunscreen.tech/snarks-shortcomings/)

想法：如何让FHE对不是密码学专家的普通工程师更有用？

**高层次的想法：能否把一个“常规”程序（比如C++、Python或Rust程序）变成一个对加密数据进行操作的FHE呢？**

sunscreen:构建一个FHE编译器，使FHE 快速同时易于访问，同时使得编译器的开销保持在10-100。

#### 2.2.1 零知识证明结合	

[SNARK 如何满足 FHE 的要求 (sunscreen.tech)](https://blog.sunscreen.tech/snarks-shortcomings/)

在**无信任环境**中使用FHE时，用户通常必须（a）加密其输入，（b）证明这些输入密文“格式良好”，最后（c）证明其明文输入满足任何与应用程序相关的条件。

为了解决（a），sunscreen开发了其FHE编译器，并已经发布了它的初始版本。为了解决 （b），sunscreen为 SDLP（短离散对数证明） 校对系统开发了一个 GPU 加速库。为了解决 （ｃ），sunscreen正开发一个支持SNARK（简短无交互证明）的**ZKP编译器**，并将其插入SDLP 库（即允许证明者证明他们已经在两个证明系统中提交了相同的输入）。

#### 2.2.4可验证的私人拍卖

[使用 FHE 建立可验证的私人拍卖 (sunscreen.tech)](https://blog.sunscreen.tech/building-private-verifiable-auctions/)

Sunscreen正在努力通过FHE启用一类在私有共享状态下运行的新型应用程序。这些应用程序（例如拍卖，更有趣的是确定区块空间排序）往往有两个要求——**输入隐私**（即使在程序完成后也隐藏输入）和**可验证性**（我们如何知道程序是否正确运行？）

一条链上的两个去中心化交易所 （DEX） 之间可能存在套利机会，以太坊的交易顺序同gas价格挂钩，cosmos交易顺序遵从FIFO规则，而这会对普通用户和搜寻者带来许多问题。

sunscreen试图通过**阈值FHE**（如何最好构建阈值FHE还没有共识）来实现拍卖，使拍卖更加透明，同时确保失败的出价对所有人保密。

#### 2.2.5暗池

[建造一个真正黑暗的黑暗池 (sunscreen.tech)](https://blog.sunscreen.tech/building-a-truly-dark-dark-pool-2/)

构建一个暗池，即使是暗池操作员也无法查看订单簿。（sunscreen仅仅做了个演示来展现这样暗池可能的样子）

### 2.3发展情况

#### 2.3.1融资

2022-07-18： Sunscreen 完成 465 万美元种子轮融资

#### 2.3.2roadmap

 web3 中支持 FHE，需要先解决几个主要挑战：

1. 性能对于各种应用程序都非常重要，但对于与金融和交易相关的应用程序更是如此。不幸的是，开发人员很难有效地使用 FHE，这既是因为学习曲线陡峭，也是因为设置 FHE 程序以获得良好的性能非常困难。
2. web3 的原则之一是“不信任，验证”。如果用户向 （d） 应用程序提供加密数据，如何知道用户提供的输入满足应用程序的条件，而不仅仅是一些垃圾值？请记住，没有其他人可以检查输入，因为它们始终是加密的！
3. 虽然 web2 中的存储非常便宜，但 web3 并不总是如此。对于某些类别的应用程序来说，完全同态加密的速度非常快，但它的空间效率不是很高。那么我们如何在 web3 中使用 FHE？

在Sunscreen，其正在努力分阶段解决这些问题。到目前为止，Sunscreen的首要任务是解决第一点问题。在此过程中，Sunscreen构建了一个针对 web3 开发人员需求量身定制的 FHE 编译器。Sunscreen现在将重点转向解决问题 #2 和 #3;为此，Sunscreen一直在开发一个与我们的 FHE 编译器兼容的零知识证明编译器（这样就可以证明有关加密数据的事情），以及与去中心化存储系统的集成，该系统可用于在链下存储更大的密文。

#### 2.3.3合作生态

投资：Polychain*、Coinbase Ventures、dao5、Lattice Capital、Gaingels、Northzone、Vasiliy Shapovalov、Naval Ravikant、Michael Egorov、Tux Pacific、Omer Shlomovits、Konstantin Lomashuk、Lisa Cuesta Bunin、Viktor Bunin

## 3.Cluster Protocol

### 3.1项目介绍

基本信息：Cluster Protocol 是去中心化人工智能模型的计算验证协议和开源社区。通过巧妙地集成全同态加密（FHE），Cluster 通过促进 GPU 提供商的安全和一致的奖励，确保了范式的转变，从而增强了全球个人和中小企业的能力。

主页：https://www.clusterprotocol.io/

blog：https://www.clusterprotocol.io/blogs

gitbook：https://cluster-protocol.gitbook.io/

### 3.2解决的问题

通过为计算能力提供一个去中心化的市场，Cluster Protocol确保人工智能的进步只受到想象力的限制，而不是硬件的可用性。

即通过区块链技术和FHE，cluster protocol企图营造一个安全、高效和社区驱动的环境，用于 AI 开发和部署，同时保证数据的安全性（通过FHE）。

### 3.3发展情况

#### 3.3.1融资

无

#### 3.3.2roadmap

2023年第四季度： 团队组建和白皮书、生成式人工智能研发、计算protcol开发证明

2024年第一季度：用于计算证明的激励测试网推出；支持机密计算环境和硬件；加入第一波AI合作伙伴；启用GPU列表和租赁市场；平台上线测试版，用于 AI 模型列表；Deploy to Earn 实施；代币发行和空投；ClusterBUILD社区 - GPU节点、AI模型部署者和AI模型用户的网络。AI 模型列表的测试版上线

2024年第二季度：主网启动；代币委托；SDK和API，供企业构建/部署模型；支持联邦学习；与存储/CDN合作伙伴的集成；整合去中心化数据集；在去中心化数据集上训练自己的自定义模型；将生态系统资金作为赠款进行分配，使建设者能够在我们的平台上进行建设

#### 3.3.3合作生态

Team：Prateek Bhatia（CEO and Co-Founder）；Yatharth Jain（CBO and Co-Founder）；Nishant Chinchole（COO）

Backers & Investors：Pivot，Genesis Capital



## 4.Privasea

### 4.1项目介绍

基本信息：Privasea 是一个去中心化的人工智能网络，通过FHEML实现数据价值的流通。该网络为 FHE AI 运行提供分布式计算资源。整个系统由 ZAMA 的 具体机器学习和 $PRVA 代币的激励众包支持。

主页：https://www.privasea.tech/

blog：https://www.clusterprotocol.io/blogs

gitbook：https://cluster-protocol.gitbook.io/

白皮书：[Privasea_Whitepaper.pdf - Google 云端硬盘](https://drive.google.com/file/d/1jbxWMgEziupt119gvM1n0Mu8sDdM7VWF/view?pli=1)

### 4.2解决的问题

privasea是一个去中心化的人工智能，其对FHE的应用主要集中在对数据加密后，FHE允许对加密数据进行计算，无需暴露原始信息。从而确保了模型评估的整个工作流程中用户数据的隐私和安全。

privasea主要的应用如下：***人类肖像证明***（即将推出）、医疗保健数据共享、寻找银行联名客户、安全生物识别算法和加密数据集数据分析（具体内容并没有提及。

### 4.3发展情况

#### 4.3.1融资

2024-03-04：Privasea 完成 500 万美元种子轮融资

2024-04-03：Privasea 完成战略融资，金额未披露

#### 4.3.2roadmap

2023之前Pri-Auto：解决如何安全地收集持续生成的用户数据并共享这些数据。

至今：去中心化的人工智能网络，最主要的应用开发是人类的肖像证明。

#### 4.3.3合作生态

 Mind Network：Privasea 和 Mind Network 正在合作加强数据加密和安全共享，为更安全、更高效的数据驱动运营铺平道路，专注于隐私。

Vinnova Fordonsstrategisk Forskning och Innovation （FFI）：FFI对Pri-Auto项目进行了资助。

投资方：Binance Labs、MH Ventures、Gate Labs、Duckdao、Basics Capital、1NVST、K300 Ventures、Zephyrus Capital、Dewhales Capital、Oxbull、Danu Ventures、QB Ventures、OKX Ventures、Laser Digital、Tané。

## 5.Mind Network

### 5.1项目介绍

基本信息：Mind Network 是一个零信任层，旨在为 Web3 带来下一个十亿用户和数万亿美元。 Mind Network提供安全和数据隐私解决方案，可实现真正的 CrossFi 规模，符合监管要求，同时恪守资产代币化和个人数据所有权的 Web3 原则。

**零知识证明+全同态加密**

主页：https://mindnetwork.xyz/

github：https://github.com/mind-network

mirror：[Mind Network (mirror.xyz)](https://mirror.xyz/0x305Fe52006E3738404A3016966e98c3b3e9D3b1b)

medium：https://mindnetwork.medium.com/

### 5.2解决的问题

#### 5.2.1 关键技术（FHE-DKSAP）

[FHE-DKSAP: Fully Homomorphic Encryption based Dual Key Stealth Address Protocol - Cryptography - Ethereum Research (ethresear.ch)](https://ethresear.ch/t/fhe-dksap-fully-homomorphic-encryption-based-dual-key-stealth-address-protocol/16213)

隐身地址 （SA） 可防止区块链交易与收件人的钱包地址公开关联，它有效地隐藏了交易的实际目的地址，对保护收件人的隐私并阻止对交易流的社会工程攻击至关重要。FHE-DKSAP具有如下优势：FHE-DKSAP 将 **EC 替换为 FHE**，以提高安全级别。FHE 构建了格加密，并在构建时配备了 FHE-DKSAP 以**防止量子计算攻击**。FHE-DKSAP中的SA是安全的，可以复用，不需要产生大量的SA，从而**降低了SA采用的复杂性和难度**。与EIP-5564中的双密钥设计相比，FHE-DKSAP中的设计可以帮助接收者**外包检查整个链中包含SA的资产**的计算，而不会泄露其视图密钥。

#### 5.2.2 可以解决Web3 安全方面的的关键挑战

Mind Network 通过为 Web3 用户提供保护数据、智能合约和 AI 的解决方案，解决了 Web3 安全方面的关键挑战：

**加密数据湖**：Mind Network 利用先进的加密机制来保护 L1/L2 链、去中心化存储和公共云中的敏感信息。它还提供了一个易于使用的开发套件，其中包含 SDK、IDE 和预构建的集成，可消除任何障碍，并允许任何人创建和使用他们的私有数据湖。通过这种方法，用户数据保持机密和安全，确保隐私和数据所有权。

**安全智能合约**：通过利用 Mind Network 的零信任架构，智能合约可以防止未经授权的访问和潜在的操纵。这确保了合同执行过程的完整性和可靠性。Mind Network与Chainlink合作，提出了一种解决方案，以保护Oracle服务，将敏感的链下数据传输到智能合约。

**零信任 AI**：在人工智能时代，保护隐私的计算至关重要。Mind Network 使开发人员能够对加密数据执行计算，在利用 AI 功能的同时保护隐私。这种革命性的方法可以保护敏感的 AI 模型免受未经授权的访问，并确保用于训练和推理的数据的机密性。

#### 5.2.3广泛应用（零信任层：零知识证明+全同态加密）

1、解决**跨链桥领域**急需的安全需求，可以再在一系列场景中提供增强的安全性：a、**银行链到公链**：将传统金融系统安全地桥接到公共区块链，促进无缝交易，同时保护敏感的金融数据；b、**CBDC链到公链**：促进央行数字货币融入公链世界，保障数字资产的隐私和安全；c、**公链到公链**：促进不同公链之间的安全跨链交互，拓展去中心化金融（DeFi）的视野，实现数字资产的自由流动。（MindSAP）

2、**增强单链隐私**：Mind Network是MetaMask ETHSG黑客松的首个获奖方案，可增强链上转账、买卖、质押等操作的交易隐私。它能遵循不同地区的监管框架。（MindSAP）

3、**AI数据保护**：作为AI解决方案的数据隐私rollup，Mind Network能通过用户私钥对数据加密，并允许AI应用在不解密的情况下进行计算。Mind Network已与Filecoin、Arweave和Greenfield在多个用例上进行了合作和集成。（MindSAP）

4、**Restaking:**Restaking 利用以太坊的共识层将加密经济安全性扩展到网络的其他应用程序上。但是Restaking面临着中心化、风险加剧和数据安全等挑战。Mind Network 以其核心 FHE 运算网络为基础，引入了 FHE 再质押层，以利用尖端的 FHE 技术来保护 AI 和 DePin 网络。（MindSAP）

#### 5.2.4推出的产品（截止2024.2.22）

1） MindLake：基于 Arweave、IPFS 和 Greenfield 的 AI、DePin 和游戏用例支持 FHE 的数据隐私和安全汇总解决方案。

2）MindSAP：以太坊基金会授予的FHE隐形地址协议，有助于在著名的公链和Chainlink CCIP上进行合规和安全的价值转移。

3.） MindRollup（即将推出）：与顶级合作伙伴合作的 FHE 重新质押汇总。



### 5.3发展情况

#### 5.3.1融资

2023-06-29：Mind Network 完成 250 万美元种子轮融资

#### 5.3.2roadmap

主要围绕零知识证明和全同态加密构成的零信任层可以解决的一系列问题发展。

#### 5.3.3合作生态

投资方：Binance Labs、SevenX Ventures、HashKey Capital、Comma3 Ventures、Big Brain Holdings、Mandala Capital、Arweave SCP Ventures。









