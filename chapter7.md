// 创建文档节点（如果尚未创建）
// 创建第七章节点
MATCH (doc:Document {name: "广东省土地管理条例"})
MERGE (chapter7:Chapter {number: "第七章", title: "法律责任"})
MERGE (chapter7)-[:PART_OF]->(doc)


// 第五十二条
MERGE (art52:Article {number: "第五十二条", full_text: "未经批准或者采取欺骗手段骗取批准，非法占用土地的，由县级以上人民政府自然资源主管部门责令退还非法占用的土地，对违反国土空间规划擅自占用建设用地、未利用地的，限期拆除在非法占用的土地上新建的建筑物和其他设施，恢复土地原状，对符合国土空间规划的，没收在非法占用的土地上新建的建筑物和其他设施，可以并处非法占用土地每平方米一百元以上一千元以下的罚款；对非法占用土地单位的直接负责的主管人员和其他直接责任人员，依法给予处分；构成犯罪的，依法追究刑事责任。"})
MERGE (art52)-[:PART_OF]->(chapter7)

// 主体
MERGE (county_above_natural_resources_dept:Agent {name: "县级以上人民政府自然资源主管部门", type: "department"})
MERGE (illegal_land_occupier:Agent {name: "非法占用土地单位", type: "entity"})
MERGE (directly_responsible_personnel:Agent {name: "直接负责的主管人员和其他直接责任人员", type: "individual"})

// 义务与禁止
MERGE (prohibition52_1:Prohibition {description: "未经批准非法占用土地", source_article: "第五十二条"})
MERGE (prohibition52_2:Prohibition {description: "采取欺骗手段骗取批准占用土地", source_article: "第五十二条"})

// 处罚
MERGE (penalty52_1:Penalty {description: "责令退还非法占用的土地", source_article: "第五十二条"})
MERGE (penalty52_2:Penalty {description: "限期拆除在非法占用的土地上新建的建筑物和其他设施，恢复土地原状", condition: "违反国土空间规划擅自占用建设用地、未利用地", source_article: "第五十二条"})
MERGE (penalty52_3:Penalty {description: "没收在非法占用的土地上新建的建筑物和其他设施", condition: "符合国土空间规划", source_article: "第五十二条"})
MERGE (penalty52_4:Penalty {description: "处以非法占用土地每平方米一百元以上一千元以下的罚款", source_article: "第五十二条"})
MERGE (penalty52_5:Penalty {description: "依法给予处分", target: "直接负责的主管人员和其他直接责任人员", source_article: "第五十四条"})
MERGE (penalty52_6:Penalty {description: "依法追究刑事责任", condition: "构成犯罪", source_article: "第五十二条、第五十四条"})

// 条件
MERGE (condition52_1:Object {name: "违反国土空间规划擅自占用建设用地、未利用地", type: "condition", source_article: "第五十二条"})
MERGE (condition52_2:Object {name: "符合国土空间规划"})
SET condition52_2.type = "condition", condition52_2.source_article = "第四十三条、第五十二条"
MERGE (condition52_3:Object {name: "构成犯罪", type: "condition", source_article: "第五十二条"})

// 关系建立 - 第五十二条
MERGE (county_above_natural_resources_dept)-[:HAS_AUTHORITY]->(authority52_1:Authority {description: "责令退还非法占用的土地", source_article: "第五十二条"})
MERGE (county_above_natural_resources_dept)-[:HAS_AUTHORITY]->(authority52_2:Authority {description: "限期拆除在非法占用的土地上新建的建筑物和其他设施，恢复土地原状", source_article: "第五十二条", condition: "违反国土空间规划擅自占用建设用地、未利用地"})
MERGE (county_above_natural_resources_dept)-[:HAS_AUTHORITY]->(authority52_3:Authority {description: "没收在非法占用的土地上新建的建筑物和其他设施", source_article: "第五十二条", condition: "符合国土空间规划"})
MERGE (county_above_natural_resources_dept)-[:HAS_AUTHORITY]->(authority52_4:Authority {description: "处以非法占用土地每平方米一百元以上一千元以下的罚款", source_article: "第五十二条"})

MERGE (authority52_2)-[:APPLIES_WHEN]->(condition52_1)
MERGE (authority52_3)-[:APPLIES_WHEN]->(condition52_2)
MERGE (authority52_4)-[:HAS_PENALTY]->(penalty52_4)

MERGE (illegal_land_occupier)-[:SUBJECT_TO]->(penalty52_1)
MERGE (illegal_land_occupier)-[:SUBJECT_TO]->(penalty52_2)
MERGE (illegal_land_occupier)-[:SUBJECT_TO]->(penalty52_3)
MERGE (illegal_land_occupier)-[:SUBJECT_TO]->(penalty52_4)
MERGE (directly_responsible_personnel)-[:SUBJECT_TO]->(penalty52_5)
MERGE (directly_responsible_personnel)-[:SUBJECT_TO]->(penalty52_6)

MERGE (penalty52_2)-[:APPLIES_WHEN]->(condition52_1)
MERGE (penalty52_3)-[:APPLIES_WHEN]->(condition52_2)
MERGE (penalty52_6)-[:APPLIES_WHEN]->(condition52_3)

// 将主体与条款关联
MERGE (art52)-[:INVOLVES]->(county_above_natural_resources_dept)
MERGE (art52)-[:INVOLVES]->(illegal_land_occupier)
MERGE (art52)-[:INVOLVES]->(directly_responsible_personnel)

// 第五十三条
MERGE (art53:Article {number: "第五十三条", full_text: "用地单位和个人未按照规定足额预存土地复垦费用的，由县级以上人民政府自然资源主管部门责令限期改正；逾期不改正的，处十万元以上五十万元以下的罚款。"})
MERGE (art53)-[:PART_OF]->(chapter7)

// 主体
MERGE (land_user_unit:Agent {name: "用地单位", type: "entity"})
MERGE (land_user_individual:Agent {name: "个人", type: "individual"})

// 义务
MERGE (duty53_1:Obligation {description: "按照规定足额预存土地复垦费用", source_article: "第五十三条"})

// 处罚
MERGE (penalty53_1:Penalty {description: "责令限期改正", source_article: "第五十三条"})
MERGE (penalty53_2:Penalty {description: "处十万元以上五十万元以下的罚款", condition: "逾期不改正", source_article: "第五十三条"})

// 条件
MERGE (condition53_1:Object {name: "逾期不改正", type: "condition", source_article: "第五十三条"})

// 关系建立 - 第五十三条
MERGE (county_above_natural_resources_dept)-[:HAS_AUTHORITY]->(authority53_1:Authority {description: "责令限期改正", source_article: "第五十三条"})
MERGE (county_above_natural_resources_dept)-[:HAS_AUTHORITY]->(authority53_2:Authority {description: "处十万元以上五十万元以下的罚款", source_article: "第五十三条", condition: "逾期不改正"})

MERGE (authority53_2)-[:APPLIES_WHEN]->(condition53_1)

MERGE (land_user_unit)-[:HAS_DUTY]->(duty53_1)
MERGE (land_user_individual)-[:HAS_DUTY]->(duty53_1)
MERGE (land_user_unit)-[:SUBJECT_TO]->(penalty53_1)
MERGE (land_user_individual)-[:SUBJECT_TO]->(penalty53_1)
MERGE (land_user_unit)-[:SUBJECT_TO]->(penalty53_2)
MERGE (land_user_individual)-[:SUBJECT_TO]->(penalty53_2)

// 将主体与条款关联
MERGE (art53)-[:INVOLVES]->(county_above_natural_resources_dept)
MERGE (art53)-[:INVOLVES]->(land_user_unit)
MERGE (art53)-[:INVOLVES]->(land_user_individual)

// 第五十四条
MERGE (art54:Article {number: "第五十四条", full_text: "各级人民政府及自然资源、农业农村等有关部门有下列情形之一，依照法律、法规和国家规定追究责任，对直接负责的主管人员和其他直接责任人员依法给予处分；构成犯罪的，依法追究刑事责任： （一）违反法定权限、程序擅自批准或者修改国土空间规划的； （二）违反法定权限、程序或者不按照国土空间规划确定的土地用途批准使用土地的； （三）违反法定权限、程序进行土地征收的； （四）侵占、挪用征收土地补偿费用和其他有关费用的； （五）未依法依规履行土地监督检查职责的； （六）拒绝、阻碍土地督察机构依法执行职务的； （七）其他玩忽职守、滥用职权、徇私舞弊的情形。"})
MERGE (art54)-[:PART_OF]->(chapter7)

// 主体
MERGE (all_level_gov:Agent {name: "各级人民政府", type: "government_level"})
MERGE (natural_resources_dept:Agent {name: "自然资源主管部门", type: "department"})
MERGE (agriculture_rural_dept:Agent {name: "农业农村主管部门", type: "department"})
MERGE (directly_resp_personnel:Agent {name: "直接负责的主管人员和其他直接责任人员", type: "individual"})
MERGE (land_supervision_org:Agent {name: "土地督察机构", type: "institution"})

// 禁止行为
MERGE (prohibition54_1:Prohibition {description: "违反法定权限、程序擅自批准或者修改国土空间规划", source_article: "第五十四条"})
MERGE (prohibition54_2:Prohibition {description: "违反法定权限、程序或者不按照国土空间规划确定的土地用途批准使用土地", source_article: "第五十四条"})
MERGE (prohibition54_3:Prohibition {description: "违反法定权限、程序进行土地征收", source_article: "第五十四条"})
MERGE (prohibition54_4:Prohibition {description: "侵占、挪用征收土地补偿费用和其他有关费用", source_article: "第五十四条"})
MERGE (prohibition54_5:Prohibition {description: "未依法依规履行土地监督检查职责", source_article: "第五十四条"})
MERGE (prohibition54_6:Prohibition {description: "拒绝、阻碍土地督察机构依法执行职务", source_article: "第五十四条"})
MERGE (prohibition54_7:Prohibition {description: "玩忽职守、滥用职权、徇私舞弊", source_article: "第五十四条"})

// 处罚
MERGE (penalty54_1:Penalty {description: "依照法律、法规和国家规定追究责任", source_article: "第五十四条"})

// 关系建立 - 第五十四条
MERGE (all_level_gov)-[:PROHIBITED_FROM]->(prohibition54_1)
MERGE (all_level_gov)-[:PROHIBITED_FROM]->(prohibition54_2)
MERGE (all_level_gov)-[:PROHIBITED_FROM]->(prohibition54_3)
MERGE (all_level_gov)-[:PROHIBITED_FROM]->(prohibition54_4)
MERGE (all_level_gov)-[:PROHIBITED_FROM]->(prohibition54_5)
MERGE (all_level_gov)-[:PROHIBITED_FROM]->(prohibition54_6)

MERGE (natural_resources_dept)-[:PROHIBITED_FROM]->(prohibition54_1)
MERGE (natural_resources_dept)-[:PROHIBITED_FROM]->(prohibition54_2)
MERGE (natural_resources_dept)-[:PROHIBITED_FROM]->(prohibition54_3)
MERGE (natural_resources_dept)-[:PROHIBITED_FROM]->(prohibition54_4)
MERGE (natural_resources_dept)-[:PROHIBITED_FROM]->(prohibition54_5)
MERGE (natural_resources_dept)-[:PROHIBITED_FROM]->(prohibition54_6)

MERGE (agriculture_rural_dept)-[:PROHIBITED_FROM]->(prohibition54_5)
MERGE (directly_resp_personnel)-[:SUBJECT_TO]->(penalty54_1)
MERGE (directly_resp_personnel)-[:SUBJECT_TO]->(penalty52_5)
MERGE (directly_resp_personnel)-[:SUBJECT_TO]->(penalty52_6)

// 将主体与条款关联
MERGE (art54)-[:INVOLVES]->(all_level_gov)
MERGE (art54)-[:INVOLVES]->(natural_resources_dept)
MERGE (art54)-[:INVOLVES]->(agriculture_rural_dept)
MERGE (art54)-[:INVOLVES]->(directly_resp_personnel)
MERGE (art54)-[:INVOLVES]->(land_supervision_org)