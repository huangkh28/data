// 第六章 监督检查
// 创建第六章节点（确保文档节点已存在）
MATCH (doc:Document {name: "广东省土地管理条例"})
MERGE (chapter6:Chapter {number: "第六章", title: "监督检查"})
MERGE (chapter6)-[:PART_OF]->(doc)

// 第四十七条
MERGE (art47:Article {number: "第四十七条", full_text: "省人民政府建立土地督察制度，对地级以上市人民政府土地利用和土地管理情况进行督察。省人民政府授权的机构进行督察时，有权向有关单位和个人了解督察事项有关情况。有关单位和个人应当支持、协助，如实反映情况，并提供有关资料。被督察的人民政府违反土地管理法律、法规、规章，或者落实国家和省有关土地管理决策不力的，省人民政府授权的机构可以向被督察的人民政府下达督察意见书，被督察的人民政府应当认真组织整改，及时报告整改情况。省人民政府授权的机构可以约谈被督察的人民政府有关负责人，并可以依法向监察机关、任免机关等有关机关提出追究相关责任人责任的建议。"})
MERGE (art47)-[:PART_OF]->(chapter6)

// 主体
MERGE (prov_gov:Agent {name: "省人民政府", type: "government_level"})
MERGE (authorized_institution:Agent {name: "省人民政府授权的机构", type: "institution"})
MERGE (municipal_gov:Agent {name: "地级以上市人民政府", type: "government_level"})
MERGE (relevant_units:Agent {name: "有关单位", type: "entity"})
MERGE (relevant_individuals:Agent {name: "个人", type: "individual"})
MERGE (supervision_target_gov:Agent {name: "被督察的人民政府", type: "government_level"})
MERGE (supervision_target_resp_person:Agent {name: "被督察的人民政府有关负责人", type: "individual"})
MERGE (supervisory_organs:Agent {name: "监察机关、任免机关等有关机关", type: "organization"})

// 制度
MERGE (land_supervision_system:System {name: "土地督察制度", type: "supervision_system", source_article: "第四十七条"})

// 义务
MERGE (duty47_1:Obligation {description: "建立土地督察制度", source_article: "第四十七条"})
MERGE (duty47_2:Obligation {description: "支持、协助督察工作，如实反映情况，并提供有关资料", source_article: "第四十七条"})
MERGE (duty47_3:Obligation {description: "认真组织整改，及时报告整改情况", source_article: "第四十七条"})

// 权限
MERGE (authority47_1:Authority {description: "向有关单位和个人了解督察事项有关情况", source_article: "第四十七条"})
MERGE (authority47_2:Authority {description: "向被督察的人民政府下达督察意见书", source_article: "第四十七条"})
MERGE (authority47_3:Authority {description: "约谈被督察的人民政府有关负责人", source_article: "第四十七条"})
MERGE (authority47_4:Authority {description: "向监察机关、任免机关等有关机关提出追究相关责任人责任的建议", source_article: "第四十七条"})

// 关系建立 - 第四十七条
MERGE (prov_gov)-[:HAS_DUTY]->(duty47_1)
MERGE (prov_gov)-[:ESTABLISHES]->(land_supervision_system)
MERGE (land_supervision_system)-[:SUPERVISES]->(municipal_gov)
MERGE (authorized_institution)-[:HAS_AUTHORITY]->(authority47_1)
MERGE (authorized_institution)-[:HAS_AUTHORITY]->(authority47_2)
MERGE (authorized_institution)-[:HAS_AUTHORITY]->(authority47_3)
MERGE (authorized_institution)-[:HAS_AUTHORITY]->(authority47_4)
MERGE (relevant_units)-[:HAS_DUTY]->(duty47_2)
MERGE (relevant_individuals)-[:HAS_DUTY]->(duty47_2)
MERGE (supervision_target_gov)-[:HAS_DUTY]->(duty47_3)
MERGE (authority47_2)-[:ISSUES_TO]->(supervision_target_gov)
MERGE (authority47_3)-[:INTERVIEWS]->(supervision_target_resp_person)
MERGE (authority47_4)-[:PROPOSES_TO]->(supervisory_organs)

// 将主体与条款关联
MERGE (art47)-[:INVOLVES]->(prov_gov)
MERGE (art47)-[:INVOLVES]->(authorized_institution)
MERGE (art47)-[:INVOLVES]->(municipal_gov)
MERGE (art47)-[:INVOLVES]->(relevant_units)
MERGE (art47)-[:INVOLVES]->(relevant_individuals)
MERGE (art47)-[:INVOLVES]->(supervision_target_gov)
MERGE (art47)-[:INVOLVES]->(supervision_target_resp_person)
MERGE (art47)-[:INVOLVES]->(supervisory_organs)

// 第四十八条
MERGE (art48:Article {number: "第四十八条", full_text: "县级以上人民政府自然资源、农业农村主管部门以及乡镇人民政府应当按照各自职责建立土地巡查制度，运用卫星遥感、无人机航摄、视频监控等手段加强土地违法行测，及时发现并依法制止土地违法行为。各级人民政府应当科学合理配备负责日常土地管理监督检查的工作人员。"})
MERGE (art48)-[:PART_OF]->(chapter6)

// 主体
MERGE (county_above_gov:Agent {name: "县级以上人民政府", type: "government_level"})
MERGE (natural_resources_dept:Agent {name: "自然资源主管部门", type: "department"})
MERGE (agriculture_rural_dept:Agent {name: "农业农村主管部门", type: "department"})
MERGE (township_gov:Agent {name: "乡镇人民政府", type: "government_level"})
MERGE (all_level_gov:Agent {name: "各级人民政府", type: "government_level"})

// 制度与工具
MERGE (land_patrol_system:System {name: "土地巡查制度", type: "supervision_system", source_article: "第四十八条"})
MERGE (satellite_remote_sensing:Object {name: "卫星遥感", type: "monitoring_tool", source_article: "第四十八条"})
MERGE (drone_aerial_photography:Object {name: "无人机航摄", type: "monitoring_tool", source_article: "第四十八条"})
MERGE (video_monitoring:Object {name: "视频监控", type: "monitoring_tool", source_article: "第四十八条"})

// 义务
MERGE (duty48_1:Obligation {description: "按照各自职责建立土地巡查制度", source_article: "第四十八条"})
MERGE (duty48_2:Obligation {description: "运用卫星遥感、无人机航摄、视频监控等手段加强土地违法行为监测", source_article: "第四十八条"})
MERGE (duty48_3:Obligation {description: "及时发现并依法制止土地违法行为", source_article: "第四十八条"})
MERGE (duty48_4:Obligation {description: "科学合理配备负责日常土地管理监督检查的工作人员", source_article: "第四十八条"})

// 关系建立 - 第四十八条
MERGE (natural_resources_dept)-[:HAS_DUTY]->(duty48_1)
MERGE (agriculture_rural_dept)-[:HAS_DUTY]->(duty48_1)
MERGE (township_gov)-[:HAS_DUTY]->(duty48_1)
MERGE (duty48_1)-[:ESTABLISHES]->(land_patrol_system)

MERGE (natural_resources_dept)-[:HAS_DUTY]->(duty48_2)
MERGE (agriculture_rural_dept)-[:HAS_DUTY]->(duty48_2)
MERGE (township_gov)-[:HAS_DUTY]->(duty48_2)
MERGE (duty48_2)-[:USES_TOOL]->(satellite_remote_sensing)
MERGE (duty48_2)-[:USES_TOOL]->(drone_aerial_photography)
MERGE (duty48_2)-[:USES_TOOL]->(video_monitoring)

MERGE (natural_resources_dept)-[:HAS_DUTY]->(duty48_3)
MERGE (agriculture_rural_dept)-[:HAS_DUTY]->(duty48_3)
MERGE (township_gov)-[:HAS_DUTY]->(duty48_3)

MERGE (all_level_gov)-[:HAS_DUTY]->(duty48_4)

// 将主体与条款关联
MERGE (art48)-[:INVOLVES]->(natural_resources_dept)
MERGE (art48)-[:INVOLVES]->(agriculture_rural_dept)
MERGE (art48)-[:INVOLVES]->(township_gov)
MERGE (art48)-[:INVOLVES]->(all_level_gov)

// 第四十九条
MERGE (art49:Article {number: "第四十九条", full_text: "省人民政府自然资源主管部门应当建立重大土地违法案件督办制度。地级以上市人民政府自然资源主管部门未按照要求和时限办理督办案件的，省人民政府自然资源主管部门可以责令其限期整改；省人民政府自然资源主管部门经省人民政府同意，可以在整改期间暂停或者责令暂停违法案件所在地有关农用地转用、征收土地的审批。"})
MERGE (art49)-[:PART_OF]->(chapter6)

// 主体
MERGE (prov_natural_resources_dept:Agent {name: "省人民政府自然资源主管部门", type: "department"})

// 制度
MERGE (major_violation_case_supervision_system:System {name: "重大土地违法案件督办制度", type: "supervision_system", source_article: "第四十九条"})

// 义务与权限
MERGE (duty49_1:Obligation {description: "建立重大土地违法案件督办制度", source_article: "第四十九条"})
MERGE (authority49_1:Authority {description: "责令限期整改", source_article: "第四十九条"})
MERGE (authority49_2:Authority {description: "暂停或者责令暂停违法案件所在地有关农用地转用、征收土地的审批", source_article: "第四十九条"})

// 相关手续
MERGE (farmland_conversion_approval:Object {name: "农用地转用审批", type: "approval", source_article: "第四十九条"})
MERGE (land_expropriation_approval:Object {name: "征收土地审批", type: "approval", source_article: "第四十九条"})

// 适用条件
MERGE (condition49_1:Object {name: "未按照要求和时限办理督办案件", type: "condition", source_article: "第四十九条"})
MERGE (condition49_2:Object {name: "整改期间，经省人民政府同意", type: "condition", source_article: "第四十九条"})

// 关系建立 - 第四十九条
MERGE (prov_natural_resources_dept)-[:HAS_DUTY]->(duty49_1)
MERGE (duty49_1)-[:ESTABLISHES]->(major_violation_case_supervision_system)
MERGE (prov_natural_resources_dept)-[:HAS_AUTHORITY]->(authority49_1)
MERGE (prov_natural_resources_dept)-[:HAS_AUTHORITY]->(authority49_2)
MERGE (authority49_1)-[:APPLIES_WHEN]->(condition49_1)
MERGE (authority49_2)-[:APPLIES_WHEN]->(condition49_2)
MERGE (authority49_2)-[:SUSPENDS]->(farmland_conversion_approval)
MERGE (authority49_2)-[:SUSPENDS]->(land_expropriation_approval)

// 将主体与条款关联
MERGE (art49)-[:INVOLVES]->(prov_natural_resources_dept)

// 第五十条
MERGE (art50:Article {number: "第五十条", full_text: "县级以上人民政府自然资源主管部门在调查处理土地违法案件期间，有权暂停或者责令暂停办理与该违法案件相关的土地审批、登记等手续。县级以上人民政府可以根保护、土地利用计划执行、土地节约集约利用、土地利用秩序等情况，按照规定相应奖励或者扣减下级人民政府土地利用年度计划指标。"})
MERGE (art50)-[:PART_OF]->(chapter6)

// 主体
MERGE (county_above_natural_resources_dept:Agent {name: "县级以上人民政府自然资源主管部门", type: "department"})
MERGE (lower_gov:Agent {name: "下级人民政府", type: "government_level"})

// 权限
MERGE (authority50_1:Authority {description: "暂停或者责令暂停办理与违法案件相关的土地审批、登记等手续", source_article: "第五十条"})
MERGE (authority50_2:Authority {description: "奖励或者扣减下级人民政府土地利用年度计划指标", source_article: "第五十条"})

// 相关手续
MERGE (land_approval:Object {name: "土地审批", type: "procedure", source_article: "第五十条"})
MERGE (land_registration:Object {name: "土地登记", type: "procedure", source_article: "第五十条"})
MERGE (land_use_annual_plan:Object {name: "土地利用年度计划指标", type: "land_use_plan", source_article: "第五十条"})

// 适用条件
MERGE (condition50_1:Object {name: "调查处理土地违法案件期间", type: "condition", source_article: "第五十条"})
MERGE (condition50_2:Object {name: "耕地保护、土地利用计划执行、土地节约集约利用、土地利用秩序等情况", type: "condition", source_article: "第五十条"})

// 关系建立 - 第五十条
MERGE (county_above_natural_resources_dept)-[:HAS_AUTHORITY]->(authority50_1)
MERGE (authority50_1)-[:SUSPENDS]->(land_approval)
MERGE (authority50_1)-[:SUSPENDS]->(land_registration)
MERGE (authority50_1)-[:APPLIES_WHEN]->(condition50_1)

MERGE (county_above_gov)-[:HAS_AUTHORITY]->(authority50_2)
MERGE (authority50_2)-[:ADJUSTS]->(land_use_annual_plan)
MERGE (authority50_2)-[:APPLIES_TO]->(lower_gov)
MERGE (authority50_2)-[:BASED_ON]->(condition50_2)

// 将主体与条款关联
MERGE (art50)-[:INVOLVES]->(county_above_natural_resources_dept)
MERGE (art50)-[:INVOLVES]->(county_above_gov)
MERGE (art50)-[:INVOLVES]->(lower_gov)

// 第五十一条
MERGE (art51:Article {number: "第五十一条", full_text: "县级以上人民政府应当将国土空间规划、土地利用年度计划、耕地保护责任制等执行情况列为国民经济和社会发展计划执行情况、国有自然资源管理情况的内容，依法向本级人民代表大会或者其常务委员会报告。"})
MERGE (art51)-[:PART_OF]->(chapter6)

// 主体
MERGE (people_congress:Agent {name: "本级人民代表大会", type: "government_level"})
MERGE (standing_committee:Agent {name: "常务委员会", type: "government_level"})

// 报告内容
MERGE (spatial_planning_execution:Object {name: "国土空间规划执行情况", type: "report_content", source_article: "第五十一条"})
MERGE (land_use_plan_execution:Object {name: "土地利用年度计划执行情况", type: "report_content", source_article: "第五十一条"})
MERGE (farmland_protection_resp_sys:Object {name: "耕地保护责任制执行情况", type: "report_content", source_article: "第五十一条"})
MERGE (economic_social_development:Object {name: "国民经济和社会发展计划执行情况", type: "report_content", source_article: "第五十一条"})
MERGE (state_natural_resources_mgmt:Object {name: "国有自然资源管理情况", type: "report_content", source_article: "第五十一条"})

// 义务
MERGE (duty51_1:Obligation {description: "将国土空间规划、土地利用年度计划、耕地保护责任制等执行情况列为国民经济和社会发展计划执行情况、国有自然资源管理情况的内容，依法向本级人民代表大会或者其常务委员会报告", source_article: "第五十一条"})

// 关系建立 - 第五十一条
MERGE (county_above_gov)-[:HAS_DUTY]->(duty51_1)
MERGE (duty51_1)-[:INCLUDES_REPORT_CONTENT]->(spatial_planning_execution)
MERGE (duty51_1)-[:INCLUDES_REPORT_CONTENT]->(land_use_plan_execution)
MERGE (duty51_1)-[:INCLUDES_REPORT_CONTENT]->(farmland_protection_resp_sys)
MERGE (duty51_1)-[:REPORTS_TO]->(people_congress)
MERGE (duty51_1)-[:REPORTS_TO]->(standing_committee)

// 将主体与条款关联
MERGE (art51)-[:INVOLVES]->(county_above_gov)
MERGE (art51)-[:INVOLVES]->(people_congress)
MERGE (art51)-[:INVOLVES]->(standing_committee)