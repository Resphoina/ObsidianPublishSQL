---
{"dg-publish":true,"permalink":"/8-000/8-002/field-assemblies-system/","dgHomeLink":true,"dgPassFrontmatter":false}
---


# <font color=#DC143C>(FIELD ASSEMBLIES)</font>
URL:: 

```
dataview
table without id 入榜亮点, 入榜输出
where contains(TITLES, "")
```

```dataview
table without id 萃取重点, 萃取难点, 萃取锚点, 萃取输出
where contains(TITLES, "FIELD ASSEMBLIES SYSTEM")
```

## 大表修改表结构操作规范
1. 停止数据更新并新建一张表
2. 数据导入至新表
3. 建立索引
4. 与原表表名互换
5. 核对数据无异常
6. 恢复数据更新
7. 观察至少1天确认无问题后，删除原表或迁移原表数据到TEMP库(备份)

## 大表数据更新缓慢解决方案
1. `NOT EXISTS`找出原表数据没有更新的部分，写入新表
2. 过程中计算生成或拉取生产的更新数据`INSERT INTO`上一步骤的新表
3. 检查新表的数据量是否异常
4. 新表建立索引
5. 与原表表名互换
6. 更新过程下次执行时删除互换的旧表

## 项目实施过程
1. 业务需求调研
2. 数据清理
3. 指标体系梳理
4. 数据模型构建

## 数据库删库视图引用检查
### 20220730版本
+ 1——主操作库`ODSDBXXX`和`ODSDBFQXXX`，右键选择→任务→生成脚本→导出视图
+ 2——检查具体哪些视图包含目标库数据表
+ 3——逐个修改视图
+ 4——上下游检查过程脚本引用情况进行修改(在线文档公告)
+ 5——再次导出视图检查确认步骤[1]修改
+ 6——执行更新上下游关系表检查确认步骤[4]修改











NULL
```SQL
月度经营分析
月度绩效考核
年度关键考核指标
日常管理分析
```