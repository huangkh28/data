// 第三章
// 创建第三章节点（确保文档节点已存在）
MATCH (doc:Document {name: "广东省土地管理条例"})
MERGE (chapter3:Chapter {number: "第三章", title: "耕地保护"})
MERGE (chapter3)-[:PART_OF]->(doc)

// 第十四条
MERGE (art14:Article {number: "第十四条", full_text: "各级人民政府对本行政区域耕地保护负总责，其主要负责人为第一责任人。县级以上人民政府应当每年对下一级人民政府耕地保护责任目标落实情况进行考核。各级人民政府应当严格执行国土空间规划和土地利用年度计划，严格控制耕地转为非耕地，有计划地组织开发补充耕地，引导各类建设项目不占或者少占耕地，采取措施保护和提升耕地质量。耕地总量减少或者质量降低的，由上级人民政府责令在规定期限内组织开垦或者整治。新开垦和整治的耕地按照国家和省有关规定进行验收。"})
MERGE (art14)-[:PART_OF]->(chapter3)

// 责任主体
MERGE (agent1:Agent {name: "各级人民政府", type: "government_level"})
MERGE (agent2:Agent {name: "县级以上人民政府", type: "government_level"})
MERGE (agent3:Agent {name: "上级人民政府", type: "government_level"})
MERGE (agent4:Agent {name: "主要负责人", type: "position"})

// 耕地保护原则
MERGE (principle1:Principle {name: "政府负总责原则", source_article: "第十四条"})
MERGE (principle2:Principle {name: "第一责任人制度", source_article: "第十四条"})
MERGE (principle3:Principle {name: "严格控制耕地转为非耕地原则", source_article: "第十四条"})

// 耕地保护义务
MERGE (duty1:Obligation {description: "对本行政区域耕地保护负总责", source_article: "第十四条"})
MERGE (duty2:Obligation {description: "每年对下一级人民政府耕地保护责任目标落实情况进行考核", source_article: "第十四条"})
MERGE (duty3:Obligation {description: "严格执行国土空间规划和土地利用年度计划", source_article: "第十四条"})
MERGE (duty4:Obligation {description: "严格控制耕地转为非耕地", source_article: "第十四条"})
MERGE (duty5:Obligation {description: "有计划地组织开发补充耕地", source_article: "第十四条"})
MERGE (duty6:Obligation {description: "引导各类建设项目不占或者少占耕地", source_article: "第十四条"})
MERGE (duty7:Obligation {description: "采取措施保护和提升耕地质量", source_article: "第十四条"})
MERGE (duty8:Obligation {description: "在规定期限内组织开垦或者整治减少或质量降低的耕地", source_article: "第十四条"})

// 耕地补充机制
MERGE (mechanism1:Object {name: "耕地补充机制", type: "mechanism", source_article: "第十四条"})
MERGE (procedure1:Procedure {name: "新开垦和整治耕地验收程序", steps: "按照国家和省有关规定进行验收", source_article: "第十四条"})

// 关系建立
MERGE (agent1)-[:FOLLOWS_PRINCIPLE]->(principle1)
MERGE (agent1)-[:FOLLOWS_PRINCIPLE]->(principle3)
MERGE (agent4)-[:FOLLOWS_PRINCIPLE]->(principle2)

MERGE (agent1)-[:HAS_DUTY]->(duty1)
MERGE (agent1)-[:HAS_DUTY]->(duty3)
MERGE (agent1)-[:HAS_DUTY]->(duty4)
MERGE (agent1)-[:HAS_DUTY]->(duty5)
MERGE (agent1)-[:HAS_DUTY]->(duty6)
MERGE (agent1)-[:HAS_DUTY]->(duty7)

MERGE (agent2)-[:HAS_DUTY]->(duty2)
MERGE (agent3)-[:HAS_DUTY]->(duty8)

MERGE (duty5)-[:USES_MECHANISM]->(mechanism1)
MERGE (mechanism1)-[:FOLLOWS_PROCEDURE]->(procedure1)

MERGE (art14)-[:ESTABLISHES_PRINCIPLE]->(principle1)
MERGE (art14)-[:ESTABLISHES_PRINCIPLE]->(principle2)
MERGE (art14)-[:ESTABLISHES_PRINCIPLE]->(principle3)
MERGE (art14)-[:INVOLVES]->(agent1)
MERGE (art14)-[:INVOLVES]->(agent2)
MERGE (art14)-[:INVOLVES]->(agent3)
MERGE (art14)-[:INVOLVES]->(agent4)

// 第十五条
MERGE (art15:Article {number: "第十五条", full_text: "县级以上人民政府应当根据国土空间总体规划确定的永久基本农田保护任务，划定永久基本农田并落实保护责任，确保本行政区域永久基本农田数量不减少、质量不降低、布局总体稳定。地级以上市人民政府划定的永久基本农田一般应当占本行政区域耕地总面积的百分之八十以上。具体比例由省人民政府根据省国土空间总体规划和地级以上市耕地实际情况作出规定。地级以上市和县级人民政府应当将永久基本农田范围以外一定数量的优质耕地划入永久基本农田储备区，作为补划永久基本农田的后备资源。"})
MERGE (art15)-[:PART_OF]->(chapter3)

// 耕地保护概念
MERGE (concept1:Object {name: "永久基本农田"})
MERGE (concept2:Object {name: "永久基本农田储备区", type: "farmland_type"})

// 比例要求
MERGE (requirement1:Object {name: "永久基本农田比例要求", value: "百分之八十以上", source_article: "第十五条"})

// 耕地保护义务
MERGE (duty9:Obligation {description: "划定永久基本农田并落实保护责任", source_article: "第十五条"})
MERGE (duty10:Obligation {description: "确保永久基本农田数量不减少、质量不降低、布局总体稳定", source_article: "第十五条"})
MERGE (duty11:Obligation {description: "将永久基本农田范围以外一定数量的优质耕地划入永久基本农田储备区", source_article: "第十五条"})

// 关系建立
MERGE (agent2)-[:HAS_DUTY]->(duty9)
MERGE (agent2)-[:HAS_DUTY]->(duty10)

MERGE (duty9)-[:DEFINES]->(concept1)
MERGE (duty11)-[:DEFINES]->(concept2)

MERGE (concept1)-[:HAS_REQUIREMENT]->(requirement1)

MERGE (art15)-[:DEFINES_CONCEPT]->(concept1)
MERGE (art15)-[:DEFINES_CONCEPT]->(concept2)
MERGE (art15)-[:INVOLVES]->(agent2)

// 第十六条
MERGE (art16:Article {number: "第十六条", full_text: "本省依法实行占用耕地补偿制度。非农业建设经依法批准占用耕地的，由占用耕地的单位按照国家和省有关规定，负责开垦与所占用耕地的数量和质量相当的耕地；没有条件开垦或者开垦的耕地不符合要求的，应当按照国家规定缴纳耕地开垦费并用于开垦新的耕地，或者通过调剂使用补充耕地指标的方式落实耕地占补平衡。耕地开垦费、补充耕地指标调剂的相关费用，应当作为建设用地成本列入建设项目总投资，并及时足额缴纳或者兑付。地级以上市、县级人民政府应当加强补充耕地项目后期种植管护，按照规定保障后期管护费用。县级人民政府应当制定补充耕地项目后期管护实施方案，明确后期种植管护职责、措施、标准、期限等要求，落实乡镇村以及土地承包经营者的责任。"})
MERGE (art16)-[:PART_OF]->(chapter3)

// 耕地补偿制度
MERGE (system1:Object {name: "占用耕地补偿制度", type: "system", source_article: "第十六条"})
MERGE (concept3:Object {name: "耕地占补平衡", type: "concept", source_article: "第十六条"})

// 补偿方式
MERGE (method1:Object {name: "开垦相当数量和质量的耕地", type: "compensation_method", source_article: "第十六条"})
MERGE (method2:Object {name: "缴纳耕地开垦费", type: "compensation_method", source_article: "第十六条"})
MERGE (method3:Object {name: "调剂使用补充耕地指标", type: "compensation_method", source_article: "第十六条"})

// 责任主体
MERGE (agent5:Agent {name: "占用耕地的单位", type: "entity"})
MERGE (agent6:Agent {name: "地级以上市、县级人民政府", type: "government_level"})
MERGE (agent7:Agent {name: "县级人民政府", type: "government_level"})

// 管护要求
MERGE (duty12:Obligation {description: "负责开垦与所占用耕地的数量和质量相当的耕地", source_article: "第十六条"})
MERGE (duty13:Obligation {description: "缴纳耕地开垦费并用于开垦新的耕地", source_article: "第十六条"})
MERGE (duty14:Obligation {description: "将耕地开垦费作为建设用地成本列入建设项目总投资", source_article: "第十六条"})
MERGE (duty15:Obligation {description: "及时足额缴纳或者兑付相关费用", source_article: "第十六条"})
MERGE (duty16:Obligation {description: "加强补充耕地项目后期种植管护", source_article: "第十六条"})
MERGE (duty17:Obligation {description: "保障后期管护费用", source_article: "第十六条"})
MERGE (duty18:Obligation {description: "制定补充耕地项目后期管护实施方案", source_article: "第十六条"})
MERGE (duty19:Obligation {description: "明确后期种植管护职责、措施、标准、期限等要求", source_article: "第十六条"})
MERGE (duty20:Obligation {description: "落实乡镇村以及土地承包经营者的责任", source_article: "第十六条"})

// 关系建立
MERGE (art16)-[:ESTABLISHES_SYSTEM]->(system1)
MERGE (system1)-[:HAS_METHOD]->(method1)
MERGE (system1)-[:HAS_METHOD]->(method2)
MERGE (system1)-[:HAS_METHOD]->(method3)
MERGE (system1)-[:AIMS_FOR]->(concept3)

MERGE (agent5)-[:HAS_DUTY]->(duty12)
MERGE (agent5)-[:HAS_DUTY]->(duty13)
MERGE (agent5)-[:HAS_DUTY]->(duty14)
MERGE (agent5)-[:HAS_DUTY]->(duty15)

MERGE (agent6)-[:HAS_DUTY]->(duty16)
MERGE (agent6)-[:HAS_DUTY]->(duty17)

MERGE (agent7)-[:HAS_DUTY]->(duty18)
MERGE (agent7)-[:HAS_DUTY]->(duty19)
MERGE (agent7)-[:HAS_DUTY]->(duty20)

MERGE (art16)-[:INVOLVES]->(agent5)
MERGE (art16)-[:INVOLVES]->(agent6)
MERGE (art16)-[:INVOLVES]->(agent7)

// 第十七条
MERGE (art17:Article {number: "第十七条", full_text: "各级人民政府应当采取措施防止和纠正耕地非农化、非粮化和长期撂荒，加强高标准农田建设，提升耕地质量，保证其用途、质量和产能。各级人民政府应当建立耕地保护奖励机制，对耕地保护成绩显著的单位和个人予以奖励。"})
MERGE (art17)-[:PART_OF]->(chapter3)

// 耕地保护目标
MERGE (goal1:Goal {description: "防止和纠正耕地非农化", source_article: "第十七条"})
MERGE (goal2:Goal {description: "防止和纠正耕地非粮化", source_article: "第十七条"})
MERGE (goal3:Goal {description: "防止和纠正耕地长期撂荒", source_article: "第十七条"})
MERGE (goal4:Goal {description: "加强高标准农田建设", source_article: "第十七条"})
MERGE (goal5:Goal {description: "提升耕地质量，保证其用途、质量和产能", source_article: "第十七条"})

// 奖励机制
MERGE (mechanism2:Object {name: "耕地保护奖励机制", type: "mechanism", source_article: "第十七条"})

// 奖励对象
MERGE (agent8:Agent {name: "耕地保护成绩显著的单位", type: "entity"})
MERGE (agent9:Agent {name: "耕地保护成绩显著的个人", type: "person"})

// 耕地保护义务
MERGE (duty21:Obligation {description: "采取措施防止和纠正耕地非农化、非粮化和长期撂荒", source_article: "第十七条"})
MERGE (duty22:Obligation {description: "加强高标准农田建设", source_article: "第十七条"})
MERGE (duty23:Obligation {description: "提升耕地质量，保证其用途、质量和产能", source_article: "第十七条"})
MERGE (duty24:Obligation {description: "建立耕地保护奖励机制", source_article: "第十七条"})
MERGE (duty25:Obligation {description: "对耕地保护成绩显著的单位和个人予以奖励", source_article: "第十七条"})

// 关系建立
MERGE (agent1)-[:HAS_DUTY]->(duty21)
MERGE (agent1)-[:HAS_DUTY]->(duty22)
MERGE (agent1)-[:HAS_DUTY]->(duty23)
MERGE (agent1)-[:HAS_DUTY]->(duty24)
MERGE (agent1)-[:HAS_DUTY]->(duty25)

MERGE (duty21)-[:ACHIEVES_GOAL]->(goal1)
MERGE (duty21)-[:ACHIEVES_GOAL]->(goal2)
MERGE (duty21)-[:ACHIEVES_GOAL]->(goal3)
MERGE (duty22)-[:ACHIEVES_GOAL]->(goal4)
MERGE (duty23)-[:ACHIEVES_GOAL]->(goal5)

MERGE (duty24)-[:ESTABLISHES_MECHANISM]->(mechanism2)
MERGE (mechanism2)-[:REWARDS]->(agent8)
MERGE (mechanism2)-[:REWARDS]->(agent9)

MERGE (art17)-[:INVOLVES]->(agent1)
MERGE (art17)-[:INVOLVES]->(agent8)
MERGE (art17)-[:INVOLVES]->(agent9)

// 第十八条
MERGE (art18:Article {number: "第十八条", full_text: "农业生产中直接用于作物种植和畜禽水产养殖的设施农业用地，应当严格执行国家和省规定的用地范围和规模标准，按照规定备案，并将用地信息上传至设施农业用地监管系统。设施农业用地应当不占或者少占耕地。确需占用耕地的，应当采取措施防止破坏耕地耕作层；不再使用的，应当及时恢复种植条件。"})
MERGE (art18)-[:PART_OF]->(chapter3)

// 设施农业用地
MERGE (concept4:Object {name: "设施农业用地", type: "land_use_type", source_article: "第十八条"})
MERGE (concept5:Object {name: "耕作层", type: "soil_layer", source_article: "第十八条"})

// 用地原则
MERGE (principle4:Principle {name: "设施农业用地不占或少占耕地原则", source_article: "第十八条"})
MERGE (principle5:Principle {name: "保护耕作层原则", source_article: "第十八条"})

// 管理要求
MERGE (requirement2:Object {name: "用地范围和规模标准", type: "standard", source_article: "第十八条"})
MERGE (requirement3:Object {name: "备案要求", type: "requirement", source_article: "第十八条"})
MERGE (requirement4:Object {name: "信息上传要求", type: "requirement", source_article: "第十八条"})

// 系统与平台
MERGE (system2:System {name: "设施农业用地监管系统", purpose: "监管设施农业用地", source_article: "第十八条"})

// 义务主体
MERGE (agent10:Agent {name: "设施农业用地使用者", type: "entity"})

// 义务
MERGE (duty26:Obligation {description: "严格执行国家和省规定的用地范围和规模标准", source_article: "第十八条"})
MERGE (duty27:Obligation {description: "按照规定备案", source_article: "第十八条"})
MERGE (duty28:Obligation {description: "将用地信息上传至设施农业用地监管系统", source_article: "第十八条"})
MERGE (duty29:Obligation {description: "采取措施防止破坏耕地耕作层", source_article: "第十八条"})
MERGE (duty30:Obligation {description: "不再使用的设施农业用地应及时恢复种植条件", source_article: "第十八条"})

// 关系建立
MERGE (agent10)-[:HAS_DUTY]->(duty26)
MERGE (agent10)-[:HAS_DUTY]->(duty27)
MERGE (agent10)-[:HAS_DUTY]->(duty28)
MERGE (agent10)-[:HAS_DUTY]->(duty29)
MERGE (agent10)-[:HAS_DUTY]->(duty30)

MERGE (duty26)-[:FOLLOWS_REQUIREMENT]->(requirement2)
MERGE (duty27)-[:FOLLOWS_REQUIREMENT]->(requirement3)
MERGE (duty28)-[:FOLLOWS_REQUIREMENT]->(requirement4)
MERGE (duty28)-[:USES_SYSTEM]->(system2)

MERGE (concept4)-[:FOLLOWS_PRINCIPLE]->(principle4)
MERGE (concept4)-[:FOLLOWS_PRINCIPLE]->(principle5)

MERGE (duty29)-[:PROTECTS]->(concept5)
MERGE (duty30)-[:RESTORES]->(concept5)

MERGE (art18)-[:DEFINES_CONCEPT]->(concept4)
MERGE (art18)-[:INVOLVES]->(agent10)
MERGE (art18)-[:USES_SYSTEM]->(system2)

// 第十九条
MERGE (art19:Article {number: "第十九条", full_text: "禁止任何单位和个人在国土空间规划确定的禁止开垦的范围内从事土地开发活动。按照国土空间规划，开发未确定土地使用权的国有荒山、荒地、荒滩从事种植业、林业、畜牧业、渔业生产的，应当向土地所在地的县级人民政府自然资源主管部门提出申请，由县级人民政府批准。开发农民集体所有荒山、荒地、荒滩的，应当符合农村土地承包管理有关规定。"})
MERGE (art19)-[:PART_OF]->(chapter3)

// 禁止行为
MERGE (prohibition1:Prohibition {description: "在禁止开垦范围内从事土地开发活动", source_article: "第十九条"})
MERGE (art19)-[:DEFINES_PROHIBITION]->(prohibition1)

// 土地类型与权属关系
MERGE (land_type_gov:Object {name: "国有荒山荒地荒滩", type: "land_type", ownership: "state", source_article: "第十九条"})
MERGE (land_type_collective:Object {name: "农民集体所有荒山荒地荒滩", type: "land_type", ownership: "collective", source_article: "第十九条"})

// 细分土地类型
MERGE (wasteland_mountain:Object {name: "荒山", type: "land_subtype", source_article: "第十九条"})
MERGE (wasteland_land:Object {name: "荒地", type: "land_subtype", source_article: "第十九条"})
MERGE (wasteland_beach:Object {name: "荒滩", type: "land_subtype", source_article: "第十九条"})

// 产业类型
MERGE (industry1:Object {name: "种植业", type: "industry", source_article: "第十九条"})
MERGE (industry2:Object {name: "林业", type: "industry", source_article: "第十九条"})
MERGE (industry3:Object {name: "畜牧业", type: "industry", source_article: "第十九条"})
MERGE (industry4:Object {name: "渔业", type: "industry", source_article: "第十九条"})

// 申请审批主体
MERGE (agent11:Agent {name: "土地开发者", type: "entity"})
MERGE (agent12:Agent {name: "县级人民政府自然资源主管部门", type: "department"})
MERGE (agent13:Agent {name: "县级人民政府", type: "government_level"})

// 法规依据
MERGE (regulation1:Object {name: "农村土地承包管理规定", type: "regulation", source_article: "第十九条"})
MERGE (regulation2:Object {name: "国土空间规划"})

// 审批流程
MERGE (procedure2:Procedure {name: "国有荒山荒地荒滩开发审批流程", steps: "向土地所在地的县级人民政府自然资源主管部门提出申请，由县级人民政府批准", source_article: "第十九条"})

// 义务
MERGE (duty31:Obligation {description: "向土地所在地的县级人民政府自然资源主管部门提出申请", source_article: "第十九条"})
MERGE (duty32:Obligation {description: "符合农村土地承包管理有关规定", source_article: "第十九条"})

// 土地开发条件
MERGE (condition1:Object {name: "未确定土地使用权", type: "condition", source_article: "第十九条"})
MERGE (condition2:Object {name: "按照国土空间规划", type: "condition", source_article: "第十九条"})

// 关系建立（增强土地类型连接）
// 土地类型与细分类型关系
MERGE (land_type_gov)-[:INCLUDES]->(wasteland_mountain)
MERGE (land_type_gov)-[:INCLUDES]->(wasteland_land)
MERGE (land_type_gov)-[:INCLUDES]->(wasteland_beach)
MERGE (land_type_collective)-[:INCLUDES]->(wasteland_mountain)
MERGE (land_type_collective)-[:INCLUDES]->(wasteland_land)
MERGE (land_type_collective)-[:INCLUDES]->(wasteland_beach)

// 土地类型与权属关系
MERGE (land_type_gov)-[:HAS_OWNERSHIP]->(regulation2)
MERGE (land_type_collective)-[:GOVERNED_BY]->(regulation1)

// 土地类型与产业类型关系
MERGE (land_type_gov)-[:SUITABLE_FOR]->(industry1)
MERGE (land_type_gov)-[:SUITABLE_FOR]->(industry2)
MERGE (land_type_gov)-[:SUITABLE_FOR]->(industry3)
MERGE (land_type_gov)-[:SUITABLE_FOR]->(industry4)
MERGE (land_type_collective)-[:SUITABLE_FOR]->(industry1)
MERGE (land_type_collective)-[:SUITABLE_FOR]->(industry2)
MERGE (land_type_collective)-[:SUITABLE_FOR]->(industry3)
MERGE (land_type_collective)-[:SUITABLE_FOR]->(industry4)

// 土地开发条件与土地类型关系
MERGE (land_type_gov)-[:REQUIRES_CONDITION]->(condition1)
MERGE (land_type_gov)-[:REQUIRES_CONDITION]->(condition2)
MERGE (land_type_collective)-[:REQUIRES_CONDITION]->(condition2)

// 申请流程与土地类型关系
MERGE (procedure2)-[:APPLIES_TO]->(land_type_gov)
MERGE (procedure2)-[:REQUIRES]->(condition1)
MERGE (procedure2)-[:REQUIRES]->(condition2)

// 主体与义务关系
MERGE (agent11)-[:PROHIBITED_FROM]->(prohibition1)
MERGE (agent11)-[:HAS_DUTY]->(duty31)
MERGE (agent11)-[:HAS_DUTY]->(duty32)

// 义务与土地类型关系
MERGE (duty31)-[:APPLIES_TO]->(land_type_gov)
MERGE (duty32)-[:APPLIES_TO]->(land_type_collective)

// 义务与审批流程关系
MERGE (duty31)-[:FOLLOWS_PROCEDURE]->(procedure2)
MERGE (duty31)-[:SUBMITS_TO]->(agent12)
MERGE (agent12)-[:FORWARDS_TO]->(agent13)
MERGE (agent13)-[:HAS_AUTHORITY]->(land_type_gov)

// 文章与主体关系
MERGE (art19)-[:INVOLVES]->(agent11)
MERGE (art19)-[:INVOLVES]->(agent12)
MERGE (art19)-[:INVOLVES]->(agent13)

// 文章与土地类型关系
MERGE (art19)-[:REGULATES]->(land_type_gov)
MERGE (art19)-[:REGULATES]->(land_type_collective)
MERGE (art19)-[:REFERENCES]->(regulation1)
MERGE (art19)-[:REFERENCES]->(regulation2)

// 文章与产业类型关系
MERGE (art19)-[:COVERS_INDUSTRY]->(industry1)
MERGE (art19)-[:COVERS_INDUSTRY]->(industry2)
MERGE (art19)-[:COVERS_INDUSTRY]->(industry3)
MERGE (art19)-[:COVERS_INDUSTRY]->(industry4)

// 第二十条
MERGE (art20:Article {number: "第二十条", full_text: "省人民政府应当根据耕地总量动态平衡目标制定开垦耕地计划，由地级以上市人民政府组织实施。"})
MERGE (art20)-[:PART_OF]->(chapter3)

// 耕地开垦计划
MERGE (plan1:Object {name: "开垦耕地计划", type: "plan", source_article: "第二十条"})
MERGE (goal6:Goal {description: "耕地总量动态平衡", source_article: "第二十条"})

// 责任主体
MERGE (agent14:Agent {name: "省人民政府", type: "government_level"})
MERGE (agent15:Agent {name: "地级以上市人民政府", type: "government_level"})

// 义务
MERGE (duty33:Obligation {description: "根据耕地总量动态平衡目标制定开垦耕地计划", source_article: "第二十条"})
MERGE (duty34:Obligation {description: "组织实施开垦耕地计划", source_article: "第二十条"})

// 关系建立
MERGE (agent14)-[:HAS_DUTY]->(duty33)
MERGE (agent15)-[:HAS_DUTY]->(duty34)

MERGE (duty33)-[:AIMS_FOR]->(goal6)
MERGE (duty33)-[:CREATES_PLAN]->(plan1)
MERGE (duty34)-[:IMPLEMENTS_PLAN]->(plan1)

MERGE (art20)-[:INVOLVES]->(agent14)
MERGE (art20)-[:INVOLVES]->(agent15)

// 第二十一条
MERGE (art21:Article {number: "第二十一条", full_text: "因挖损、塌陷、压占等造成土地破坏的，用地单位和个人应当按照国家和省有关规定负责复垦。用地单位和个人用地前应当依法编制土地复垦方案，合理安排足额的土地复垦费用。县级以上人民政府自然资源主管部门应当综合考虑土地类型、预计损毁面积及程度、复垦标准、复垦用途和完成复垦任务所需的工程量等因素，根据土地复垦有关标准和要求，对土地复垦方案安排的土地复垦费用进行审查。土地复垦费用测算不足够、不合理，或者预存和使用计划不清晰的，不予通过审查。用地单位和个人应当与损毁土地所在地县级以上人民政府自然资源主管部门、银行共同签订土地复垦费用使用监管协议，明确土地复垦费用预存和使用的时间、数额、程序、条件和违约责任等，并明确支取土地复垦费用的情形。用地单位和个人应当按照土地复垦方案开展土地复垦工作。拒不履行土地复垦义务，或者复垦验收中经整改仍不合格的，依法缴纳土地复垦费。县级以上人民政府自然资源主管部门可以委托第三方机构测算土地复垦费，测算数额按照有关规定审查确定，测算费用一并计入土地复垦费。用地单位和个人未按照审查确定的数额缴纳土地复垦费，经催告仍不缴纳的，由县级以上人民政府自然资源主管部门会同有关部门代为组织复垦。所需费用由县级以上人民政府自然资源主管部门出具支取通知书，按照土地复垦费用使用监管协议约定从预存的土地复垦费用中支取，对因分期预存等原因导致不足部分可以继续向用地单位和个人追缴。"})
MERGE (art21)-[:PART_OF]->(chapter3)

// 土地复垦概念
MERGE (concept6:Object {name: "土地复垦", type: "concept", source_article: "第二十一条"})
MERGE (concept7:Object {name: "土地复垦费", type: "fee", source_article: "第二十一条"})
MERGE (concept8:Object {name: "土地复垦费用", type: "fee", source_article: "第二十一条"})

// 责任主体
MERGE (agent16:Agent {name: "用地单位和个人", type: "entity"})
MERGE (agent17:Agent {name: "县级以上人民政府自然资源主管部门", type: "department"})
MERGE (agent18:Agent {name: "银行", type: "organization"})
MERGE (agent19:Agent {name: "第三方机构", type: "organization"})

// 复垦方案
MERGE (plan2:Object {name: "土地复垦方案", type: "plan", source_article: "第二十一条"})

// 监管协议
MERGE (agreement1:Object {name: "土地复垦费用使用监管协议", type: "agreement", source_article: "第二十一条"})

// 审查标准
MERGE (criterion1:Object {name: "土地复垦费用审查标准", factors: "土地类型、预计损毁面积及程度、复垦标准、复垦用途和完成复垦任务所需的工程量等因素", source_article: "第二十一条"})

// 义务
MERGE (duty35:Obligation {description: "负责复垦被破坏的土地", source_article: "第二十一条"})
MERGE (duty36:Obligation {description: "编制土地复垦方案", source_article: "第二十一条"})
MERGE (duty37:Obligation {description: "合理安排足额的土地复垦费用", source_article: "第二十一条"})
MERGE (duty38:Obligation {description: "签订土地复垦费用使用监管协议", source_article: "第二十一条"})
MERGE (duty39:Obligation {description: "按照土地复垦方案开展土地复垦工作", source_article: "第二十一条"})
MERGE (duty40:Obligation {description: "依法缴纳土地复垦费", source_article: "第二十一条"})

// 审查义务
MERGE (duty41:Obligation {description: "对土地复垦方案安排的土地复垦费用进行审查", source_article: "第二十一条"})
MERGE (duty42:Obligation {description: "委托第三方机构测算土地复垦费", source_article: "第二十一条"})
MERGE (duty43:Obligation {description: "代为组织复垦", source_article: "第二十一条"})

// 关系建立
MERGE (agent16)-[:HAS_DUTY]->(duty35)
MERGE (agent16)-[:HAS_DUTY]->(duty36)
MERGE (agent16)-[:HAS_DUTY]->(duty37)
MERGE (agent16)-[:HAS_DUTY]->(duty38)
MERGE (agent16)-[:HAS_DUTY]->(duty39)
MERGE (agent16)-[:HAS_DUTY]->(duty40)

MERGE (agent17)-[:HAS_DUTY]->(duty41)
MERGE (agent17)-[:HAS_DUTY]->(duty42)
MERGE (agent17)-[:HAS_DUTY]->(duty43)

MERGE (duty36)-[:CREATES_PLAN]->(plan2)
MERGE (duty41)-[:FOLLOWS_CRITERION]->(criterion1)
MERGE (duty38)-[:SIGNS_AGREEMENT]->(agreement1)

MERGE (agent16)-[:PARTICIPATES_IN]->(agreement1)
MERGE (agent17)-[:PARTICIPATES_IN]->(agreement1)
MERGE (agent18)-[:PARTICIPATES_IN]->(agreement1)

MERGE (duty40)-[:PAYS_FEE]->(concept7)
MERGE (duty37)-[:ALLOWS_FEE]->(concept8)

MERGE (art21)-[:DEFINES_CONCEPT]->(concept6)
MERGE (art21)-[:INVOLVES]->(agent16)
MERGE (art21)-[:INVOLVES]->(agent17)
MERGE (art21)-[:INVOLVES]->(agent18)
MERGE (art21)-[:INVOLVES]->(agent19)

// 第二十二条
MERGE (art22:Article {number: "第二十二条", full_text: "县级以上人民政府应当加强对耕地耕作层的保护，依法对建设所占用耕地耕作层的土壤利用作出合理安排。非农业建设占用耕地的，应当编制耕作层剥离再利用方案，按照国家有关技术规范进行耕作层剥离，并按照要求将剥离的耕作层土壤用于新开垦耕地、劣质地或者其他耕地的土壤改良等。剥离相关费用作为生产成本列入建设项目投资预算。确因受到严重破坏或者严重污染等无法剥离再利用的，经县级人民政府同意后方可不实施剥离。鼓励依托公共资源交易平台，探索剥离耕作层土壤交易。"})
MERGE (art22)-[:PART_OF]->(chapter3)

// 耕作层保护核心概念
MERGE (concept9:Object {name: "耕地耕作层", type: "soil_layer", source_article: "第二十二条"})
MERGE (concept10:Object {name: "耕作层剥离再利用", type: "concept", source_article: "第二十二条"})
MERGE (concept11:Object {name: "耕作层土壤", type: "soil_type", source_article: "第二十二条"})

// 保护主体
MERGE (agent20:Agent {name: "非农业建设单位", type: "entity"})
MERGE (agent21:Agent {name: "县级人民政府", type: "government_level"})

// 保护方案与方法
MERGE (plan3:Object {name: "耕作层剥离再利用方案", type: "plan", source_article: "第二十二条"})
MERGE (method4:Object {name: "耕作层剥离", type: "protection_method", source_article: "第二十二条"})
MERGE (method5:Object {name: "土壤改良", type: "improvement_method", source_article: "第二十二条"})

// 技术规范
MERGE (standard1:Object {name: "国家有关技术规范", type: "standard", source_article: "第二十二条"})

// 土壤利用去向
MERGE (land_use1:Object {name: "新开垦耕地", type: "land_use", source_article: "第二十二条"})
MERGE (land_use2:Object {name: "劣质地", type: "land_use", source_article: "第二十二条"})
MERGE (land_use3:Object {name: "其他耕地", type: "land_use", source_article: "第二十二条"})

// 费用管理
MERGE (cost1:Object {name: "剥离相关费用", type: "cost", source_article: "第二十二条"})
MERGE (budget1:Object {name: "建设项目投资预算", type: "budget", source_article: "第二十二条"})

// 例外情况
MERGE (exception1:Object {name: "严重破坏", type: "exception_condition", source_article: "第二十二条"})
MERGE (exception2:Object {name: "严重污染", type: "exception_condition", source_article: "第二十二条"})
MERGE (exception3:Object {name: "无法剥离再利用", type: "exception_condition", source_article: "第二十二条"})

// 交易平台
MERGE (platform1:Object {name: "公共资源交易平台", type: "platform", purpose: "耕作层土壤交易", source_article: "第二十二条"})
MERGE (transaction1:Object {name: "剥离耕作层土壤交易", type: "transaction_type", source_article: "第二十二条"})

// 保护义务
MERGE (duty44:Obligation {description: "加强对耕地耕作层的保护", source_article: "第二十二条"})
MERGE (duty45:Obligation {description: "对建设所占用耕地耕作层的土壤利用作出合理安排", source_article: "第二十二条"})
MERGE (duty46:Obligation {description: "编制耕作层剥离再利用方案", source_article: "第二十二条"})
MERGE (duty47:Obligation {description: "按照国家有关技术规范进行耕作层剥离", source_article: "第二十二条"})
MERGE (duty48:Obligation {description: "将剥离的耕作层土壤用于新开垦耕地、劣质地或者其他耕地的土壤改良等", source_article: "第二十二条"})
MERGE (duty49:Obligation {description: "将剥离相关费用作为生产成本列入建设项目投资预算", source_article: "第二十二条"})
MERGE (duty52:Obligation {description: "经县级人民政府同意后方可不实施剥离", condition: "确因受到严重破坏或者严重污染等无法剥离再利用", source_article: "第二十二条"})

// 鼓励措施
MERGE (encourage1:Object {name: "探索剥离耕作层土壤交易", type: "encouragement", source_article: "第二十二条"})

// 关系建立（全面连接各实体）
// 政府保护责任关系
MERGE (agent2)-[:HAS_DUTY]->(duty44)
MERGE (agent2)-[:HAS_DUTY]->(duty45)
MERGE (duty44)-[:PROTECTS]->(concept9)
MERGE (duty45)-[:MANAGES]->(concept11)

// 非农业建设单位义务关系
MERGE (agent20)-[:HAS_DUTY]->(duty46)
MERGE (agent20)-[:HAS_DUTY]->(duty47)
MERGE (agent20)-[:HAS_DUTY]->(duty48)
MERGE (agent20)-[:HAS_DUTY]->(duty49)
MERGE (agent20)-[:HAS_DUTY]->(duty52)

// 方案与方法关系
MERGE (duty46)-[:CREATES_PLAN]->(plan3)
MERGE (plan3)-[:USES_METHOD]->(method4)
MERGE (method4)-[:PROTECTS]->(concept9)
MERGE (duty47)-[:FOLLOWS_STANDARD]->(standard1)

// 土壤利用关系
MERGE (duty48)-[:USES_SOIL]->(concept11)
MERGE (duty48)-[:USES_METHOD]->(method5)
MERGE (concept11)-[:USED_FOR_IMPROVEMENT_OF]->(land_use1)
MERGE (concept11)-[:USED_FOR_IMPROVEMENT_OF]->(land_use2)
MERGE (concept11)-[:USED_FOR_IMPROVEMENT_OF]->(land_use3)
MERGE (method5)-[:IMPROVES]->(land_use1)
MERGE (method5)-[:IMPROVES]->(land_use2)
MERGE (method5)-[:IMPROVES]->(land_use3)

// 费用管理关系
MERGE (duty49)-[:ALLOWS_COST]->(cost1)
MERGE (cost1)-[:INCLUDED_IN]->(budget1)
MERGE (budget1)-[:BELONGS_TO]->(agent20)

// 例外情况关系
MERGE (exception1)-[:LEADS_TO]->(exception3)
MERGE (exception2)-[:LEADS_TO]->(exception3)
MERGE (exception3)-[:REQUIRES_APPROVAL_FROM]->(agent21)
MERGE (duty52)-[:TRIGGERED_BY]->(exception3)
MERGE (duty52)-[:REQUIRES_APPROVAL_FROM]->(agent21)

// 交易平台关系
MERGE (platform1)-[:SUPPORTS]->(transaction1)
MERGE (transaction1)-[:TRADES]->(concept11)
MERGE (art22)-[:ENCOURAGES]->(encourage1)
MERGE (encourage1)-[:USES_PLATFORM]->(platform1)
MERGE (encourage1)-[:PROMOTES]->(transaction1)

// 文章与主体关系
MERGE (art22)-[:INVOLVES]->(agent2)
MERGE (art22)-[:INVOLVES]->(agent20)
MERGE (art22)-[:INVOLVES]->(agent21)

// 文章与核心概念关系
MERGE (art22)-[:DEFINES_CONCEPT]->(concept9)
MERGE (art22)-[:DEFINES_CONCEPT]->(concept10)
MERGE (art22)-[:DEFINES_CONCEPT]->(concept11)

// 文章与平台关系
MERGE (art22)-[:USES_PLATFORM]->(platform1)
MERGE (art22)-[:PROMOTES_TRANSACTION]->(transaction1)

// 第二十三条
MERGE (art23:Article {number: "第二十三条", full_text: "各级人民政府应当加强对耕地质量的保护和提升，任何单位和个人不得损毁耕地种植条件。因人为因素损毁耕地种植条件需要进行技术鉴定的，行政机关、当事人或者其他利害关系人可以向具备鉴定能力的机构或者县级以上人民政府农业农村等相关主管部门申请。"})
MERGE (art23)-[:PART_OF]->(chapter3)

// 耕地质量保护
MERGE (concept13:Object {name: "耕地种植条件", type: "concept", source_article: "第二十三条"})
MERGE (concept12:Object {name: "耕地质量", type: "concept", source_article: "第二十三条"})

// 禁止行为
MERGE (prohibition2:Prohibition {description: "损毁耕地种植条件", source_article: "第二十三条"})

// 技术鉴定
MERGE (service1:Object {name: "耕地种植条件技术鉴定", type: "service", source_article: "第二十三条"})

// 申请主体
MERGE (applicant1:Agent {name: "行政机关", type: "entity"})
MERGE (applicant2:Agent {name: "当事人", type: "person"})
MERGE (applicant3:Agent {name: "利害关系人", type: "entity"})
MERGE (applicant4:Agent {name: "县级以上人民政府农业农村主管部门", type: "department"})

// 保护义务
MERGE (duty50:Obligation {description: "加强对耕地质量的保护和提升", source_article: "第二十三条"})
MERGE (duty51:Obligation {description: "不得损毁耕地种植条件", source_article: "第二十三条"})

// 申请权利
MERGE (right1:Right {description: "向具备鉴定能力的机构或者县级以上人民政府农业农村等相关主管部门申请技术鉴定", source_article: "第二十三条"})

// 关系建立
MERGE (agent1)-[:HAS_DUTY]->(duty50)
MERGE (agent1)-[:HAS_DUTY]->(duty51)
MERGE (applicant1)-[:HAS_RIGHT]->(right1)
MERGE (applicant2)-[:HAS_RIGHT]->(right1)
MERGE (applicant3)-[:HAS_RIGHT]->(right1)

MERGE (applicant1)-[:PROHIBITED_FROM]->(prohibition2)
MERGE (applicant2)-[:PROHIBITED_FROM]->(prohibition2)
MERGE (applicant3)-[:PROHIBITED_FROM]->(prohibition2)

MERGE (duty50)-[:PROTECTS]->(concept12)
MERGE (duty51)-[:PROTECTS]->(concept12)
MERGE (right1)-[:REQUESTS_SERVICE]->(service1)
MERGE (service1)-[:RELATED_TO]->(concept13)

MERGE (art23)-[:INVOLVES]->(agent1)
MERGE (art23)-[:INVOLVES]->(applicant1)
MERGE (art23)-[:INVOLVES]->(applicant2)
MERGE (art23)-[:INVOLVES]->(applicant3)
MERGE (art23)-[:INVOLVES]->(applicant4)