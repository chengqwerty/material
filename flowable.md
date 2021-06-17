# 表名称解释


- ACT_RE_*: 'RE'代表repository仓库。RE开头的表一般用来放置静态资源，比如流程定义或者流程资源（图片、规则等）。

- ACT_RU_*: 'RU'代表runtime运行。是运行时表包含运行的流程实例、用户任务、variables、jobs等。为了节省存储空间和保证速度这些表只在流程运行过程中存储数据，流程结束删除数据。

- ACT_HI_*: 'HI'代表history历史。存储历史数据比如process instances, variables, tasks等。

- ACT_GE_*: general data, which is used for various use cases.


# 流程解析
## 启动流程

