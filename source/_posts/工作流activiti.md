---
title: 工作流activiti
date: 2020-09-24 17:31:42
categories: 工作流
tags: activiti
---

### 工作流activit

工作流(Workflow)，就是通过计算机对业务流程自动化执行管理。Activiti 是一个工作流引擎， activiti 可以将业务系统中复杂的业务流程抽取出来，使用专门的 建模语言（BPMN2.0）进行定义，业务系统按照预先定义的流程进行执行，实现了业务系统的业务 流程由 activiti进行管理，减少业务系统由于流程变更进行系统升级改造的工作量，从而提高系统的 健壮性，同时也减少了系统开发维护成本。 

<!--more-->

##### 1，ProcessEngine 

一般创建方式:

```java
// 创建processEngineConfiguration 
ProcessEngineConfiguration configuration = ProcessEngineConfiguration;  .createProcessEngineConfigurationFromResource("activiti.cfg.xml") 
//通过ProcessEngineConfiguration创建ProcessEngine   
    ProcessEngine processEngine =  processEngineConfiguration.buildProcessEngine();
```

 简单创建方式 :

```java
//使用classpath下的activiti.cfg.xml中的配置创建processEngine   
ProcessEngine processEngine = ProcessEngines.getDefaultProcessEngine();   
System.out.println(processEngine); 
```

##### 2, Service

工作流中的Service 的创建

```java
//在上文中创建了processEngine
RuntimeService runtimeService = processEngine.getRuntimeService();
RepositoryService repositoryService = processEngine.getRepositoryService();
TaskService taskService = processEngine.getTaskService();

```

常用Service以及功能：

2.1RepositoryService 

RepositoryService 是 activiti 的资源管理类，提供了管理和控制流程发布包和流程定义的操作。使用工作流建模工 具设计的业务流程图需要使用此 service 将流程定义文件的内容部署到计算机。 除了部署流程定义以外还可以： 查询引擎中的发布包和流程定义。 暂停或激活发布包，对应全部和特定流程定义。 暂停意味着它们不能再执行任何操作了，激活 是对应的反向操作。 获得多种资源，像是包含在发布包里的文件， 或引擎自动生成的流程图。 获得流程定义的 pojo 版本， 可以用来通过 java 解析流程，而不必通过 xml。

 2.2 RuntimeService 

RuntimeService 是 activiti 的流程运行管理类。可以从这个服务类中获取很多关于流程执行相关的信息 

2.3 TaskService 

TaskService 是 activiti 的任务管理类。可以从这个类中获取任务的信息。

 2.4 HistoryService 

HistoryService 是 activiti 的历史管理类，可以查询历史信息，执行流程时，引擎会保存很多数据（根据配置），比 如流程实例启动时间，任务的参与者， 完成任务的时间，每个流程实例的执行路径，等等。 这个 服务主要通过查询功能来获得这些数据。

 2.5 ManagementService 

ManagementService 是 activiti 的引擎管理类，提供了对 Activiti 流程引擎的管理和维护功能，这些功能不在工作流驱动 的应用程序中使用，主要用于 Activiti 系统的日常维护。



##### 3. 工作流数据库

1. 资源库流程规则表
   1. act_re_deployment 部署信息表
   2. act_re_model 流程设计模型部署表
   3. act_re_procdef 流程定义数据表
2. 运行时数据库表
   1. act_ru_execution 运行时流程执行实例表
   2. act_ru_identitylink 运行时流程人员表，主要存储任务节点与参与者的相关信息
   3. act_ru_task 运行时任务节点表
   4. act_ru_variable 运行时流程变量数据表
3. 历史数据库表
   1. act_hi_actinst 历史节点表
   2. act_hi_attachment 历史附件表
   3. act_hi_comment 历史意见表
   4. act_hi_identitylink 历史流程人员表
   5. act_hi_detail 历史详情表，提供历史变量的查询
   6. act_hi_procinst 历史流程实例表
   7. act_hi_taskinst 历史任务实例表
   8. act_hi_varinst 历史变量表
4. 组织机构表
   1. act_id_group 用户组信息表
   2. act_id_info 用户扩展信息表
   3. act_id_membership 用户与用户组对应信息表
   4. act_id_user 用户信息表

1. 通用数据表
   1. act_ge_bytearray 二进制数据表
   2. act_ge_property 属性数据表存储整个流程引擎级别的数据,初始化表结构时，会默认插入三条记录，



