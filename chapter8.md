// 创建第八章节点
MERGE (chapter8:Chapter {number: "第八章", title: "附则"})
MERGE (chapter8)-[:PART_OF]->(doc)

// 第五十五条
MERGE (art55:Article {number: "第五十五条", full_text: "本条例自 2022年 8月 1日起施行，《广东省实施〈中华人民共和国土地管理法〉办法》同时废止。"})
MERGE (art55)-[:PART_OF]->(chapter8)

// 实施日期
MERGE (implementation_date:Object {name: "实施日期", value: "2022年8月1日", source_article: "第五十五条"})

// 废止法规
MERGE (repealed_regulation:Object {name: "广东省实施《中华人民共和国土地管理法》办法", type: "regulation", status: "废止", source_article: "第五十五条"})

// 关系建立 - 第五十五条
MERGE (doc)-[:HAS_IMPLEMENTATION_DATE]->(implementation_date)
MERGE (doc)-[:REPEALS]->(repealed_regulation)

// 将主体与条款关联
MERGE (art55)-[:INVOLVES]->(doc)




// 模糊化处理
CREATE FULLTEXT INDEX authorityDescription FOR (n:Authority) ON EACH [n.description];


//索引案例
// 利用索引进行模糊匹配
CALL db.index.fulltext.queryNodes("authorityDescription", "农用地 AND 转为建设用地 AND 审批") YIELD node, score
MATCH (agent:Agent)-[:HAS_AUTHORITY]->(node)
RETURN agent.name, node.description, score
ORDER BY score DESC
LIMIT 10














// 1. 创建顶层概念节点
MERGE (c_gov:Concept {name: "政府机关", description: "各级人民政府及其派出机关"})
MERGE (c_dept:Concept {name: "主管部门", description: "负责具体专项行政管理事务的政府职能部门"})
MERGE (c_leg:Concept {name: "立法机关", description: "各级人民代表大会及其常务委员会"})

// 2. 将具体“政府机关”映射到概念
MATCH (a:Agent)
WHERE a.name IN [
    '各级人民政府', '县级以上人民政府', '上级人民政府', '上一级人民政府', '被督察的人民政府',
    '国务院', '省人民政府', '地级以上市人民政府', '县（市、区）人民政府', '县级人民政府', 
    '乡镇人民政府', '街道办事处'
]
MERGE (a)-[:BELONGS_TO_CONCEPT]->(c_gov)

// 3. 将具体“主管部门”映射到概念
MATCH (a:Agent)
WHERE a.name CONTAINS '自然资源' 
   OR a.name CONTAINS '农业农村' 
   OR a.name IN [
    '林业主管部门', '发展改革部门', '人力资源社会保障部门', '住房城乡建设部门', 
    '交通运输部门', '政务服务数据管理部门', '有关部门', '其他相关主管部门'
]
WITH a
MATCH (c_dept:Concept {name: "主管部门"})
MERGE (a)-[:BELONGS_TO_CONCEPT]->(c_dept)

// 4. 将具体“立法机关”映射到概念
MATCH (a:Agent)
WHERE a.name CONTAINS '人民代表大会' OR a.name = '常务委员会'
WITH a
MATCH (c_leg:Concept {name: "立法机关"})
MERGE (a)-[:BELONGS_TO_CONCEPT]->(c_leg)


MATCH (all:Agent {name: "各级人民政府"})
MATCH (above_county:Agent {name: "县级以上人民政府"})
MATCH (county:Agent {name: "县级人民政府"})
MATCH (city:Agent {name: "地级以上市人民政府"})

// 建立层级包含关系
MERGE (all)-[:INCLUDES_LEVEL]->(above_county)
MERGE (all)-[:INCLUDES_LEVEL]->(county)
MERGE (all)-[:INCLUDES_LEVEL]->(city)
MERGE (above_county)-[:INCLUDES_LEVEL]->(county)
MERGE (above_county)-[:INCLUDES_LEVEL]->(city)