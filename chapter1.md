// 创建唯一约束，防止重复节点
CREATE CONSTRAINT IF NOT EXISTS FOR (d:Document) REQUIRE d.name IS UNIQUE;
CREATE CONSTRAINT IF NOT EXISTS FOR (c:Chapter) REQUIRE c.number IS UNIQUE;
CREATE CONSTRAINT IF NOT EXISTS FOR (a:Article) REQUIRE a.number IS UNIQUE;
CREATE CONSTRAINT IF NOT EXISTS FOR (ag:Agent) REQUIRE ag.name IS UNIQUE;
CREATE CONSTRAINT IF NOT EXISTS FOR (o:Obligation) REQUIRE o.description IS UNIQUE;
CREATE CONSTRAINT IF NOT EXISTS FOR (p:Purpose) REQUIRE p.description IS UNIQUE;
CREATE CONSTRAINT IF NOT EXISTS FOR (pr:Principle) REQUIRE pr.name IS UNIQUE;
CREATE CONSTRAINT IF NOT EXISTS FOR (g:Goal) REQUIRE g.description IS UNIQUE;
CREATE CONSTRAINT IF NOT EXISTS FOR (au:Authority) REQUIRE au.description IS UNIQUE;
CREATE CONSTRAINT IF NOT EXISTS FOR (p:Penalty) REQUIRE p.description IS UNIQUE;
CREATE CONSTRAINT IF NOT EXISTS FOR (s:System) REQUIRE s.name IS UNIQUE;
CREATE CONSTRAINT IF NOT EXISTS FOR (obj:Object) REQUIRE obj.name IS UNIQUE;


// 创建文档节点
MERGE (doc:Document {name: "广东省土地管理条例", promulgation_date: "2022年6月1日", implementation_date: "2022年8月1日", legislative_body: "广东省第十三届人民代表大会常务委员会第四十三次会议"})

// 创建第一章节点
MERGE (chapter1:Chapter {number: "第一章", title: "第一章 总则"})
MERGE (chapter1)-[:PART_OF]->(doc)

// 第一条
MERGE (art1:Article {number: "第一条", full_text: "为了加强土地管理，保护、开发土地资源，合理利用土地，落实最严格的耕地保护制度，促进社会经济的可持续发展，根据《中华人民共和国土地管理法》《中华人民共和国土地管理法实施条例》等法律、行政法规，结合本省实际，制定本条例。"})
MERGE (art1)-[:PART_OF]->(chapter1)

MERGE (purpose1:Purpose {description: "加强土地管理"})
MERGE (purpose2:Purpose {description: "保护土地资源"})
MERGE (purpose3:Purpose {description: "开发土地资源"})
MERGE (purpose4:Purpose {description: "合理利用土地"})
MERGE (purpose5:Purpose {description: "落实最严格的耕地保护制度"})
MERGE (purpose6:Purpose {description: "促进社会经济的可持续发展"})

MERGE (art1)-[:HAS_PURPOSE]->(purpose1)
MERGE (art1)-[:HAS_PURPOSE]->(purpose2)
MERGE (art1)-[:HAS_PURPOSE]->(purpose3)
MERGE (art1)-[:HAS_PURPOSE]->(purpose4)
MERGE (art1)-[:HAS_PURPOSE]->(purpose5)
MERGE (art1)-[:HAS_PURPOSE]->(purpose6)

// 引用的法律法规
MERGE (law1:Document {name: "中华人民共和国土地管理法", type: "national_law"})
MERGE (law2:Document {name: "中华人民共和国土地管理法实施条例", type: "administrative_regulation"})

MERGE (art1)-[:CITES]->(law1)
MERGE (art1)-[:CITES]->(law2)

// 第二条
MERGE (art2:Article {number: "第二条", full_text: "各级人民政府应当加强对土地管理工作的领导，坚持生态优先、绿色发展、全面规划、严格管理，优化土地资源配置，推动节约集约用地，提升用地效率，制止非法占用土地和破坏土地资源的行为。街道办事处在本辖区内办理派出它的人民政府交办的土地管理相关工作。"})
MERGE (art2)-[:PART_OF]->(chapter1)

MERGE (agent1:Agent {name: "各级人民政府", type: "government_level"})
MERGE (agent2:Agent {name: "街道办事处", type: "organization", function: "办理派出它的人民政府交办的土地管理相关工作"})

MERGE (principle1:Principle {name: "生态优先",source_article:"第二条"})
MERGE (principle2:Principle {name: "绿色发展",source_article:"第二条"})
MERGE (principle3:Principle {name: "全面规划",source_article:"第二条"})
MERGE (principle4:Principle {name: "严格管理",source_article:"第二条"})

MERGE (goal1:Goal {description: "优化土地资源配置",source_article:"第二条"})
MERGE (goal2:Goal {description: "推动节约集约用地",source_article:"第二条"})
MERGE (goal3:Goal {description: "提升用地效率",source_article:"第二条"})
MERGE (goal4:Goal {description: "制止非法占用土地",source_article:"第二条"})
MERGE (goal5:Goal {description: "制止破坏土地资源的行为",source_article:"第二条"})

// 各级人民政府的职责和遵循的原则
MERGE (agent1)-[:HAS_DUTY]->(duty1:Obligation {description: "加强对土地管理工作的领导",source_article:"第二条"})
MERGE (agent1)-[:FOLLOWS_PRINCIPLE]->(principle1)
MERGE (agent1)-[:FOLLOWS_PRINCIPLE]->(principle2)
MERGE (agent1)-[:FOLLOWS_PRINCIPLE]->(principle3)
MERGE (agent1)-[:FOLLOWS_PRINCIPLE]->(principle4)
MERGE (agent1)-[:HAS_GOAL]->(goal1)
MERGE (agent1)-[:HAS_GOAL]->(goal2)
MERGE (agent1)-[:HAS_GOAL]->(goal3)
MERGE (agent1)-[:HAS_GOAL]->(goal4)
MERGE (agent1)-[:HAS_GOAL]->(goal5)

// 街道办事处的职责
MERGE (agent2)-[:HAS_DUTY]->(duty2:Obligation {description: "在本辖区内办理派出它的人民政府交办的土地管理相关工作",source_article:"第二条"})

// 将主体与条例关联
MERGE (art2)-[:INVOLVES]->(agent1)
MERGE (art2)-[:INVOLVES]->(agent2)

// 第三条
MERGE (art3:Article {number: "第三条", full_text: "县级以上人民政府自然资源主管部门负责土地管理和监督工作。县级以上人民政府农业农村主管部门负责农村宅基地改革和管理相关工作，做好耕地质量管理相关工作；林业主管部门负责林地管理相关工作。其他有关部门按照各自职责，共同做好土地管理相关工作。"})
MERGE (art3)-[:PART_OF]->(chapter1)

// 各部门及其职责
MERGE (dept1:Agent {name: "县级以上人民政府自然资源主管部门", type: "department"})
MERGE (dept2:Agent {name: "县级以上人民政府农业农村主管部门", type: "department"})
MERGE (dept3:Agent {name: "林业主管部门", type: "department"})
MERGE (dept4:Agent {name: "其他有关部门", type: "department"})

MERGE (dept1)-[:HAS_DUTY]->(duty3:Obligation {description: "负责土地管理和监督工作",source_article:"第三条"})
MERGE (dept2)-[:HAS_DUTY]->(duty4:Obligation {description: "负责农村宅基地改革和管理相关工作",source_article:"第三条"})
MERGE (dept2)-[:HAS_DUTY]->(duty5:Obligation {description: "做好耕地质量管理相关工作",source_article:"第三条"})
MERGE (dept3)-[:HAS_DUTY]->(duty6:Obligation {description: "负责林地管理相关工作",source_article:"第三条"})
MERGE (dept4)-[:HAS_DUTY]->(duty7:Obligation {description: "按照各自职责，共同做好土地管理相关工作",source_article:"第三条"})

// 将部门与条例关联
MERGE (art3)-[:INVOLVES]->(dept1)
MERGE (art3)-[:INVOLVES]->(dept2)
MERGE (art3)-[:INVOLVES]->(dept3)
MERGE (art3)-[:INVOLVES]->(dept4)

// 第四条
MERGE (art4:Article {number: "第四条", full_text: "县级以上人民政府及自然资源主管部门应当加强土地管理信息化建设，落实经费保障，按照数字政府集约化建设要求，建立统一的国土空间基础信息平台，支撑国土空间规划、耕地保护、土地开发利用、不动产登记、土地调查、生态保护修复、执法监督等事项的信息化管理，对土地利用状况和管理情况进行动态监测。自然资源、发展改革、人力资源社会保障、住房城乡建设、交通运输、农业农村、政务服务数据管理等有关部门应当建立土地管理信息共享机制，实现土地管理数据共享和业务协同，依法公开土地管理信息。"})
MERGE (art4)-[:PART_OF]->(chapter1)

MERGE (agent3:Agent {name: "县级以上人民政府", type: "government_level"})
MERGE (agent4:Agent {name: "县级以上人民政府自然资源主管部门", type: "department"})
MERGE (agent5:Agent {name: "自然资源主管部门", type: "department"})
MERGE (agent6:Agent {name: "发展改革部门", type: "department"})
MERGE (agent7:Agent {name: "人力资源社会保障部门", type: "department"})
MERGE (agent8:Agent {name: "住房城乡建设部门", type: "department"})
MERGE (agent9:Agent {name: "交通运输部门", type: "department"})
MERGE (agent10:Agent {name: "农业农村部门", type: "department"})
MERGE (agent11:Agent {name: "政务服务数据管理部门", type: "department"})

MERGE (agent3)-[:HAS_DUTY]->(duty8:Obligation {description: "加强土地管理信息化建设",source_article:"第四条"})
MERGE (agent3)-[:HAS_DUTY]->(duty9:Obligation {description: "落实经费保障",source_article:"第四条"})
MERGE (agent4)-[:HAS_DUTY]->(duty10:Obligation {description: "建立统一的国土空间基础信息平台",source_article:"第四条"})
MERGE (agent4)-[:HAS_DUTY]->(duty11:Obligation {description: "对土地利用状况和管理情况进行动态监测",source_article:"第四条"})

MERGE (platform:Object {name: "国土空间基础信息平台", purpose: "支撑国土空间规划、耕地保护、土地开发利用、不动产登记、土地调查、生态保护修复、执法监督等事项的信息化管理",source_article:"第四条"})

MERGE (duty10)-[:USES]->(platform)

// 信息共享机制
MERGE (mechanism:Object {name: "土地管理信息共享机制", purpose: "实现土地管理数据共享和业务协同，依法公开土地管理信息"})

MERGE (agent5)-[:PARTICIPATES_IN]->(mechanism)
MERGE (agent6)-[:PARTICIPATES_IN]->(mechanism)
MERGE (agent7)-[:PARTICIPATES_IN]->(mechanism)
MERGE (agent8)-[:PARTICIPATES_IN]->(mechanism)
MERGE (agent9)-[:PARTICIPATES_IN]->(mechanism)
MERGE (agent10)-[:PARTICIPATES_IN]->(mechanism)
MERGE (agent11)-[:PARTICIPATES_IN]->(mechanism)

// 将主体与条例关联
MERGE (art4)-[:INVOLVES]->(agent3)
MERGE (art4)-[:INVOLVES]->(agent4)
MERGE (art4)-[:INVOLVES]->(agent5)
MERGE (art4)-[:INVOLVES]->(agent6)
MERGE (art4)-[:INVOLVES]->(agent7)
MERGE (art4)-[:INVOLVES]->(agent8)
MERGE (art4)-[:INVOLVES]->(agent9)
MERGE (art4)-[:INVOLVES]->(agent10)
MERGE (art4)-[:INVOLVES]->(agent11)

// 第五条
MERGE (art5:Article {number: "第五条", full_text: "任何单位和个人都有遵守土地管理法律、法规的义务，不得侵占、买卖或者以其他形式非法转让土地，不得非法占用土地。"})
MERGE (art5)-[:PART_OF]->(chapter1)

MERGE (agent12:Agent {name: "任何单位", type: "entity"})
MERGE (agent13:Agent {name: "任何个人", type: "person"})

MERGE (agent12)-[:HAS_DUTY]->(duty12:Obligation {description: "遵守土地管理法律、法规",source_article:"第五条"})
MERGE (agent13)-[:HAS_DUTY]->(duty12)

MERGE (agent12)-[:PROHIBITED_FROM]->(prohibition1:Prohibition {description: "侵占土地",source_article:"第五条"})
MERGE (agent12)-[:PROHIBITED_FROM]->(prohibition2:Prohibition {description: "买卖土地",source_article:"第五条"})
MERGE (agent12)-[:PROHIBITED_FROM]->(prohibition3:Prohibition {description: "以其他形式非法转让土地",source_article:"第五条"})
MERGE (agent12)-[:PROHIBITED_FROM]->(prohibition4:Prohibition {description: "非法占用土地",source_article:"第五条"})

MERGE (agent13)-[:PROHIBITED_FROM]->(prohibition1)
MERGE (agent13)-[:PROHIBITED_FROM]->(prohibition2)
MERGE (agent13)-[:PROHIBITED_FROM]->(prohibition3)
MERGE (agent13)-[:PROHIBITED_FROM]->(prohibition4)

// 将主体与条例关联
MERGE (art5)-[:INVOLVES]->(agent12)
MERGE (art5)-[:INVOLVES]->(agent13)