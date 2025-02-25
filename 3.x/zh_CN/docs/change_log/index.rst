##############################################################
版本和兼容性
##############################################################

标签：``版本特性`` ``Release Note``

------------

.. important::
    相关软件和环境版本说明！`请查看 <https://fisco-bcos-documentation.readthedocs.io/zh_CN/latest/docs/compatibility.html>`_

FISCO BCOS 3.x 新特性
---------------------


微服务架构
>>>>>>>>>>>>>>

FISCO BCOS 3.0版本采用 **微服务模块化** 设计架构，总体上系统包含接入层、调度层、计算层、存储层和管理层:

- **接入层**：负责区块链 **连接的能力** ，包括提供P2P能力的“对外网关服务”和提供给SDK访问的“对内网关服务”。

- **调度层**：区块链内核运转调度的“大脑中枢”系统，负责整个区块链系统 **运行调度**，包括网络分发调度、交易池管理、共识机制、计算调度等模块。

- **计算层**：负责 **交易验证**，将交易解码放入合约虚拟机中执行，得到交易执行结果，是整个区块链的核心。

- **存储层**：负责 **落盘存储** 交易、区块、账本状态等数据。

- **管理层**：为整个区块链系统各模块实现 **可视化管理** 的平台，包括部署、配置、日志、网络路由等管理功能。FISCO BCOS 3.0系统架构基于开源微服务框架Tars构建。


----

灵活易拆分的微服务模块
>>>>>>>>>>>>>>
----

支持 **灵活拆分组合** 微服务模块，可以构建不同形态的服务模式，目前包括:

- **轻便Air版**：采用all-in-one的封装模式，将所有模块编译成一个二进制（进程），一个进程即为一个区块链节点，包括网络、共识、接入等所有功能模块，采用本地RocksDB存储，适用于初学者入门、功能验证、POC产品等。

- **专业Pro版**：包括RPC、Gateway服务和多个区块链节点Node服务组成，多个Node服务可构成一个群组，所有Node共用接入层服务，接入层的服务可平行扩展，适用于容量可控（T级以内）的生产环境。

----

两阶段并行拜占庭共识
>>>>>>>>>>>>>>
----

为解决当前区块链系统串行共识的性能问题，FISCO BCOS 3.x提出了一种两阶段并行拜占庭共识算法。

该算法将区块链系统共识划分成区块批量并行排序共识和区块执行结果流水线共识两个阶段。

区块批量并行排序共识和区块执行结果流水线共识均支持对多个区块进行并行共识，从而提升了区块链吞吐量。

**两阶段并行拜占庭共识设计可参考** `这里 <../design/consensus.html>`_

----

确定性并行合约(DMC)
>>>>>>>>>>>>>>
----


保证证并行交易执行过程中互斥资源访问的确定性，实现以下几个目标：

- **易用**：区块链底层自动启用并行，无需使用者关注并行逻辑、预先提供冲突字段。
- **高效**：区块内的交易不重复执行，没有预执行、预分析或重试的流程。
- **兼容**：无论 EVM、WASM、Precompiled 或其它合约，使用任意的共识机制，都能使用此方案。

**确定性并行合约可参考** `这里 <../design/DMC.html>`_

----

区块链文件系统
>>>>>>>>>>>>>>
----


支持所见即所得的区块链资源管理方式，对区块链的合约与数据治理更友好，详细设计请参考 `这里 <../design/contract_directory.html>`_

----

集成WeBankBlockchain Liquid和WASM虚拟机
>>>>>>>>>>>>>>
----


支持Solidity的同时，新增支持WeBankBlockchain Liquid(简称WBC-Liquid)合约，合约功能更强大。

**WBC-Liquid请参考** `这里 <https://liquid-doc.readthedocs.io/zh_CN/latest/>`_

----


统一通用的存储层
>>>>>>>>>>>>>>

存储层需要能够满足Air、Pro和Max三个版本的不同设计目标。

存储层使用同一套接口来屏蔽不同版本存储的具体实现。

Air和Pro版本FISCO BCOS的存储层使用RocksDB来满足其轻便和高性能的需求。

Max版本则通过接入能够支持水平扩展的分布式数据库支撑大规模数据存储的需求。

**存储层的设计可参考** `这里 <../design/storage.html>`_

v3.0.0-rc1
------------------

.. admonition:: FISCO BCOS 3.x Releases

     - `FISCO BCOS v3.0.0-rc1 <./3_0_0_rc1.html>`_ [`release <https://github.com/FISCO-BCOS/FISCO-BCOS/releases/tag/v3.0.0-rc1>`_]
     
     - v3.0.0-rc1不包括 ``FISCO BCOS Max`` 版本，Max版本的FISCO BCOS会在后续版本中推出

.. toctree::
   :hidden:
   :maxdepth: 0

   3_0_0_rc1.md


v3.0.0-rc2
------------------

.. admonition:: FISCO BCOS 3.x Releases

     - `FISCO BCOS v3.0.0-rc2 <./3_0_0_rc2.html>`_ [`release <https://github.com/FISCO-BCOS/FISCO-BCOS/releases/tag/v3.0.0-rc2>`_]
     
     - v3.0.0-rc2不包括 ``FISCO BCOS Max`` 版本，Max版本的FISCO BCOS会在后续版本中推出
     

.. admonition:: 查看节点和数据版本

    - 查看Air版本FISCO BCOS节点二进制版本：``./fisco-bcos --version``
    - 查看Pro版本FISCO BCOS节点二进制版本：``./BcosNodeService --version``, ``./BcosRpcService --version``, ``./BcosGatewayService --version``


.. toctree::
   :hidden:
   :maxdepth: 0

   3_0_0_rc2.md


v3.0.0-rc3
------------------

.. admonition:: FISCO BCOS 3.x Releases

     - `FISCO BCOS v3.0.0-rc3 <./3_0_0_rc3.html>`_ [`release <https://github.com/FISCO-BCOS/FISCO-BCOS/releases/tag/v3.0.0-rc3>`_]
     
     - v3.0.0-rc3不包括 ``FISCO BCOS Max`` 版本，Max版本的FISCO BCOS会在后续版本中推出
     

.. admonition:: 查看节点和数据版本

    - 查看Air版本FISCO BCOS节点二进制版本：``./fisco-bcos --version``
    - 查看Pro版本FISCO BCOS节点二进制版本：``./BcosNodeService --version``, ``./BcosRpcService --version``, ``./BcosGatewayService --version``


.. toctree::
   :hidden:
   :maxdepth: 0

   3_0_0_rc3.md

v3.0.0-rc4
------------------

.. admonition:: FISCO BCOS 3.x Releases

     - `FISCO BCOS v3.0.0-rc4 <./3_0_0_rc4.html>`_ [`release <https://github.com/FISCO-BCOS/FISCO-BCOS/releases/tag/v3.0.0-rc4>`_]
     

.. admonition:: 查看节点和数据版本

    - 查看Air版本FISCO BCOS节点二进制版本：``./fisco-bcos --version``
    - 查看Pro版本FISCO BCOS节点二进制版本：``./BcosNodeService --version``, ``./BcosRpcService --version``, ``./BcosGatewayService --version``
    - 查看Max版本FISCO BCOS节点二进制版本：``./BcosMaxNodeService --version``, ``./BcosRpcService --version``, ``./BcosGatewayService --version``, ``./BcosExecutorService --version``


.. toctree::
   :hidden:
   :maxdepth: 0

   3_0_0_rc4.md