### FAIC功能介绍：
1、FAIC区块链技术框架为：模块化区块链、PoS共识机制、分层验证机制、vllm框架、零知识证明优化zk-stark、全同态加密fhe。
2、FAIC集成ollama全部功能，定时获取模型列表、模型名称、模型介绍、模型下载。且允许用户使用ollama的方法部署自己的模型，和使用第三方AI公司的API，如claude、openai、google等。
3、用户选择指定的算力节点与AI模型
  1、当该节点的算力能满足用户需求时，全程由该节点完成算力服务。
  2、当该节点的算力不能满足用户需求时，该节点会使用vllm框架，让更多的算力节点参与，从而完成算力服务。
4、FAIC奖励办法（测试网络暂行办法）
  1、提供算力并获得验证：获得1FAIC/1tokens的奖励
  2、提供路由服务并获得验证：获得15FAIC/1request的奖励
  3、验证其他节点提供算力或路由服务：获得30FAIC/1request的奖励
  4、算力节点在线时长并获得验证：获得60FAIC/1hour的奖励
  5、验证节点在线时长并获得验证：获得60FAIC/1hour的奖励
  6、用户在官网捐赠给FAIW公共钱包，即可获得FAIC。
  7、路由服务奖励机制：
    a) 在线时长：10FAIC/1hour，每半小时遍历一次节点。
    b) 成功匹配次数：3FAIC/1request

### FAIC用户操作逻辑
第一步：用户选择节点和选择模型
第二步：程序连接节点和模型，判断成功与否
第三步：用户输入问题，程序将问题发送给节点，并等待节点返回结果
第四步：用户选择结束任务，程序关闭与节点的链接，并删除请求信息；超过30分钟未发生任何操作，节点自动关闭与删除当前请求与请求信息。

### FAIC架构
1、FAIC用户客户端，使用flutter开发：
  1、ios
  2、android
  3、web
2、FAIC节点程序：完全通过命令行操作,使用rust开发
  1、FAIC算力节点程序
    1、包含功能：算力节点、验证节点、路由节点
    2、算力节点中的验证节点功能默认设置零知识证明优化（ZK-STARK）
    3、算力传输过程默认为未加密，节点也可以手动设置为全同态加密（FHE）。
    4、算力节点应当隐藏并加密节点信息，不被查询，预防节点被攻击。
    5、算力节点验证、存储和维护整个区块链数据，包括所有区块、交易、状态数据。
  2、FAIC验证节点程序
    1、包含功能：验证节点、路由节点
    2、验证节点默认设置零知识证明优化（ZK-STARK）
    3、验证节点应当隐藏并加密节点信息，不被查询，预防节点被攻击。
    4、验证节点只存储区块链的部分数据（如区块头），依赖算力节点获取完整数据。
    5、验证交易和区块头信息，但不存储所有历史数据。

### 用户客户端功能
0、FAIC钱包
  1、基于"无需注册"和"非托管"的原则，像metamask一样。
  2、注册流程参照metamask
    1、确认用户协议
    2、输入密码即可创建钱包
    3、创建成功后，用户即可获得一个钱包地址和助记词，建议用户备份助记词。
  3、登录流程参照metamask
    1、用户注册成功后，帐户信息缓存在应用中，用户下次登录时，输入密码或指纹识别、面部识别等手段即可登录。
  4、跨链支持
    1、支持主流的区块链网络，如：以太坊、比特币、波卡、solana等。
    2、支持主流的跨链桥，如：anyswap。
  5、钱包页（首页）
    1、显示用户钱包地址
    2、显示用户不同代币的余额
  6、钱包菜单底栏
    1、钱包页
    2、交易记录
    3、动作弹窗
      1、买入
      2、卖出
      3、兑换
      4、跨链桥
      5、发送
      6、接受
    5、设置
1、菜单栏：
  1、节点列表
  2、历史任务：显示所有节点和模型下的所有历史任务
  3、FAIC钱包
  4、设置
  5、关于（以下信息全部在一个页面中，文字铺排）
    1、关于FAIC
    2、免责声明
    3、隐私政策
    4、使用条款
    5、版本号
  6、用户引导流程
2、用户与AI交互模块
  1、当前选择的节点名称、模型名称
  2、新建任务
  3、历史任务：显示当前节点和模型下的所有历史任务
  4、用户信息互动栏：
      1、文本输入框；
      2、语言按钮：按住开始录音，松开结束录音，并发送录音内容；
      3、图片按钮：选择本地图片，并发送图片内容；
      4、文件按钮：选择本地文件，并发送文件内容；
      5、视频按钮：选择本地视频，并发送视频内容；
      6、多模态：文本、图片、语音、视频；如果用户选择的节点和模型不支持对应模态，则在用户发送请求的窗口对应该模态的按钮变为灰色且不可点击，并提示用户该节点和模型不支持该模态。
  5、用户与AI交互窗口：
      1、用户输入的文本、图片、语音、视频会显示在窗口中。
      2、AI返回的信息，如：文本、图片、语音、视频会显示在窗口中。
      3、AI每条返回的信息的下方都会有复制、分享、重新生成三个按钮。
  6、错误判断
      1、当用户输入的文本、图片、语音、视频为空时，程序会提示用户输入内容不能为空。
      2、选中的节点如果在任务中离线，或响应时间超过20秒，则提示用户节点离线或响应超时，并提示用户选择其他节点。
3、节点列表（对节点列表中涉及到底层的ip地址以及延迟信息应当进行加密，预防节点被攻击）
  1、节点筛选
      1、延迟筛选：低于100ms的节点，100~200ms的节点，200ms以上的节点。
      2、模型筛选：
          输入模型描述文本中的关键字，如“生图”、“llama3”、“gpt4”等。
          根据关键词匹配节点列表中的节点，并显示匹配的节点列表。
  2、节点名称，由节点提供者填写
  3、节点描述，由节点提供者填写
  4、节点支持的模型描述文本，由节点提供者填写
  5、节点延迟
  6、加密办法：
      1、零知识证明（ZK-STARK）
      2、全同态加密（FHE）
  7、节点操作按钮
      1、选择
      2、收藏（收藏后，该节点会置顶在列表最上方）
4、历史任务：用户可以查看历史任务，并选择继续该任务。该历史任务缓存在本地。
  1、当用户选择历史任务时，用户与AI交互窗口会显示该历史任务的输入和输出。
  2、当用户在该历史任务再次发起请求时，程序会先把历史会话打包压缩发给节点，节点会结合历史会话与新的请求内容继续生成回答。    

### FAIC算力节点程序
  1、适用于高性能个人电脑、服务器、服务器中心。
  2、算力节点程序会同时具有设置AI模型、提供算力功能、验证功能、路由功能。
  3、算力节点可以使用CPU、GPU硬件资源。
  4、算力节点采用vllm模型框架提升算力节点的并发能力与吞吐能力。当用户的请求当前算力节点无法满足时，可通过vllm调用其他算力节点，从而完成算力服务。
  5、算力节点可以配置多个AI大模型，并且能够同时运行。
  6、用户发起算力请求后，在用户没有选择结束任务时或在30分钟以内一直保持与该节点的该模型的链接，从而实现AI短期记忆保存能力。超过30分钟节点自动关闭与删除当前请求与请求信息。
  7、用户从历史任务中发起的新请求，用户客户端会先将历史任务中的信息打包压缩，然后发送给算力节点，算力节点会结合历史信息与新请求内容继续生成回答。
  8、响应用户算力需求且完成算力服务的节点，且进过分层验证机制，该算力节点将获得FAIC的奖励。
  9、算力节点的算力服务默认未加密，节点也可以手动设置为全同态加密（FHE）。
  10、算力节点的验证功能与路由功能与验证节点程序相同。

### FAIC验证节点程序
1、适用于低性能个人电脑、服务器、服务器中心。
2、验证节点程序会同时具有验证功能、路由功能。
3、最快速验证算力服务与路由服务的三个验证节点，将获得FAIC的奖励。
4、验证节点需质押FAIC以获得验证权：
  1、初始阶段（前1000个验证节点）：
    - 无需质押即可成为验证节点
    - 通过提供验证服务获得初始FAIC
    - 重点关注节点的服务质量和稳定性
  2、过渡阶段（第1001~10000个验证节点）：
    - 开始引入质押机制
    - 设置较低的质押门槛：100000USDT
    - 给予现有节点过渡期完成质押
  3、正式阶段：（第10001~无限的验证节点）：
    - 实施完整的质押验证机制
    - 需达到最低质押要求：1000000USDT
    - 按质押量分配验证权重
5、验证节点主要功能：
  - 验证代币交易的合法性
  - 验证区块的有效性
  - 参与区块共识
  - 维护账本状态
  - 验证算力服务
  - 提供路由服务
6、验证节点的奖励来源：
  - 区块验证奖励
  - 交易手续费
  - 算力服务验证奖励
  - 路由服务奖励
7、恶意行为将被惩罚，包括剔除节点、删除节点绑定的钱包、削减质押等

### FAIC路由说明
1、集成在算力节点、验证节点程序中
2、定时获取FAIC算力节点列表：
  - 节点名称文本
  - 节点描述文本
  - 节点支持的模型描述文本
  - 节点延迟
  - 节点加密办法：零知识证明优化（ZK-STARK）、全同态加密（FHE）
  - 节点类型(个人电脑/个人服务器/服务器中心)
3、完成路由服务且获得验证的节点，将获得FAIC的奖励。

### 分层验证机制：
  1、第一层：快速响应验证
    目的：快速确认算力服务的可用性和初步合法性
    验证节点数量：3个随机验证节点
    验证内容：
      算力节点是否完成用户请求的算力服务
      服务质量指标(完成时间、AI回答准确率等)
      交易验证
  2、第二层：区块打包验证
    目的：将已通过快速验证的交易打包进区块
    验证节点数量：至少33%的活跃验证节点参与
    验证内容：
      第一层验证结果的合法性
      算力服务的完整性验证
      服务质量指标(完成时间、AI回答准确率等)
      交易验证
      交易双方的身份和权限验证
      FAIC奖励计算的准确性
  3、第三层：最终确认验证
    目的：确保交易的最终不可逆性
    验证节点数量：全网超过51%节点共识
    验证内容：
      区块的完整性和合法性
      跨区块交易的一致性
      长期历史记录的维护
  4、奖励分配机制
    第一层验证节点：获得20%的验证奖励
    第二层验证节点：获得50%的验证奖励
    第三层验证节点：获得30%的验证奖励

### 统一的错误处理框架
1、服务节点、算力节点使用rust中的result或option类型，并使用统一的错误处理框架。
  1、计算资源不足: 例如，GPU/CPU资源耗尽。需要监控资源利用率，并在接近阈值时报警或自动扩展资源。
  2、网络延迟或断开: 节点之间的通信问题。可以设置心跳检测（heartbeat）来确保节点在线。
  3、数据一致性错误: 特别是在区块链验证中，确保数据的完整性和合法性。使用分层验证机制来逐层确认数据的准确性。
2、用户客户端使用flutter中可以定义全局的错误处理widget或service，集中管理和展示错误信息。
  1、输入错误: 例如，用户输入格式不正确或者必填字段为空。可以使用客户端验证（如表单验证）来捕捉这些错误。
  2、网络错误: 如无法连接到节点或API超时。可以使用网络状态监控库来预判和处理这些情况。
3、错误日志记录：确保每个错误都记录到日志中，提供足够的上下文信息（例如用户ID、请求内容、发生时间等）。这有助于后续的调试和分析。可以使用日志库如log或tracing在Rust中，或者Flutter中的logging包。
4、错误状态判断与反馈：
  1、即时反馈: 对于用户操作，提供即时反馈，如通过UI提示用户当前状态（如“正在处理”或“连接失败”）。
  2、状态机设计: 使用状态机来管理节点或客户端的状态转换，确保每个状态都有相应的错误处理逻辑。例如，当节点从“在线”变为“离线”，立即触发适当的错误处理流程。
  3、断点续传和重试机制:
    在节点通信中，设计断点续传逻辑，确保在网络中断后可以从上次失败的地方继续操作。
    实现合理的重试策略，比如指数退避重试，以处理瞬时的网络问题。
5、错误码列表
6、测试策略
  1、单元测试: 测试每个单独的功能模块的错误处理能力。
  2、集成测试: 验证系统组件之间的交互，特别是在跨节点的操作时是否能正确处理错误。
  3、压力测试: 模拟高并发或资源紧张情况下的错误处理表现。

### 开发计划
1、先开发用户客户端、验证节点程序；实现钱包功能和区块链转账功能。
2、开发算力节点程序，实现算力节点功能。
3、将路由节点程序融入算力节点与验证节点程序中。
4、FAIC要求使用模块化区块链、vllm框架、零知识证明优化zk-stark、全同态加密fhe、区块链分层验证机制。
  1、算力提供默认未加密，节点可以选择全同态加密和零知识证明优化zk-stark。
  2、验证节点默认设置零知识证明优化zk-stark
  3、当该节点算力不足以满足用户需求时，该节点会使用vllm框架，让更多的算力节点参与，从而完成算力服务。
5、完整开发FAIC奖励机制。


