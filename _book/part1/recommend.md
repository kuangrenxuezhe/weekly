### 推荐架构

---

#### exp

```mermaid
sequenceDiagram
    exp->>rcm: 请求自然推荐 + 实验信息
    rcm->>exp: 返回自然推荐结果
    exp->>商投: 请求商投 + 实验信息
    商投->>exp: 返回商投推荐结果
    exp->>置顶&投放: 请求置顶&投放数据
    置顶&投放->>exp: 返回置顶&投放数据
    exp->>包装服务: 请求包装服务
    包装服务->>exp: 返回包装结果
```

---

#### rcm
```mermaid
sequenceDiagram
rcm->>画像: 请求画像服务 
画像->>rcm: 返回用户画像 
rcm->>倒排索引: 请求召回数据 
rcm->>召回服务: 请求召回服务
召回服务->>rcm: 返回召回结果 
rcm->>向量服务: 请求embedding
向量服务->>rcm: 返回embedding数据
倒排索引->>rcm: 返回召回数据
rcm->>排序服务: 请求排序数据
排序服务->>rcm: 返回排序数据
rcm->>正排服务:  请求正排数据
正排服务->>rcm: 返回正排数据
```

#### 商投
```mermaid
sequenceDiagram
商投->>倒排索引: 请求召回数据
商投->>召回服务: 请求召回服务
召回服务->>商投: 返回召回结果 
商投->>向量服务: 请求embedding
向量服务->>商投: 返回embedding数据
倒排索引->>商投: 返回召回数据
```





```mermaid
gantt
        dateFormat  YYYY-MM-DD
        title Adding GANTT diagram functionality to mermaid

        section A section
        Completed task            :done,    des1, 2014-01-06,2014-01-08
        Active task               :active,  des2, 2014-01-09, 3d
        Future task               :         des3, after des2, 5d
        Future task2               :         des4, after des3, 5d

        section Critical tasks
        Completed task in the critical line :crit, done, 2014-01-06,24h
        Implement parser and jison          :crit, done, after des1, 2d
        Create tests for parser             :crit, active, 3d
        Future task in critical line        :crit, 5d
        Create tests for renderer           :2d
        Add to mermaid                      :1d

        section Documentation
        Describe gantt syntax               :active, a1, after des1, 3d
        Add gantt diagram to demo page      :after a1  , 20h
        Add another diagram to demo page    :doc1, after a1  , 48h

        section Last section
        Describe gantt syntax               :after doc1, 3d
        Add gantt diagram to demo page      : 20h
        Add another diagram to demo page    : 48h
```

```mermaid
sequenceDiagram
    participant z as 张三
    participant l as 李四
    loop 日复一日
        z->>l: 吃了吗您呐？
        l-->>z: 吃了，您呢？
        activate z
        Note left of z: 想了一下
        alt 还没吃
            z-xl: 还没呢，正准备回去吃
        else 已经吃了
            z-xl: 我也吃过了，哈哈
        end
        opt 大过年的
            l-->z: 祝您新年好啊
        end
    end
```

---
#### 开发流程及问题

1. 收集频道页信息
1. 推荐引擎接入新频道或已有频道
1. DMS接入新频道页
1. 研发自测、联调、性能测试
1. QA测试
1. 当前问题
##### 一、收集频道页信息
1. 文档类信息：产品文档、接口文档、统一接口文档
1. 工程信息：线上代码分支，线上编译环境
1. api信息：线上历史接口，线上summary接口
##### 二、推荐引擎接入新频道或已有频道，引擎配置及输入输出参数（0.5天）
1. 配置PID相应的用户画像信息（APP端、M端）、用户曝光信息
1. 配置PID相应的flag信息
1. 输入输出特殊参数开发
1. exp配置PID路由信息
1. 引擎合一接口文档、测试文档、问题文档补充编写
##### 三、DMS接入新频道页
##### 四、召回模块开发
1. 召回模块从现有模块迁移到dms召回
##### 五、研发自测、联调、性能测试、
1. 基于收集到的信息进行联调、测试，以及压测
##### 六、QA测试
1. 测试环境部署
1. 测试环境压测
##### 七、当前问题
1. 信息不足，部分频道页没有完善的文档
2. 人力不足，信息收集、引擎配置、研发（周成冲、张军生），召回（袁可柔），DMS（赵广），部分人员还涉及其他项目
3. 自测不足，自测、联调、压测不足，压测、预发环境不统一
4. 效率较低，联调过程中问题解决比较慢，缺少人力支持
5. 测试配置测试环境准备不足，耗时较久，已积累文档并固定测试资源减少沟通成本
6. QA资源不足，从提测到测试需要1-2天
---
#### 排期计划

