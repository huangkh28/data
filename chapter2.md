//第二章
// 创建第二章节点（确保文档节点已存在）
MATCH (doc:Document {name: "广东省土地管理条例"})
MERGE (chapter2:Chapter {number: "第二章", title: "国土空间规划"})
MERGE (chapter2)-[:PART_OF]->(doc)

// 第六条
MERGE (art6:Article {number: "第六条", full_text: "经依法批准的国土空间规划是各类开发、保护、建设活动的基本依据。不得在国土空间规划体系之外另设其他空间规划。各级人民政府应当按照国家和省有关规定组织编制国土空间规划。国土空间规划包括总体规划、详细规划和专项规划。下级国土空间规划应当服从上级国土空间规划；详细规划、专项规划应当服从总体规划；相关专项规划应当相互协同，并与详细规划做好衔接。"})
MERGE (art6)-[:PART_OF]->(chapter2)

// 规划类型
MERGE (plan_type1:Object {name: "总体规划", type: "plan_type",source_article:"第六条"})
MERGE (plan_type2:Object {name: "详细规划", type: "plan_type",source_article:"第六条"})
MERGE (plan_type3:Object {name: "专项规划", type: "plan_type",source_article:"第六条"})
MERGE (plan_type4:Object {name: "国土空间规划", type: "plan_type",source_article:"第六条"})

// 规划层级关系
MERGE (plan_type2)-[:SUBORDINATE_TO]->(plan_type1)
MERGE (plan_type3)-[:SUBORDINATE_TO]->(plan_type1)
MERGE (plan_type3)-[:COORDINATES_WITH]->(plan_type2)
MERGE (plan_type2)-[:COORDINATES_WITH]->(plan_type3)

// 规划原则
MERGE (principle1:Principle {name: "规划体系唯一性原则",source_article:"第六条"})
MERGE (principle2:Principle {name: "下级服从上级原则",source_article:"第六条"})
MERGE (principle3:Principle {name: "详细规划、专项规划服从总体规划原则",source_article:"第六条"})
MERGE (principle4:Principle {name: "专项规划协同原则",source_article:"第六条"})

MERGE (art6)-[:ESTABLISHES_PRINCIPLE]->(principle1)
MERGE (art6)-[:ESTABLISHES_PRINCIPLE]->(principle2)
MERGE (art6)-[:ESTABLISHES_PRINCIPLE]->(principle3)
MERGE (art6)-[:ESTABLISHES_PRINCIPLE]->(principle4)

// 规划编制主体
MERGE (agent1:Agent {name: "各级人民政府", type: "government_level"})
MERGE (agent1)-[:HAS_DUTY]->(duty1:Obligation {description: "按照国家和省有关规定组织编制国土空间规划",source_article:"第六条"})

// 将主体与条例关联
MERGE (art6)-[:INVOLVES]->(agent1)
MERGE (art6)-[:STIPULATE]->(plan_type4)
MERGE (plan_type4)-[:CONTAIN]->(plan_type1)
MERGE (plan_type4)-[:CONTAIN]->(plan_type2)
MERGE (plan_type4)-[:CONTAIN]->(plan_type3)

// 第七条
MERGE (art7:Article {number: "第七条", full_text: "编制国土空间规划应当细化落实国家和省发展规划提出的国土空间开发保护要求，科学有序统筹安排农业、生态、城镇等功能空间，划定落实永久基本农田、生态保护红线和城镇开发边界，优化国土空间结构和布局，提升国土空间开发保护的质量和效率。国土空间规划的编制、实施应当公开征求社会公众意见，主动接受公众监督。规划依据、内容、程序、结果、查询方式、监督方式等信息应当依法公开。"})
MERGE (art7)-[:PART_OF]->(chapter2)

// 功能空间
MERGE (space1:Object {name: "农业功能空间", type: "space",source_article:"第七条"})
MERGE (space2:Object {name: "生态功能空间", type: "space",source_article:"第七条"})
MERGE (space3:Object {name: "城镇功能空间", type: "space",source_article:"第七条"})

// 控制线
MERGE (control_line1:Object {name: "永久基本农田", type: "control_line"})
MERGE (control_line2:Object {name: "生态保护红线", type: "control_line"})
MERGE (control_line3:Object {name: "城镇开发边界", type: "control_line"})

// 规划编制内容
MERGE (duty2:Obligation {description: "细化落实国家和省发展规划提出的国土空间开发保护要求",source_article:"第七条"})
MERGE (duty3:Obligation {description: "科学有序统筹安排农业、生态、城镇等功能空间",source_article:"第七条"})
MERGE (duty4:Obligation {description: "划定落实永久基本农田、生态保护红线和城镇开发边界",source_article:"第七条"})
MERGE (duty5:Obligation {description: "优化国土空间结构和布局",source_article:"第七条"})
MERGE (duty6:Obligation {description: "提升国土空间开发保护的质量和效率",source_article:"第七条"})

// 规划公开要求
MERGE (duty7:Obligation {description: "编制、实施应当公开征求社会公众意见",source_article:"第七条"})
MERGE (duty8:Obligation {description: "主动接受公众监督",source_article:"第七条"})
MERGE (duty9:Obligation {description: "规划依据、内容、程序、结果、查询方式、监督方式等信息应当依法公开",source_article:"第七条"})

// 将义务与条例关联
MERGE (art7)-[:HAS_DUTY]->(duty2)
MERGE (art7)-[:HAS_DUTY]->(duty3)
MERGE (art7)-[:HAS_DUTY]->(duty4)
MERGE (art7)-[:HAS_DUTY]->(duty5)
MERGE (art7)-[:HAS_DUTY]->(duty6)
MERGE (art7)-[:HAS_DUTY]->(duty7)
MERGE (art7)-[:HAS_DUTY]->(duty8)
MERGE (art7)-[:HAS_DUTY]->(duty9)

// 将功能空间与义务关联
MERGE (duty3)-[:ALLOCATES_SPACE]->(space1)
MERGE (duty3)-[:ALLOCATES_SPACE]->(space2)
MERGE (duty3)-[:ALLOCATES_SPACE]->(space3)

// 将控制线与义务关联
MERGE (duty4)-[:DEFINES_CONTROL_LINE]->(control_line1)
MERGE (duty4)-[:DEFINES_CONTROL_LINE]->(control_line2)
MERGE (duty4)-[:DEFINES_CONTROL_LINE]->(control_line3)

// 第八条
MERGE (art8:Article {number: "第八条", full_text: "省国土空间总体规划由省人民政府组织编制，经省人民代表大会常务委员会审议后，报国务院批准。地级以上市国土空间总体规划由本级人民政府组织编制，经本级人民代表大会常务委员会审议后，报省人民政府批准。国家规定需报国务院批准的城市国土空间总体规划，由本级人民政府组织编制，经本级人民代表大会常务委员会审议后，由省人民政府审核并报批。县（市、区）国土空间总体规划由本级人民政府组织编制，经本级人民代表大会常务委员会审议后，按照省的规定报批。乡镇国土空间总体规划由乡镇人民政府组织编制，逐级报地级以上市人民政府批准；以多个乡镇为单元的乡镇国土空间总体规划，按照省的规定组织编制，报地级以上市人民政府批准。"})
MERGE (art8)-[:PART_OF]->(chapter2)

// 规划编制主体与审批主体
MERGE (agent2:Agent {name: "省人民政府", type: "government_level"})
MERGE (agent3:Agent {name: "省人民代表大会常务委员会", type: "legislative_body"})
MERGE (agent4:Agent {name: "国务院", type: "government_level"})
MERGE (agent5:Agent {name: "地级以上市人民政府", type: "government_level"})
MERGE (agent6:Agent {name: "地级以上市人民代表大会常务委员会", type: "legislative_body"})
MERGE (agent7:Agent {name: "县（市、区）人民政府", type: "government_level"})
MERGE (agent8:Agent {name: "乡镇人民政府", type: "government_level"})
MERGE (agent9:Agent {name: "地级以上市人民政府", type: "government_level"})
MERGE (agent10:Agent {name: "省", type: "government_level"})

// 规划类型
MERGE (plan1:Object {name: "省国土空间总体规划", type: "plan",source_article:"第八条"})
MERGE (plan2:Object {name: "地级以上市国土空间总体规划", type: "plan",source_article:"第八条"})
MERGE (plan3:Object {name: "国家规定需报国务院批准的城市国土空间总体规划", type: "plan",source_article:"第八条"})
MERGE (plan4:Object {name: "县（市、区）国土空间总体规划", type: "plan",source_article:"第八条"})
MERGE (plan5:Object {name: "乡镇国土空间总体规划", type: "plan",source_article:"第八条"})

// 审批流程
MERGE (procedure1:Procedure {name: "省国土空间总体规划审批流程", steps: "省人民政府组织编制，经省人民代表大会常务委员会审议后，报国务院批准",source_article:"第八条"})
MERGE (procedure2:Procedure {name: "地级以上市国土空间总体规划审批流程", steps: "地级以上市人民政府组织编制，经本级人民代表大会常务委员会审议后，报省人民政府批准",source_article:"第八条"})
MERGE (procedure3:Procedure {name: "需报国务院批准的城市国土空间总体规划审批流程", steps: "本级人民政府组织编制，经本级人民代表大会常务委员会审议后，由省人民政府审核并报批",source_article:"第八条"})
MERGE (procedure4:Procedure {name: "县（市、区）国土空间总体规划审批流程", steps: "县（市、区）人民政府组织编制，经本级人民代表大会常务委员会审议后，按照省的规定报批",source_article:"第八条"})
MERGE (procedure5:Procedure {name: "乡镇国土空间总体规划审批流程", steps: "乡镇人民政府组织编制，逐级报地级以上市人民政府批准；以多个乡镇为单元的，按照省的规定组织编制，报地级以上市人民政府批准",source_article:"第八条"})

// 将规划与审批流程关联
MERGE (plan1)-[:FOLLOWS_PROCEDURE]->(procedure1)
MERGE (plan2)-[:FOLLOWS_PROCEDURE]->(procedure2)
MERGE (plan3)-[:FOLLOWS_PROCEDURE]->(procedure3)
MERGE (plan4)-[:FOLLOWS_PROCEDURE]->(procedure4)
MERGE (plan5)-[:FOLLOWS_PROCEDURE]->(procedure5)

// 将主体与规划关联
MERGE (agent2)-[:ORGANIZES]->(plan1)
MERGE (agent3)-[:REVIEW]->(plan1)
MERGE (agent4)-[:HAS_AUTHORITY]->(plan1)

MERGE (agent5)-[:ORGANIZES]->(plan2)
MERGE (agent6)-[:REVIEW]->(plan2)
MERGE (agent7)-[:HAS_AUTHORITY]->(plan2)

MERGE (agent5)-[:ORGANIZES]->(plan3)
MERGE (agent6)-[:REVIEW]->(plan3)
MERGE (agent10)-[:REVIEW]->(plan3)
MERGE (agent4)-[:HAS_AUTHORITY]->(plan3)

MERGE (agent7)-[:ORGANIZES]->(plan4)
MERGE (agent7)-[:REVIEW]->(plan4)
MERGE (agent7)-[:HAS_AUTHORITY]->(plan4)

MERGE (agent8)-[:ORGANIZES]->(plan5)
MERGE (agent9)-[:HAS_AUTHORITY]->(plan5)

//将主体与条例相关联
MERGE (art8)-[:INVOLVES]->(agent2)
MERGE (art8)-[:INVOLVES]->(agent3)
MERGE (art8)-[:INVOLVES]->(agent4)
MERGE (art8)-[:INVOLVES]->(agent5)
MERGE (art8)-[:INVOLVES]->(agent6)
MERGE (art8)-[:INVOLVES]->(agent7)
MERGE (art8)-[:INVOLVES]->(agent8)
MERGE (art8)-[:INVOLVES]->(agent9)
MERGE (art8)-[:INVOLVES]->(agent10)

// 第九条
MERGE (art9:Article {number: "第九条", full_text: "详细规划应当对具体地块用途和开发建设强度等作出实施性安排，作为开展国土空间开发保护活动、实施国土空间用途管制、核发城乡建设项目规划许可、进行各项建设等的法定依据。城镇开发边界内的详细规划由地级以上市、县（市）人民政府自然资源主管部门组织编制，报本级人民政府批准。城镇开发边界外的乡村地区，由乡镇人民政府以一个或者几个行政村为单元，组织编制村庄规划作为详细规划，报上一级人民政府批准。"})
MERGE (art9)-[:PART_OF]->(chapter2)

// 详细规划类型
MERGE (detail_plan1:Object {name: "城镇开发边界内详细规划", type: "detail_plan",source_article:"第九条"})
MERGE (detail_plan2:Object {name: "城镇开发边界外村庄规划", type: "detail_plan",source_article:"第九条"})

// 详细规划功能
MERGE (duty10:Obligation {description: "对具体地块用途和开发建设强度等作出实施性安排",source_article:"第九条"})
MERGE (duty11:Obligation {description: "作为开展国土空间开发保护活动的法定依据",source_article:"第九条"})
MERGE (duty12:Obligation {description: "实施国土空间用途管制的法定依据",source_article:"第九条"})
MERGE (duty13:Obligation {description: "核发城乡建设项目规划许可的法定依据",source_article:"第九条"})
MERGE (duty14:Obligation {description: "进行各项建设的法定依据",source_article:"第九条"})

// 将义务与条例关联
MERGE (art9)-[:HAS_DUTY]->(duty10)
MERGE (art9)-[:HAS_DUTY]->(duty11)
MERGE (art9)-[:HAS_DUTY]->(duty12)
MERGE (art9)-[:HAS_DUTY]->(duty13)
MERGE (art9)-[:HAS_DUTY]->(duty14)

// 详细规划编制主体
MERGE (agent11:Agent {name: "地级以上市、县（市）人民政府自然资源主管部门", type: "department"})
MERGE (agent12:Agent {name: "乡镇人民政府", type: "government_level"})
MERGE (agent13:Agent {name: "上一级人民政府", type: "government_level"})

// 将主体与详细规划关联
MERGE (agent11)-[:ORGANIZES]->(detail_plan1)
MERGE (agent12)-[:ORGANIZES]->(detail_plan2)
MERGE (agent13)-[:HAS_AUTHORITY]->(detail_plan2)

//将主体与条例关联
MERGE (art9)-[:INVOLVES]->(agent11)
MERGE (art9)-[:INVOLVES]->(agent12)
MERGE (art9)-[:INVOLVES]->(agent13)

// 第十条
MERGE (art10:Article {number: "第十条", full_text: "专项规划应当体现特定功能，对国土空间特定区域、特定流域、特定领域的开发、保护和利用作出专门安排。不同层级、不同地区的专项规划可以结合实际选择编制的类型和精度。专项规划由县级以上人民政府自然资源主管部门或者其他相关主管部门按照职责分工组织编制。自然资源主管部门组织编制的，报本级人民政府批准；其他相关主管部门组织编制的，按照有关规定审批。"})
MERGE (art10)-[:PART_OF]->(chapter2)

// 专项规划特点
MERGE (feature1:Object {name: "体现特定功能", type: "feature"})
MERGE (feature2:Object {name: "对特定区域、特定流域、特定领域作出专门安排", type: "feature"})
MERGE (feature3:Object {name: "结合实际选择编制类型和精度", type: "feature"})

// 专项规划编制主体
MERGE (agent14:Agent {name: "县级以上人民政府自然资源主管部门", type: "department"})
MERGE (agent15:Agent {name: "其他相关主管部门", type: "department"})
MERGE (agent16:Agent {name: "本级人民政府", type: "government_level"})

// 专项规划审批流程
MERGE (procedure6:Procedure {name: "自然资源主管部门组织编制专项规划审批流程", steps: "报本级人民政府批准",source_article:"第十条"})
MERGE (procedure7:Procedure {name: "其他相关主管部门组织编制专项规划审批流程", steps: "按照有关规定审批",source_article:"第十条"})

// 将专项规划特点与条例关联
MERGE (art10)-[:DESCRIBES_FEATURE]->(feature1)
MERGE (art10)-[:DESCRIBES_FEATURE]->(feature2)
MERGE (art10)-[:DESCRIBES_FEATURE]->(feature3)

// 将编制主体与专项规划关联
MERGE (agent14)-[:ORGANIZES]->(plan_type3)
MERGE (agent15)-[:ORGANIZES]->(plan_type3)
MERGE (agent16)-[:HAS_AUTHORITY]->(plan_type3)

// 将审批流程与专项规划关联
MERGE (plan_type3)-[:FOLLOWS_PROCEDURE]->(procedure6)
MERGE (plan_type3)-[:FOLLOWS_PROCEDURE]->(procedure7)

// 将主题和条例相连
MERGE (art10)-[:INVOLVES]->(agent14)
MERGE (art10)-[:INVOLVES]->(agent15)
MERGE (art10)-[:INVOLVES]->(agent16)

// 第十一条
MERGE (art11:Article {number: "第十一条", full_text: "国土空间规划必须严格执行，不得擅自修改；确需修改的，应当经原批准机关同意后，方可按照法定程序进行修改。"})
MERGE (art11)-[:PART_OF]->(chapter2)

// 规划修改原则
MERGE (principle5:Principle {name: "规划严格执行原则",source_article:"第十一条"})
MERGE (principle6:Principle {name: "规划修改需经原批准机关同意原则",source_article:"第十一条"})

MERGE (art11)-[:ESTABLISHES_PRINCIPLE]->(principle5)
MERGE (art11)-[:ESTABLISHES_PRINCIPLE]->(principle6)

MERGE (art11)-[:STIPULATE]->(plan_type4)
MERGE (plan_type4)-[:FOLLOWS_PRINCIPLE]->(principle5)
MERGE (plan_type4)-[:FOLLOWS_PRINCIPLE]->(principle6)


// 第十二条
MERGE (art12:Article {number: "第十二条", full_text: "各级人民政府应当建立规划实施评估机制，依托国土空间基础信息平台，运用国土空间规划实施监督信息系统，开展国土空间规划动态监测评估预警，对国土空间规划实施情况进行监管和评估。"})
MERGE (art12)-[:PART_OF]->(chapter2)

// 评估机制
MERGE (mechanism1:Mechanism {name: "规划实施评估机制", purpose: "对国土空间规划实施情况进行监管和评估",source_article:"第十二条"})
MERGE (platform:Platform {name: "国土空间基础信息平台", purpose: "依托平台开展规划实施监督",source_article:"第十二条"})
MERGE (system:System {name: "国土空间规划实施监督信息系统", purpose: "运用系统开展规划动态监测评估预警",source_article:"第十二条"})

// 评估机制内容
MERGE (duty15:Obligation {description: "建立规划实施评估机制",source_article:"第十二条"})
MERGE (duty16:Obligation {description: "依托国土空间基础信息平台开展规划实施监督",source_article:"第十二条"})
MERGE (duty17:Obligation {description: "运用国土空间规划实施监督信息系统开展动态监测评估预警",source_article:"第十二条"})

// 将义务与条例关联
MERGE (art12)-[:HAS_DUTY]->(duty15)
MERGE (art12)-[:HAS_DUTY]->(duty16)
MERGE (art12)-[:HAS_DUTY]->(duty17)

// 将机制与平台、系统关联
MERGE (mechanism1)-[:USES_PLATFORM]->(platform)
MERGE (mechanism1)-[:USES_SYSTEM]->(system)
MERGE (agent1)-[:HAS_DUTY] ->(mechanism1)
MERGE (art12)-[:INVOLVES] ->(agent1)

// 第十三条
MERGE (art13:Article {number: "第十三条", full_text: "各级人民政府应当根据本级国土空间规划安排，加强土地利用的计划管理，严格按照土地利用年度计划依法批准建设用地，实行建设用地总量控制。"})
MERGE (art13)-[:PART_OF]->(chapter2)

// 土地利用计划管理
MERGE (duty18:Obligation {description: "加强土地利用的计划管理",source_article:"第十三条"})
MERGE (duty19:Obligation {description: "严格按照土地利用年度计划依法批准建设用地",source_article:"第十三条"})
MERGE (duty20:Obligation {description: "实行建设用地总量控制",source_article:"第十三条"})

// 将义务与条例关联
MERGE (art13)-[:HAS_DUTY]->(duty18)
MERGE (art13)-[:HAS_DUTY]->(duty19)
MERGE (art13)-[:HAS_DUTY]->(duty20)