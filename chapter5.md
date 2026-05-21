// 第五章 建设用地供应与利用
// 创建第五章节点（确保文档节点已存在）
MATCH (doc:Document {name: "广东省土地管理条例"})
MERGE (chapter5:Chapter {number: "第五章", title: "建设用地供应与利用"})
MERGE (chapter5)-[:PART_OF]->(doc)

// 第三十九条
MERGE (art39:Article {number: "第三十九条", full_text: "地级以上市、县级人民政府自然资源主管部门应当按照规定组织编制年度建设用地供应计划，征求有关单位意见，报本级人民政府批准后，在政府网站上向社会公布，供社会公众查阅。县级以上人民政府自然资源主管部门应当加强土地市场动态监测与监管，对建设用地批准和供应后的开发情况实行全程监管。"})
MERGE (art39)-[:PART_OF]->(chapter5)

// 相关主体
MERGE (agent38:Agent {name: "地级以上市人民政府自然资源主管部门", type: "department"})
MERGE (agent39:Agent {name: "县级人民政府自然资源主管部门", type: "department"})
MERGE (agent41:Agent {name: "社会公众", type: "public"})

// 供应计划
MERGE (plan1:Object {name: "年度建设用地供应计划", type: "plan"})
MERGE (action1:Object {name: "组织编制", type: "action"})
MERGE (action2:Object {name: "征求有关单位意见", type: "action"})
MERGE (action3:Object {name: "批准", type: "action"})
MERGE (action4:Object {name: "向社会公布", type: "action"})
MERGE (platform1:Object {name: "政府网站", type: "platform"})

// 监管要求
MERGE (monitoring1:Object {name: "土地市场动态监测与监管", type: "monitoring"})
MERGE (monitoring2:Object {name: "全程监管", type: "monitoring", target: "建设用地批准和供应后的开发情况"})

// 义务
MERGE (duty118:Obligation {description: "组织编制年度建设用地供应计划", source_article: "第三十九条"})
MERGE (duty119:Obligation {description: "征求有关单位意见", source_article: "第三十九条"})
MERGE (duty120:Obligation {description: "报本级人民政府批准", source_article: "第三十九条"})
MERGE (duty121:Obligation {description: "在政府网站上向社会公布", source_article: "第三十九条"})
MERGE (duty122:Obligation {description: "加强土地市场动态监测与监管", source_article: "第三十九条"})
MERGE (duty123:Obligation {description: "对建设用地批准和供应后的开发情况实行全程监管", source_article: "第三十九条"})

// 关系建立
MERGE (agent38)-[:HAS_DUTY]->(duty118)
MERGE (agent39)-[:HAS_DUTY]->(duty118)
MERGE (agent38)-[:HAS_DUTY]->(duty119)
MERGE (agent39)-[:HAS_DUTY]->(duty119)
MERGE (agent38)-[:HAS_DUTY]->(duty120)
MERGE (agent39)-[:HAS_DUTY]->(duty120)
MERGE (agent38)-[:HAS_DUTY]->(duty121)
MERGE (agent39)-[:HAS_DUTY]->(duty121)
MERGE (agent38)-[:HAS_DUTY]->(duty122)
MERGE (agent39)-[:HAS_DUTY]->(duty122)
MERGE (agent38)-[:HAS_DUTY]->(duty123)
MERGE (agent39)-[:HAS_DUTY]->(duty123)

MERGE (duty118)-[:PRODUCES]->(plan1)
MERGE (duty119)-[:RELATES_TO]->(plan1)
MERGE (duty120)-[:APPLIES_TO]->(plan1)
MERGE (duty121)-[:PUBLISHES]->(plan1)
MERGE (duty121)-[:USES_PLATFORM]->(platform1)
MERGE (duty121)-[:TARGETS]->(agent41)

MERGE (duty122)-[:IMPLEMENTS]->(monitoring1)
MERGE (duty123)-[:IMPLEMENTS]->(monitoring2)

// 第四十条
MERGE (art40:Article {number: "第四十条", full_text: "新供应国有工业用地，地级以上市、县级人民政府可以与工业用地取得方签订项目履约监管协议，明确产业准入条件、投产时间、投资强度、产出效率、退出机制、股权变更约束、生态环境保护要求等内容。地级以上市、县（市）人民政府可以探索采取先租赁后出让的方式供应工业用地，出让年期在法定出让最高年期内合理确定。采取先租赁后出让方式供应的，应当符合国家规定的条件。"})
MERGE (art40)-[:PART_OF]->(chapter5)

// 相关主体
MERGE (agent42:Agent {name: "工业用地取得方", type: "entity"})
MERGE (agent43:Agent {name: "县（市）人民政府", type: "government"})

// 协议与内容
MERGE (agreement2:Object {name: "项目履约监管协议", type: "agreement"})
MERGE (content29:Object {name: "产业准入条件", type: "agreement_content"})
MERGE (content30:Object {name: "投产时间", type: "agreement_content"})
MERGE (content31:Object {name: "投资强度", type: "agreement_content"})
MERGE (content32:Object {name: "产出效率", type: "agreement_content"})
MERGE (content33:Object {name: "退出机制", type: "agreement_content"})
MERGE (content34:Object {name: "股权变更约束", type: "agreement_content"})
MERGE (content35:Object {name: "生态环境保护要求", type: "agreement_content"})

// 供地方式
MERGE (supply_method1:Object {name: "先租赁后出让", type: "supply_method"})
MERGE (requirement28:Object {name: "符合国家规定的条件", type: "requirement"})
MERGE (term_limit:Object {name: "法定出让最高年期", type: "term_limit"})

// 义务
MERGE (duty124:Obligation {description: "签订项目履约监管协议", condition: "新供应国有工业用地", source_article: "第四十条"})
MERGE (duty125:Obligation {description: "明确协议内容", source_article: "第四十条"})
MERGE (duty126:Obligation {description: "探索采取先租赁后出让的方式供应工业用地", source_article: "第四十条"})
MERGE (duty127:Obligation {description: "合理确定出让年期", source_article: "第四十条"})
MERGE (duty128:Obligation {description: "符合国家规定的条件", condition: "采取先租赁后出让方式供应", source_article: "第四十条"})

// 关系建立
MERGE (agent24)-[:HAS_DUTY]->(duty124)
MERGE (agent24)-[:HAS_DUTY]->(duty126)
MERGE (agent43)-[:HAS_DUTY]->(duty126)
MERGE (agent24)-[:HAS_DUTY]->(duty127)
MERGE (agent43)-[:HAS_DUTY]->(duty127)
MERGE (agent24)-[:HAS_DUTY]->(duty128)
MERGE (agent43)-[:HAS_DUTY]->(duty128)

MERGE (duty124)-[:CREATES]->(agreement2)
MERGE (duty124)-[:INVOLVES]->(agent42)
MERGE (duty125)-[:RELATED_TO]->(agreement2)
MERGE (duty125)-[:SPECIFIES]->(content29)
MERGE (duty125)-[:SPECIFIES]->(content30)
MERGE (duty125)-[:SPECIFIES]->(content31)
MERGE (duty125)-[:SPECIFIES]->(content32)
MERGE (duty125)-[:SPECIFIES]->(content33)
MERGE (duty125)-[:SPECIFIES]->(content34)
MERGE (duty125)-[:SPECIFIES]->(content35)

MERGE (duty126)-[:USES_METHOD]->(supply_method1)
MERGE (duty127)-[:BASED_ON]->(term_limit)
MERGE (duty128)-[:MEETS_REQUIREMENT]->(requirement28)

// 第四十一条
MERGE (art41:Article {number: "第四十一条", full_text: "乡镇企业、乡镇村公共设施、公益事业等乡镇村建设，需要使用农村集体所有土地的，由县级人民政府批准；其中，涉及占用农用地、未利用地的，依法办理相关审批手续。县级以上人民政府应当优先引导和推动城中村、城边村、村镇工业集聚区等可连片开发的存量集体经营性建设用地入市，推动集体所有制经济和乡村产业发展。集体经营性建设用地入市应当通过公开的交易平台进行交易，纳入公共资源交易平台体系，并按照国家和省有关规定实施。"})
MERGE (art41)-[:PART_OF]->(chapter5)

// 相关主体
MERGE (agent44:Agent {name: "县级人民政府", type: "government_level"})
MERGE (agent45:Agent {name: "乡镇企业", type: "entity"})
MERGE (agent46:Agent {name: "农村集体经济组织", type: "organization"})

// 用地类型
MERGE (land_use4:Object {name: "乡镇企业用地", type: "land_use_type"})
MERGE (land_use5:Object {name: "乡镇村公共设施用地", type: "land_use_type"})
MERGE (land_use6:Object {name: "公益事业用地", type: "land_use_type"})
MERGE (land_use7:Object {name: "集体经营性建设用地", type: "land_use_type"})

// 重点区域
MERGE (area1:Object {name: "城中村", type: "development_area"})
MERGE (area2:Object {name: "城边村", type: "development_area"})
MERGE (area3:Object {name: "村镇工业集聚区", type: "development_area"})

// 交易机制
MERGE (trading1:Object {name: "公开的交易平台", type: "trading_platform"})
MERGE (trading2:Object {name: "公共资源交易平台体系", type: "trading_system"})

// 义务
MERGE (duty129:Obligation {description: "批准乡镇村建设使用农村集体所有土地", source_article: "第四十一条"})
MERGE (duty130:Obligation {description: "办理相关审批手续", condition: "涉及占用农用地、未利用地", source_article: "第四十一条"})
MERGE (duty131:Obligation {description: "优先引导和推动存量集体经营性建设用地入市", source_article: "第四十一条"})
MERGE (duty132:Obligation {description: "通过公开的交易平台进行交易", condition: "集体经营性建设用地入市", source_article: "第四十一条"})
MERGE (duty133:Obligation {description: "按照国家和省有关规定实施", condition: "集体经营性建设用地入市", source_article: "第四十一条"})

// 关系建立
MERGE (agent44)-[:HAS_DUTY]->(duty129)
MERGE (agent45)-[:HAS_DUTY]->(duty130)
MERGE (agent25)-[:HAS_DUTY]->(duty131)
MERGE (agent46)-[:HAS_DUTY]->(duty132)
MERGE (agent46)-[:HAS_DUTY]->(duty133)

MERGE (duty129)-[:APPLIES_TO]->(land_use4)
MERGE (duty129)-[:APPLIES_TO]->(land_use5)
MERGE (duty129)-[:APPLIES_TO]->(land_use6)
MERGE (duty130)-[:REQUIRES_PROCEDURE]->(procedure4)
MERGE (duty130)-[:REQUIRES_PROCEDURE]->(procedure5)

MERGE (duty131)-[:PRIORITIZES]->(area1)
MERGE (duty131)-[:PRIORITIZES]->(area2)
MERGE (duty131)-[:PRIORITIZES]->(area3)
MERGE (duty131)-[:PROMOTES]->(land_use7)
MERGE (duty131)-[:PROMOTES]->(agent31)
MERGE (duty131)-[:PROMOTES]->(agent46)

MERGE (duty132)-[:USES_PLATFORM]->(trading1)
MERGE (trading1)-[:PART_OF]->(trading2)
MERGE (land_use7)-[:TRADED_ON]->(trading1)

// 第四十二条
MERGE (art42:Article {number: "第四十二条", full_text: "县级以上人民政府应当按照国家和省有关规定落实建设用地指标，合理保障本行政区域农村村民宅基地需求。农村村民一户只能拥有一处宅基地，新批准宅基地的面积按照以下标准执行：平原地区和城市郊区每户不得超过八十平方米，丘陵地区每户不得超过一百二十平方米，山区每户不得超过一百五十平方米。农村村民应当严格按照批准面积和建房标准建设住宅，禁止未批先建、超面积占用宅基地。鼓励通过集体建房、合建住房等方式，保障农村村民户有所居。"})
MERGE (art42)-[:PART_OF]->(chapter5)

// 相关主体
MERGE (agent47:Agent {name: "农村村民", type: "individual"})
MERGE (agent48:Agent {name: "本行政区域", type: "administrative_area"})

// 宅基地管理
MERGE (land_use8:Object {name: "宅基地", type: "land_use_type",source_article: "第四十二条"})
MERGE (indicator1:Object {name: "建设用地指标", type: "land_indicator",source_article: "第四十二条"})
MERGE (standard7:Object {name: "宅基地面积标准", type: "standard",source_article: "第四十二条"})
MERGE (condition1:Object {name: "一户只能拥有一处宅基地", type: "condition",source_article: "第四十二条"})
MERGE (limit3:Object {name: "平原地区和城市郊区每户不超过八十平方米", type: "area_limit",source_article: "第四十二条"})
MERGE (limit4:Object {name: "丘陵地区每户不超过一百二十平方米", type: "area_limit",source_article: "第四十二条"})
MERGE (limit5:Object {name: "山区每户不超过一百五十平方米", type: "area_limit",source_article: "第四十二条"})

// 住宅建设
MERGE (construction1:Object {name: "严格按照批准面积和建房标准建设住宅", type: "construction_requirement"})
MERGE (prohibition5:Object {name: "未批先建", type: "prohibited_action"})
MERGE (prohibition6:Object {name: "超面积占用宅基地", type: "prohibited_action"})

// 保障方式
MERGE (housing1:Object {name: "集体建房", type: "housing_method"})
MERGE (housing2:Object {name: "合建住房", type: "housing_method"})
MERGE (goal3:Object {name: "保障农村村民户有所居", type: "policy_goal"})

// 义务
MERGE (duty134:Obligation {description: "落实建设用地指标", source_article: "第四十二条"})
MERGE (duty135:Obligation {description: "合理保障农村村民宅基地需求", source_article: "第四十二条"})
MERGE (duty136:Obligation {description: "遵守一户一宅规定", source_article: "第四十二条"})
MERGE (duty137:Obligation {description: "严格按照批准面积和建房标准建设住宅", source_article: "第四十二条"})
MERGE (duty138:Obligation {description: "不得未批先建、超面积占用宅基地", source_article: "第四十二条"})

// 鼓励措施
MERGE (encourage1:Object {name: "通过集体建房、合建住房等方式保障农村村民户有所居", type: "encouraged_practice", source_article: "第四十二条"})

// 关系建立
MERGE (agent25)-[:HAS_DUTY]->(duty134)
MERGE (agent25)-[:HAS_DUTY]->(duty135)
MERGE (agent47)-[:HAS_DUTY]->(duty136)
MERGE (agent47)-[:HAS_DUTY]->(duty137)
MERGE (agent47)-[:MUST_NOT]->(prohibition5)
MERGE (agent47)-[:MUST_NOT]->(prohibition6)

MERGE (duty134)-[:RELATED_TO]->(indicator1)
MERGE (duty135)-[:TARGETS]->(land_use8)
MERGE (duty135)-[:TARGETS]->(agent47)
MERGE (duty136)-[:FOLLOWS_CONDITION]->(condition1)
MERGE (duty136)-[:FOLLOWS_STANDARD]->(standard7)
MERGE (standard7)-[:INCLUDES_LIMIT]->(limit3)
MERGE (standard7)-[:INCLUDES_LIMIT]->(limit4)
MERGE (standard7)-[:INCLUDES_LIMIT]->(limit5)

MERGE (duty137)-[:FOLLOWS_REQUIREMENT]->(construction1)
MERGE (construction1)-[:RELATED_TO]->(land_use8)

MERGE (encourage1)-[:USES_METHOD]->(housing1)
MERGE (encourage1)-[:USES_METHOD]->(housing2)
MERGE (encourage1)-[:SERVES_GOAL]->(goal3)
MERGE (art42)-[:ENCOURAGES]->(encourage1)

// 第四十三条
MERGE (art43:Article {number: "第四十三条", full_text: "对进城落户的农村村民，可以通过多种方式鼓励其依法自愿有偿退出宅基地。退出的宅基地，应当优先用于保障本农村集体经济组织成员的宅基地需求。在符合国土空间规划、用途管制和农村村民自愿的前提下，鼓励利用闲置的宅基地用于乡镇村公共设施、公益事业和集体经营性建设用地等用途，或者复垦为农用地。"})
MERGE (art43)-[:PART_OF]->(chapter5)

// 相关主体
MERGE (agent49:Agent {name: "进城落户的农村村民", type: "individual"})
MERGE (agent50:Agent {name: "本农村集体经济组织成员", type: "individual"})

// 退出机制
MERGE (exit_mechanism:Object {name: "依法自愿有偿退出宅基地", type: "exit_mechanism"})
MERGE (priority_use:Object {name: "优先用于保障本农村集体经济组织成员的宅基地需求", type: "priority_use"})

// 闲置宅基地利用
MERGE (idle_land_use1:Object {name: "乡镇村公共设施", type: "land_use_type", source_article: "第四十三条"})
MERGE (idle_land_use2:Object {name: "公益事业", type: "land_use_type"})
MERGE (idle_land_use4:Object {name: "复垦为农用地", type: "land_use_type", source_article: "第四十三条"})
MERGE (condition2:Object {name: "符合国土空间规划", type: "condition", source_article: "第四十三条、第五十二条"})
MERGE (condition3:Object {name: "符合用途管制", type: "condition", source_article: "第四十三条"})
MERGE (condition4:Object {name: "农村村民自愿", type: "condition", source_article: "第四十三条"})

// 义务与鼓励措施
MERGE (encourage2:Object {name: "鼓励依法自愿有偿退出宅基地", type: "encouraged_practice", source_article: "第四十三条"})
MERGE (encourage3:Object {name: "优先用于保障宅基地需求", type: "encouraged_practice", source_article: "第四十三条"})
MERGE (encourage4:Object {name: "鼓励利用闲置宅基地", type: "encouraged_practice", source_article: "第四十三条"})

// 关系建立
MERGE (agent25)-[:ENCOURAGES]->(encourage2)
MERGE (agent25)-[:ENCOURAGES]->(encourage3)
MERGE (agent25)-[:ENCOURAGES]->(encourage4)

MERGE (encourage2)-[:TARGETS]->(agent49)
MERGE (encourage2)-[:RELATED_TO]->(exit_mechanism)
MERGE (encourage3)-[:RELATED_TO]->(priority_use)
MERGE (encourage3)-[:TARGETS]->(agent50)
MERGE (encourage4)-[:REQUIRES_CONDITION]->(condition2)
MERGE (encourage4)-[:REQUIRES_CONDITION]->(condition3)
MERGE (encourage4)-[:REQUIRES_CONDITION]->(condition4)
MERGE (encourage4)-[:USES_FOR]->(idle_land_use1)
MERGE (encourage4)-[:USES_FOR]->(idle_land_use2)
MERGE (encourage4)-[:USES_FOR]->(land_use7)
MERGE (encourage4)-[:USES_FOR]->(idle_land_use4)

// 第四十四条
MERGE (art44:Article {number: "第四十四条", full_text: "县级以上人民政府应当引导各项建设优先开发利用空闲、废弃、闲置和低效利用的土地，稳妥有序推进旧城镇、旧厂房、旧村庄改造。旧城镇、旧厂房、旧村庄改造应当坚持生态优先、绿色发展，提高节约集约用地水平，依法保护历史文化名城、名镇、名村（传统村落）、街区和不可移动文物、历史建筑、历史地段、非物质文化遗产、红色资源、自然景观、古树名木等，保障权利人合法权益。旧城镇、旧厂房、旧村庄改造具体管理办法由省人民政府制定。"})
MERGE (art44)-[:PART_OF]->(chapter5)

// 土地类型
MERGE (land_status1:Object {name: "空闲土地", type: "land_status"})
MERGE (land_status2:Object {name: "废弃土地", type: "land_status"})
MERGE (land_status3:Object {name: "闲置土地", type: "land_status"})
MERGE (land_status4:Object {name: "低效利用土地", type: "land_status"})

// 三旧改造
MERGE (renovation1:Object {name: "旧城镇改造", type: "renovation_type"})
MERGE (renovation2:Object {name: "旧厂房改造", type: "renovation_type"})
MERGE (renovation3:Object {name: "旧村庄改造", type: "renovation_type"})

// 改造原则
MERGE (principle2:Object {name: "生态优先", type: "principle"})
MERGE (principle3:Object {name: "绿色发展", type: "principle"})
MERGE (principle4:Object {name: "节约集约用地", type: "principle"})

// 保护对象
MERGE (protection1:Object {name: "历史文化名城", type: "protection_object"})
MERGE (protection2:Object {name: "名镇", type: "protection_object"})
MERGE (protection3:Object {name: "名村（传统村落）", type: "protection_object"})
MERGE (protection4:Object {name: "街区", type: "protection_object"})
MERGE (protection5:Object {name: "不可移动文物", type: "protection_object"})
MERGE (protection6:Object {name: "历史建筑", type: "protection_object"})
MERGE (protection7:Object {name: "历史地段", type: "protection_object"})
MERGE (protection8:Object {name: "非物质文化遗产", type: "protection_object"})
MERGE (protection9:Object {name: "红色资源", type: "protection_object"})
MERGE (protection10:Object {name: "自然景观", type: "protection_object"})
MERGE (protection11:Object {name: "古树名木", type: "protection_object"})

// 管理办法
MERGE (management1:Object {name: "旧城镇、旧厂房、旧村庄改造具体管理办法", type: "management_measure"})

// 义务
MERGE (duty139:Obligation {description: "引导优先开发利用空闲、废弃、闲置和低效利用的土地", source_article: "第四十四条"})
MERGE (duty140:Obligation {description: "稳妥有序推进旧城镇、旧厂房、旧村庄改造", source_article: "第四十四条"})
MERGE (duty141:Obligation {description: "坚持生态优先、绿色发展", condition: "三旧改造", source_article: "第四十四条"})
MERGE (duty142:Obligation {description: "提高节约集约用地水平", condition: "三旧改造", source_article: "第四十四条"})
MERGE (duty143:Obligation {description: "依法保护文化遗产和自然资源", condition: "三旧改造", source_article: "第四十四条"})
MERGE (duty144:Obligation {description: "保障权利人合法权益", condition: "三旧改造", source_article: "第四十四条"})
MERGE (duty145:Obligation {description: "制定三旧改造具体管理办法", source_article: "第四十四条"})

// 关系建立
MERGE (agent25)-[:HAS_DUTY]->(duty139)
MERGE (agent25)-[:HAS_DUTY]->(duty140)
MERGE (agent25)-[:HAS_DUTY]->(duty141)
MERGE (agent25)-[:HAS_DUTY]->(duty142)
MERGE (agent25)-[:HAS_DUTY]->(duty143)
MERGE (agent25)-[:HAS_DUTY]->(duty144)
MERGE (agent23)-[:HAS_DUTY]->(duty145)

MERGE (duty139)-[:PROMOTES_USE_OF]->(land_status1)
MERGE (duty139)-[:PROMOTES_USE_OF]->(land_status2)
MERGE (duty139)-[:PROMOTES_USE_OF]->(land_status3)
MERGE (duty139)-[:PROMOTES_USE_OF]->(land_status4)

MERGE (duty140)-[:PROMOTES]->(renovation1)
MERGE (duty140)-[:PROMOTES]->(renovation2)
MERGE (duty140)-[:PROMOTES]->(renovation3)

MERGE (duty141)-[:FOLLOWS_PRINCIPLE]->(principle2)
MERGE (duty141)-[:FOLLOWS_PRINCIPLE]->(principle3)
MERGE (duty142)-[:FOLLOWS_PRINCIPLE]->(principle4)

MERGE (duty143)-[:PROTECTS]->(protection1)
MERGE (duty143)-[:PROTECTS]->(protection2)
MERGE (duty143)-[:PROTECTS]->(protection3)
MERGE (duty143)-[:PROTECTS]->(protection4)
MERGE (duty143)-[:PROTECTS]->(protection5)
MERGE (duty143)-[:PROTECTS]->(protection6)
MERGE (duty143)-[:PROTECTS]->(protection7)
MERGE (duty143)-[:PROTECTS]->(protection8)
MERGE (duty143)-[:PROTECTS]->(protection9)
MERGE (duty143)-[:PROTECTS]->(protection10)
MERGE (duty143)-[:PROTECTS]->(protection11)

MERGE (duty145)-[:PRODUCES]->(management1)
MERGE (management1)-[:REGULATES]->(renovation1)
MERGE (management1)-[:REGULATES]->(renovation2)
MERGE (management1)-[:REGULATES]->(renovation3)

// 第四十五条
MERGE (art45:Article {number: "第四十五条", full_text: "县级以上人民政府设立的土地储备机构，负责土地储备的具体实施工作。土地储备机构按照国家规定实行名录制管理，未纳入国家名录的，不得承担土地储备相关工作。鼓励土地储备机构指导农村集体经济组织开展集体经营性建设用地的前期开发、管护等工作。"})
MERGE (art45)-[:PART_OF]->(chapter5)

// 相关主体
MERGE (agent51:Agent {name: "土地储备机构", type: "organization"})
MERGE (agent52:Agent {name: "国家名录", type: "registry"})

// 土地储备
MERGE (land_reserve:Object {name: "土地储备", type: "land_management"})
MERGE (management2:Object {name: "名录制管理", type: "management_method"})
MERGE (prohibition7:Object {name: "未纳入国家名录不得承担土地储备相关工作", type: "prohibition"})

// 鼓励措施
MERGE (encourage5:Object {name: "指导农村集体经济组织开展集体经营性建设用地的前期开发、管护等工作", type: "encouraged_practice", source_article: "第四十五条"})
MERGE (development_work:Object {name: "前期开发", type: "development_work"})
MERGE (maintenance_work:Object {name: "管护", type: "maintenance_work"})

// 义务
MERGE (duty146:Obligation {description: "负责土地储备的具体实施工作", source_article: "第四十五条"})
MERGE (duty147:Obligation {description: "按照国家规定实行名录制管理", source_article: "第四十五条"})
MERGE (duty148:Obligation {description: "不得承担土地储备相关工作", condition: "未纳入国家名录", source_article: "第四十五条"})

// 关系建立
MERGE (agent51)-[:HAS_DUTY]->(duty146)
MERGE (agent25)-[:HAS_DUTY]->(duty147)
MERGE (agent51)-[:MUST_NOT]->(prohibition7)

MERGE (duty146)-[:IMPLEMENTING]->(land_reserve)
MERGE (duty147)-[:USES_METHOD]->(management2)
MERGE (duty147)-[:MANAGES]->(agent52)

MERGE (prohibition7)-[:CONDITIONED_BY]->(agent52)
MERGE (agent51)-[:ENCOURAGED_TO]->(encourage5)
MERGE (encourage5)-[:TARGETS]->(agent31)
MERGE (encourage5)-[:INVOLVES_WORK]->(development_work)
MERGE (encourage5)-[:INVOLVES_WORK]->(maintenance_work)
MERGE (development_work)-[:RELATED_TO]->(land_use7)
MERGE (maintenance_work)-[:RELATED_TO]->(land_use7)

// 第四十六条
MERGE (art46:Article {number: "第四十六条", full_text: "建设项目施工、地质勘查需要临时使用土地的，由县级以上人民政府自然资源主管部门批准。使用国有土地的，应当与有关自然资源主管部门签订临时使用土地合同；使用农民集体所有土地的，应当与土地所属的农村集体经济组织或者村民委员会签订临时使用土地合同。对原土地使用权人或者土地承包经营权人造成损失的，由签订合同的自然资源主管部门或者农村集体经济组织、村民委员会依法给予补偿，相关补偿费用纳入临时使用土地补偿费。"})
MERGE (art46)-[:PART_OF]->(chapter5)

// 相关主体
MERGE (agent53:Agent {name: "建设项目施工单位", type: "entity"})
MERGE (agent54:Agent {name: "地质勘查单位", type: "entity"})
MERGE (agent55:Agent {name: "村民委员会", type: "organization"})

// 临时用地
MERGE (temp_land_use:Object {name: "临时使用土地", type: "land_use_type"})
MERGE (temp_contract:Object {name: "临时使用土地合同", type: "contract_type"})
MERGE (approval2:Object {name: "临时使用土地批准", type: "approval"})
MERGE (compensation3:Object {name: "临时使用土地补偿费", type: "compensation_type"})

// 合同签订主体
MERGE (contract_party1:Object {name: "自然资源主管部门（国有土地）", type: "contract_party"})
MERGE (contract_party2:Object {name: "农村集体经济组织或村民委员会（集体土地）", type: "contract_party"})

// 义务
MERGE (duty149:Obligation {description: "批准临时使用土地", source_article: "第四十六条"})
MERGE (duty150:Obligation {description: "（国有）签订临时使用土地合同", condition: "使用国有土地", source_article: "第四十六条"})
MERGE (duty151:Obligation {description: "（农民集体）签订临时使用土地合同", condition: "使用农民集体所有土地", source_article: "第四十六条"})
MERGE (duty152:Obligation {description: "依法给予补偿", condition: "对原土地使用权人或者土地承包经营权人造成损失", source_article: "第四十六条"})

// 关系建立
MERGE (agent38)-[:HAS_DUTY]->(duty149)
MERGE (agent39)-[:HAS_DUTY]->(duty149)
MERGE (agent53)-[:HAS_DUTY]->(duty150)
MERGE (agent54)-[:HAS_DUTY]->(duty150)
MERGE (agent53)-[:HAS_DUTY]->(duty151)
MERGE (agent54)-[:HAS_DUTY]->(duty151)
MERGE (agent38)-[:HAS_DUTY]->(duty152)
MERGE (agent39)-[:HAS_DUTY]->(duty152)
MERGE (agent31)-[:HAS_DUTY]->(duty152)
MERGE (agent55)-[:HAS_DUTY]->(duty152)

MERGE (duty149)-[:HAS_AUTHORITY]->(temp_land_use)
MERGE (duty149)-[:GRANTS_APPROVAL]->(approval2)

MERGE (duty150)-[:SIGNS_CONTRACT_WITH]->(contract_party1)
MERGE (duty150)-[:SIGNS_CONTRACT]->(temp_contract)
MERGE (duty151)-[:SIGNS_CONTRACT_WITH]->(contract_party2)
MERGE (duty151)-[:SIGNS_CONTRACT]->(temp_contract)

MERGE (duty152)-[:PAYS_COMPENSATION]->(compensation3)
MERGE (compensation3)-[:RELATED_TO]->(temp_contract)
MERGE (compensation3)-[:COMPENSATES]->(agent28)
MERGE (compensation3)-[:COMPENSATES]->(agent29)