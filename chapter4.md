// 第四章
// 创建第四章节点（确保文档节点已存在）
MATCH (doc:Document {name: "广东省土地管理条例"})
MERGE (chapter4:Chapter {number: "第四章", title: "农用地转用和土地征收"})
MERGE (chapter4)-[:PART_OF]->(doc)

// 第二十四条
MERGE (art24:Article {number: "第二十四条", full_text: "建设占用土地涉及农用地转为建设用地的，应当办理农用地转用审批手续；涉及征收土地的，应当同时提出征收土地申请，报有批准权的人民政府批准。农用地转用、征收土地依法由省人民政府批准或者审核上报的，应当先经地级以上市人民政府审核。"})
MERGE (art24)-[:PART_OF]->(chapter4)

// 土地类型
MERGE (land_type1:Object {name: "农用地", type: "land_type", source_article: "第二十四条"})
MERGE (land_type2:Object {name: "建设用地", type: "land_type", source_article: "第二十四条"})

// 审批主体
MERGE (agent22:Agent {name: "有批准权的人民政府", type: "government_level"})
MERGE (agent23:Agent {name: "省人民政府", type: "government_level"})
MERGE (agent24:Agent {name: "地级以上市人民政府", type: "government_level"})

// 审批程序
MERGE (procedure3:Object {name: "农用地转用审批手续", type: "procedure", source_article: "第二十四条"})
MERGE (procedure4:Object {name: "征收土地申请", type: "procedure", source_article: "第二十四条"})
MERGE (procedure5:Object {name: "审核程序", type: "procedure", source_article: "第二十四条"})

// 义务
MERGE (duty53:Obligation {description: "办理农用地转用审批手续", source_article: "第二十四条"})
MERGE (duty54:Obligation {description: "提出征收土地申请", source_article: "第二十四条"})
MERGE (duty55:Obligation {description: "先经地级以上市人民政府审核", condition: "农用地转用、征收土地依法由省人民政府批准或者审核上报", source_article: "第二十四条"})

// 关系建立
MERGE (agent22)-[:HAS_AUTHORITY]->(procedure3)
MERGE (agent22)-[:HAS_AUTHORITY]->(procedure4)
MERGE (agent23)-[:HAS_DUTY]->(duty55)
MERGE (agent24)-[:PERFORMS]->(procedure5)

MERGE (procedure3)-[:CONVERTS]->(land_type1)
MERGE (procedure3)-[:TO]->(land_type2)
MERGE (procedure4)-[:INVOLVES]->(land_type1)

MERGE (duty53)-[:FOLLOWS_PROCEDURE]->(procedure3)
MERGE (duty54)-[:FOLLOWS_PROCEDURE]->(procedure4)
MERGE (duty55)-[:FOLLOWS_PROCEDURE]->(procedure5)

MERGE (procedure5)-[:REQUIRED_BEFORE]->(procedure3)
MERGE (procedure5)-[:REQUIRED_BEFORE]->(procedure4)
MERGE (procedure5)-[:PERFORMED_BY]->(agent24)
MERGE (procedure5)-[:REQUIRED_FOR]->(agent23)

MERGE (art24)-[:REGULATES_PROCEDURE]->(procedure3)
MERGE (art24)-[:REGULATES_PROCEDURE]->(procedure4)
MERGE (art24)-[:INVOLVES]->(agent22)
MERGE (art24)-[:INVOLVES]->(agent23)
MERGE (art24)-[:INVOLVES]->(agent24)

// 第二十五条
MERGE (art25:Article {number: "第二十五条", full_text: "建设占用未利用地的，应当办理未利用地转用审批手续，由地级以上市人民政府批准；同时占用农用地和未利用地的，由农用地转用批准机关一并审批。"})
MERGE (art25)-[:PART_OF]->(chapter4)


MERGE (land_type3:Object {name: "审批占用未利用地", type: "land_type", source_article: "第二十五条"})
MERGE (land_type4:Object {name: "审批同时占用农用地和未利用地的", type: "land_type", source_article: "第二十五条"})
MERGE (agent56:Agent {name: "农用地转用批准机关", type: "government_level"})

// 审批程序
MERGE (procedure6:Object {name: "未利用地转用审批手续", type: "procedure", source_article: "第二十五条"})

// 义务
MERGE (duty56:Obligation {description: "办理未利用地转用审批手续", source_article: "第二十五条"})

// 关系建立
MERGE (agent24)-[:HAS_AUTHORITY]->(procedure6)
MERGE (agent24)-[:HAS_AUTHORITY]->(land_type3)
MERGE (duty56)-[:FOLLOWS_PROCEDURE]->(procedure6)
MERGE (procedure6)-[:CONVERTS]->(land_type3)
MERGE (procedure6)-[:TO]->(land_type2)
MERGE (agent56)-[:HAS_AUTHORITY]->(land_type4)

// 一并审批机制
MERGE (mechanism3:Object {name: "一并审批机制", type: "mechanism", source_article: "第二十五条"})
MERGE (mechanism3)-[:HANDLES]->(procedure3)
MERGE (mechanism3)-[:HANDLES]->(procedure6)
MERGE (procedure3)-[:APPROVING_AUTHORITY_HANDLES]->(mechanism3)

MERGE (art25)-[:REGULATES_PROCEDURE]->(procedure6)
MERGE (art25)-[:INVOLVES]->(agent24)
MERGE (art25)-[:INVOLVES]->(agent56)
MERGE (art25)-[:USES_MECHANISM]->(mechanism3)

// 第二十六条
MERGE (art26:Article {number: "第二十六条", full_text: "为了公共利益的需要征收土地的，县级以上人民政府应当依法完成征收土地预公告、土地现状调查及结果确认、社会稳定风险评估、征地补偿安置公告、征地补偿登记、征地补偿安置协议签订等前期工作后，方可提出征收土地申请。涉及成片开发建设需要征收土地的，应当编制土地征收成片开发方案。"})
MERGE (art26)-[:PART_OF]->(chapter4)

// 征收主体
MERGE (agent25:Agent {name: "县级以上人民政府", type: "government_level"})

// 征收前期工作
MERGE (task1:Object {name: "征收土地预公告", type: "task", source_article: "第二十六条"})
MERGE (task2:Object {name: "土地现状调查及结果确认", type: "task", source_article: "第二十六条"})
MERGE (task3:Object {name: "社会稳定风险评估", type: "task", source_article: "第二十六条"})
MERGE (task4:Object {name: "征地补偿安置公告", type: "task", source_article: "第二十六条"})
MERGE (task5:Object {name: "征地补偿登记", type: "task", source_article: "第二十六条"})
MERGE (task6:Object {name: "征地补偿安置协议签订", type: "task", source_article: "第二十六条"})

// 征收目的
MERGE (purpose1:Object {name: "公共利益需要", type: "purpose", source_article: "第二十六条"})

// 特殊征收类型
MERGE (plan4:Object {name: "土地征收成片开发方案", type: "plan", source_article: "第二十六条"})
MERGE (condition3:Object {name: "成片开发建设需要", type: "condition", source_article: "第二十六条"})

// 征收前置条件
MERGE (condition4:Object {name: "完成前期工作", type: "condition", source_article: "第二十六条"})

// 义务
MERGE (duty57:Obligation {description: "完成征收土地前期工作", source_article: "第二十六条"})
MERGE (duty58:Obligation {description: "编制土地征收成片开发方案", condition: "涉及成片开发建设需要征收土地", source_article: "第二十六条"})

// 关系建立
MERGE (agent25)-[:HAS_DUTY]->(duty57)
MERGE (agent25)-[:HAS_DUTY]->(duty58)

MERGE (duty57)-[:INCLUDES_TASK]->(task1)
MERGE (duty57)-[:INCLUDES_TASK]->(task2)
MERGE (duty57)-[:INCLUDES_TASK]->(task3)
MERGE (duty57)-[:INCLUDES_TASK]->(task4)
MERGE (duty57)-[:INCLUDES_TASK]->(task5)
MERGE (duty57)-[:INCLUDES_TASK]->(task6)

MERGE (duty57)-[:REQUIRED_BEFORE]->(procedure4)
MERGE (procedure4)-[:REQUIRES_CONDITION]->(condition4)

MERGE (task1)-[:SERVES_PURPOSE]->(purpose1)
MERGE (task2)-[:SERVES_PURPOSE]->(purpose1)
MERGE (task3)-[:SERVES_PURPOSE]->(purpose1)
MERGE (task4)-[:SERVES_PURPOSE]->(purpose1)
MERGE (task5)-[:SERVES_PURPOSE]->(purpose1)
MERGE (task6)-[:SERVES_PURPOSE]->(purpose1)

MERGE (duty58)-[:REQUIRED_WHEN]->(condition3)
MERGE (duty58)-[:CREATES_PLAN]->(plan4)
MERGE (plan4)-[:REQUIRED_FOR]->(procedure4)

MERGE (art26)-[:INVOLVES]->(agent25)
MERGE (art26)-[:REGULATES_PROCEDURE]->(procedure4)
MERGE (art26)-[:DEFINES_TASK]->(task1)
MERGE (art26)-[:DEFINES_TASK]->(task2)
MERGE (art26)-[:DEFINES_TASK]->(task3)
MERGE (art26)-[:DEFINES_TASK]->(task4)
MERGE (art26)-[:DEFINES_TASK]->(task5)
MERGE (art26)-[:DEFINES_TASK]->(task6)

// 第二十七条
MERGE (art27:Article {number: "第二十七条", full_text: "征收土地应当依法预公告，采用书面张贴、网站公开、信息推送或者上户送达等多种有利于社会公众知晓的方式，在拟征收土地所在的乡镇和村、村民小组范围内发布，预公告时间不少于十个工作日，并采取拍照、录像、公证等方式留存记录。"})
MERGE (art27)-[:PART_OF]->(chapter4)

// 公告方式
MERGE (method6:Object {name: "书面张贴", type: "announcement_method", source_article: "第二十七条"})
MERGE (method7:Object {name: "网站公开", type: "announcement_method", source_article: "第二十七条"})
MERGE (method8:Object {name: "信息推送", type: "announcement_method", source_article: "第二十七条"})
MERGE (method9:Object {name: "上户送达", type: "announcement_method", source_article: "第二十七条"})

// 公告范围
MERGE (scope1:Object {name: "乡镇和村、村民小组范围", type: "announcement_scope", source_article: "第二十七条"})

// 公告要求
MERGE (requirement5:Object {name: "预公告时间不少于十个工作日", type: "time_requirement", source_article: "第二十七条"})
MERGE (requirement6:Object {name: "采取拍照、录像、公证等方式留存记录", type: "record_requirement", source_article: "第二十七条、第三十条、第三十四条"})

// 义务
MERGE (duty59:Obligation {description: "依法进行征收土地预公告", source_article: "第二十七条"})
MERGE (duty60:Obligation {description: "采用多种有利于社会公众知晓的方式发布预公告", source_article: "第二十七条"})
MERGE (duty61:Obligation {description: "在规定范围内发布预公告", source_article: "第二十七条"})
MERGE (duty62:Obligation {description: "确保预公告时间不少于十个工作日", source_article: "第二十七条"})

// 关系建立
MERGE (agent25)-[:HAS_DUTY]->(duty59)
MERGE (agent25)-[:HAS_DUTY]->(duty60)
MERGE (agent25)-[:HAS_DUTY]->(duty61)
MERGE (agent25)-[:HAS_DUTY]->(duty62)
MERGE (agent25)-[:HAS_DUTY]->(requirement6)

MERGE (duty59)-[:INCLUDES_TASK]->(task1)
MERGE (duty60)-[:USES_METHOD]->(method6)
MERGE (duty60)-[:USES_METHOD]->(method7)
MERGE (duty60)-[:USES_METHOD]->(method8)
MERGE (duty60)-[:USES_METHOD]->(method9)

MERGE (duty61)-[:APPLIES_TO_SCOPE]->(scope1)
MERGE (duty62)-[:MEETS_REQUIREMENT]->(requirement5)

MERGE (task1)-[:USES_METHOD]->(method6)
MERGE (task1)-[:USES_METHOD]->(method7)
MERGE (task1)-[:USES_METHOD]->(method8)
MERGE (task1)-[:USES_METHOD]->(method9)
MERGE (task1)-[:APPLIES_TO_SCOPE]->(scope1)
MERGE (task1)-[:HAS_TIME_REQUIREMENT]->(requirement5)
MERGE (task1)-[:HAS_RECORD_REQUIREMENT]->(requirement6)

MERGE (art27)-[:DEFINES_TASK]->(task1)
MERGE (art27)-[:INVOLVES]->(agent25)

// 第二十八条
MERGE (art28:Article {number: "第二十八条", full_text: "土地现状调查由县级以上人民政府组织有关部门或者乡镇人民政府开展。调查结果应当由拟征收土地的所有权人、使用权人予以确认。个别土地所有权人、使用权人因客观原因无法确认或者拒不确认的，有关部门或者乡镇人民政府应当在调查结果中注明原因，对调查结果采取见证、公证等方式留存记录，并在拟征收土地所在的乡镇和村、村民小组范围内公示，时间不少于十个工作日。公示期间有异议的，应当及时核查处理。"})
MERGE (art28)-[:PART_OF]->(chapter4)

// 调查主体
MERGE (agent26:Agent {name: "有关部门", type: "department"})
MERGE (agent27:Agent {name: "乡镇人民政府", type: "government_level"})

// 调查对象
MERGE (agent28:Agent {name: "土地所有权人", type: "rights_holder"})
MERGE (agent29:Agent {name: "土地使用权人", type: "rights_holder"})

// 调查方法
MERGE (method10:Object {name: "见证", type: "record_method", source_article: "第二十八条"})
MERGE (method11:Object {name: "公证", type: "record_method", source_article: "第二十八条"})

// 公示要求
MERGE (requirement7:Object {name: "公示时间不少于十个工作日", type: "time_requirement", source_article: "第二十八条"})
MERGE (requirement8:Object {name: "及时核查处理异议", type: "handling_requirement", source_article: "第二十八条"})

// 特殊情况
MERGE (exception4:Object {name: "因客观原因无法确认", type: "exception_condition", source_article: "第二十八条"})
MERGE (exception5:Object {name: "拒不确认", type: "exception_condition", source_article: "第二十八条"})

// 义务
MERGE (duty64:Obligation {description: "组织开展土地现状调查", source_article: "第二十八条"})
MERGE (duty65:Obligation {description: "确认调查结果", source_article: "第二十八条"})
MERGE (duty66:Obligation {description: "在调查结果中注明无法确认或拒不确认的原因", condition: "个别土地所有权人、使用权人因客观原因无法确认或者拒不确认", source_article: "第二十八条"})
MERGE (duty67:Obligation {description: "对调查结果采取见证、公证等方式留存记录", condition: "个别土地所有权人、使用权人因客观原因无法确认或者拒不确认", source_article: "第二十八条"})
MERGE (duty68:Obligation {description: "在规定范围内公示调查结果", condition: "个别土地所有权人、使用权人因客观原因无法确认或者拒不确认", source_article: "第二十八条"})
MERGE (duty69:Obligation {description: "及时核查处理公示期间的异议", source_article: "第二十八条"})

// 关系建立
MERGE (agent25)-[:HAS_DUTY]->(duty64)
MERGE (agent26)-[:PARTICIPATES_IN]->(duty64)
MERGE (agent27)-[:PARTICIPATES_IN]->(duty64)

MERGE (agent28)-[:HAS_DUTY]->(duty65)
MERGE (agent29)-[:HAS_DUTY]->(duty65)

MERGE (agent26)-[:HAS_DUTY]->(duty66)
MERGE (agent27)-[:HAS_DUTY]->(duty66)
MERGE (agent26)-[:HAS_DUTY]->(duty67)
MERGE (agent27)-[:HAS_DUTY]->(duty67)
MERGE (agent26)-[:HAS_DUTY]->(duty68)
MERGE (agent27)-[:HAS_DUTY]->(duty68)
MERGE (agent26)-[:HAS_DUTY]->(duty69)
MERGE (agent27)-[:HAS_DUTY]->(duty69)

MERGE (duty64)-[:INCLUDES_TASK]->(task2)
MERGE (task2)-[:INVOLVES]->(agent28)
MERGE (task2)-[:INVOLVES]->(agent29)

MERGE (duty66)-[:TRIGGERED_BY]->(exception4)
MERGE (duty66)-[:TRIGGERED_BY]->(exception5)
MERGE (duty67)-[:TRIGGERED_BY]->(exception4)
MERGE (duty67)-[:TRIGGERED_BY]->(exception5)
MERGE (duty68)-[:TRIGGERED_BY]->(exception4)
MERGE (duty68)-[:TRIGGERED_BY]->(exception5)

MERGE (duty67)-[:USES_METHOD]->(method10)
MERGE (duty67)-[:USES_METHOD]->(method11)

MERGE (duty68)-[:APPLIES_TO_SCOPE]->(scope1)
MERGE (duty68)-[:MEETS_REQUIREMENT]->(requirement7)

MERGE (duty69)-[:MEETS_REQUIREMENT]->(requirement8)

MERGE (task2)-[:HAS_EXCEPTION]->(exception4)
MERGE (task2)-[:HAS_EXCEPTION]->(exception5)
MERGE (task2)-[:USES_METHOD]->(method10)
MERGE (task2)-[:USES_METHOD]->(method11)
MERGE (task2)-[:HAS_SCOPE]->(scope1)
MERGE (task2)-[:HAS_TIME_REQUIREMENT]->(requirement7)
MERGE (task2)-[:HAS_HANDLING_REQUIREMENT]->(requirement8)

MERGE (art28)-[:DEFINES_TASK]->(task2)
MERGE (art28)-[:INVOLVES]->(agent25)
MERGE (art28)-[:INVOLVES]->(agent26)
MERGE (art28)-[:INVOLVES]->(agent27)
MERGE (art28)-[:INVOLVES]->(agent28)
MERGE (art28)-[:INVOLVES]->(agent29)

// 第二十九条
MERGE (art29:Article {number: "第二十九条", full_text: "社会稳定风险评估由县级以上人民政府组织有关部门或者委托第三方机构开展，针对拟征收土地社会稳定风险状况进行综合研判，确定风险点，提出风险防范措施和处置预案，形成评估报告。社会稳定风险评估应当有被征地的农村集体经济组织及其成员、村民委员会和其他利害关系人参加，充分听取其意见。"})
MERGE (art29)-[:PART_OF]->(chapter4)

// 评估主体
MERGE (agent30:Agent {name: "第三方机构", type: "organization"})

// 评估参与方
MERGE (agent31:Agent {name: "被征地的农村集体经济组织", type: "organization"})
MERGE (agent32:Agent {name: "农村集体经济组织成员", type: "person"})
MERGE (agent33:Agent {name: "村民委员会", type: "organization"})
MERGE (agent34:Agent {name: "其他利害关系人", type: "person"})

// 评估内容
MERGE (content1:Object {name: "社会稳定风险状况综合研判", type: "assessment_content", source_article: "第二十九条"})
MERGE (content2:Object {name: "确定风险点", type: "assessment_content", source_article: "第二十九条"})
MERGE (content3:Object {name: "提出风险防范措施", type: "assessment_content", source_article: "第二十九条"})
MERGE (content4:Object {name: "提出处置预案", type: "assessment_content", source_article: "第二十九条"})
MERGE (content5:Object {name: "形成评估报告", type: "assessment_content", source_article: "第二十九条"})

// 评估要求
MERGE (requirement9:Object {name: "充分听取参与方意见", type: "participation_requirement", source_article: "第二十九条"})

// 义务
MERGE (duty70:Obligation {description: "组织开展社会稳定风险评估", source_article: "第二十九条"})
MERGE (duty71:Obligation {description: "委托第三方机构开展评估", option: true, source_article: "第二十九条"})
MERGE (duty72:Obligation {description: "确保相关方参与评估过程", source_article: "第二十九条"})
MERGE (duty73:Obligation {description: "充分听取参与方意见", source_article: "第二十九条"})

// 关系建立
MERGE (agent25)-[:HAS_DUTY]->(duty70)
MERGE (agent25)-[:HAS_OPTION]->(duty71)
MERGE (agent25)-[:HAS_DUTY]->(duty72)
MERGE (agent25)-[:HAS_DUTY]->(duty73)

MERGE (agent26)-[:PARTICIPATES_IN]->(duty70)
MERGE (agent30)-[:CONDUCTS]->(duty70)

MERGE (agent31)-[:PARTICIPATES_IN]->(duty72)
MERGE (agent32)-[:PARTICIPATES_IN]->(duty72)
MERGE (agent33)-[:PARTICIPATES_IN]->(duty72)
MERGE (agent34)-[:PARTICIPATES_IN]->(duty72)

MERGE (duty70)-[:INCLUDES_TASK]->(task3)
MERGE (task3)-[:INCLUDES_CONTENT]->(content1)
MERGE (task3)-[:INCLUDES_CONTENT]->(content2)
MERGE (task3)-[:INCLUDES_CONTENT]->(content3)
MERGE (task3)-[:INCLUDES_CONTENT]->(content4)
MERGE (task3)-[:INCLUDES_CONTENT]->(content5)

MERGE (duty73)-[:MEETS_REQUIREMENT]->(requirement9)
MERGE (task3)-[:HAS_REQUIREMENT]->(requirement9)

MERGE (art29)-[:DEFINES_TASK]->(task3)
MERGE (art29)-[:INVOLVES]->(agent25)
MERGE (art29)-[:INVOLVES]->(agent26)
MERGE (art29)-[:INVOLVES]->(agent30)
MERGE (art29)-[:INVOLVES]->(agent31)
MERGE (art29)-[:INVOLVES]->(agent32)
MERGE (art29)-[:INVOLVES]->(agent33)
MERGE (art29)-[:INVOLVES]->(agent34)

// 第三十条
MERGE (art30:Article {number: "第三十条", full_text: "依法拟定的征地补偿安置方案，应当在拟征收土地所在的乡镇和村、村民小组范围内进行公告，听取被征地的农村集体经济组织及其成员、村民委员会和其他利害关系人的意见。公告时间不少于三十日，并采取拍照、录像、公证等方式留存记录。公告应当载明办理补偿登记的方式和期限、不办理补偿登记的后果以及异议反馈渠道等内容。征地补偿安置公告期满，过半数被征地的农村集体经济组织成员对征地补偿安置方案有异议或者县级以上人民政府认为确有必要的，应当组织召开听证会。方案需要修改的，修改后重新公告，公告时间不少于十个工作日，并重新载明办理补偿登记期限；方案无需修改的，应当公布不修改的理由。"})
MERGE (art30)-[:PART_OF]->(chapter4)

// 公告内容
MERGE (content6:Object {name: "办理补偿登记的方式和期限", type: "announcement_content", source_article: "第三十条"})
MERGE (content7:Object {name: "不办理补偿登记的后果", type: "announcement_content", source_article: "第三十条"})
MERGE (content8:Object {name: "异议反馈渠道", type: "announcement_content", source_article: "第三十条"})

// 公告要求
MERGE (requirement10:Object {name: "公告时间不少于三十日", type: "time_requirement", source_article: "第三十条"})

// 听证条件
MERGE (condition5:Object {name: "过半数被征地的农村集体经济组织成员有异议", type: "hearing_condition", source_article: "第三十条"})
MERGE (condition6:Object {name: "县级以上人民政府认为确有必要", type: "hearing_condition", source_article: "第三十条"})

// 听证后续
MERGE (consequence1:Object {name: "方案需要修改", type: "hearing_consequence", source_article: "第三十条"})
MERGE (consequence2:Object {name: "方案无需修改", type: "hearing_consequence", source_article: "第三十条"})

// 修改方案要求
MERGE (requirement12:Object {name: "修改后重新公告", type: "modification_requirement", source_article: "第三十条"})
MERGE (requirement13:Object {name: "重新公告时间不少于十个工作日", type: "time_requirement", source_article: "第三十条"})
MERGE (requirement14:Object {name: "重新载明办理补偿登记期限", type: "content_requirement", source_article: "第三十条"})
MERGE (requirement15:Object {name: "公布不修改的理由", type: "disclosure_requirement", source_article: "第三十条"})

// 义务
MERGE (duty74:Obligation {description: "公告征地补偿安置方案", source_article: "第三十条"})
MERGE (duty75:Obligation {description: "在规定范围内公告方案", source_article: "第三十条"})
MERGE (duty76:Obligation {description: "确保公告时间不少于三十日", source_article: "第三十条"})
MERGE (duty78:Obligation {description: "载明公告必要内容", source_article: "第三十条"})
MERGE (duty79:Obligation {description: "组织召开听证会", condition: "征地补偿安置公告期满，过半数被征地的农村集体经济组织成员对征地补偿安置方案有异议或者县级以上人民政府认为确有必要", source_article: "第三十条"})
MERGE (duty80:Obligation {description: "修改方案并重新公告", condition: "方案需要修改", source_article: "第三十条"})
MERGE (duty81:Obligation {description: "公布不修改的理由", condition: "方案无需修改", source_article: "第三十条"})

// 关系建立
MERGE (agent25)-[:HAS_DUTY]->(duty74)
MERGE (agent25)-[:HAS_DUTY]->(duty75)
MERGE (agent25)-[:HAS_DUTY]->(duty76)
MERGE (agent25)-[:HAS_DUTY]->(requirement6)
MERGE (agent25)-[:HAS_DUTY]->(duty78)
MERGE (agent25)-[:HAS_DUTY]->(duty79)
MERGE (agent25)-[:HAS_DUTY]->(duty80)
MERGE (agent25)-[:HAS_DUTY]->(duty81)

MERGE (duty74)-[:INCLUDES_TASK]->(task4)
MERGE (duty75)-[:APPLIES_TO_SCOPE]->(scope1)
MERGE (duty76)-[:MEETS_REQUIREMENT]->(requirement10)
MERGE (requirement6)-[:MEETS_REQUIREMENT]->(requirement6)
MERGE (duty78)-[:INCLUDES_CONTENT]->(content6)
MERGE (duty78)-[:INCLUDES_CONTENT]->(content7)
MERGE (duty78)-[:INCLUDES_CONTENT]->(content8)

MERGE (task4)-[:HAS_SCOPE]->(scope1)
MERGE (task4)-[:HAS_TIME_REQUIREMENT]->(requirement10)
MERGE (task4)-[:HAS_RECORD_REQUIREMENT]->(requirement6)
MERGE (task4)-[:HAS_CONTENT]->(content6)
MERGE (task4)-[:HAS_CONTENT]->(content7)
MERGE (task4)-[:HAS_CONTENT]->(content8)

MERGE (duty79)-[:TRIGGERED_BY]->(condition5)
MERGE (duty79)-[:TRIGGERED_BY]->(condition6)
MERGE (condition5)-[:INVOLVES]->(agent32)
MERGE (condition6)-[:DECIDED_BY]->(agent25)

MERGE (duty79)-[:LEADS_TO]->(consequence1)
MERGE (duty79)-[:LEADS_TO]->(consequence2)
MERGE (consequence1)-[:TRIGGERS]->(duty80)
MERGE (consequence2)-[:TRIGGERS]->(duty81)

MERGE (duty80)-[:MEETS_REQUIREMENT]->(requirement12)
MERGE (duty80)-[:MEETS_REQUIREMENT]->(requirement13)
MERGE (duty80)-[:MEETS_REQUIREMENT]->(requirement14)

MERGE (art30)-[:DEFINES_TASK]->(task4)
MERGE (art30)-[:INVOLVES]->(agent25)
MERGE (art30)-[:INVOLVES]->(agent31)
MERGE (art30)-[:INVOLVES]->(agent32)
MERGE (art30)-[:INVOLVES]->(agent33)
MERGE (art30)-[:INVOLVES]->(agent34)

// 第三十一条
MERGE (art31:Article {number: "第三十一条", full_text: "拟征收土地的所有权人、使用权人应当在公告载明的办理补偿登记期限内，持不动产权属证明材料办理补偿登记；规定期限内未办理补偿登记的，相关情况按照经确认或者公示的土地现状调查结果确定。补偿登记办理过程，可以采用邀请公证机构现场公证等形式进行记录。"})
MERGE (art31)-[:PART_OF]->(chapter4)

// 补偿登记要求
MERGE (requirement16:Object {name: "持不动产权属证明材料", type: "document_requirement", source_article: "第三十一条"})
MERGE (requirement17:Object {name: "在公告载明的办理补偿登记期限内", type: "time_requirement", source_article: "第三十一条"})
MERGE (requirement18:Object {name: "邀请公证机构现场公证", type: "record_method", source_article: "第三十一条"})

// 补偿登记程序
MERGE (procedure11:Object {name: "补偿登记", type: "procedure", source_article: "第三十一条"})

// 未登记处理方式
MERGE (handling1:Object {name: "按照经确认或者公示的土地现状调查结果确定", type: "handling_method", source_article: "第三十一条"})

// 义务
MERGE (duty82:Obligation {description: "办理补偿登记", source_article: "第三十一条"})
MERGE (duty83:Obligation {description: "持不动产权属证明材料", source_article: "第三十一条"})
MERGE (duty84:Obligation {description: "在规定期限内办理补偿登记", source_article: "第三十一条"})

// 关系建立
MERGE (agent28)-[:HAS_DUTY]->(duty82)
MERGE (agent29)-[:HAS_DUTY]->(duty82)
MERGE (duty82)-[:REQUIRES_DOCUMENT]->(requirement16)
MERGE (duty82)-[:HAS_DEADLINE]->(requirement17)
MERGE (duty82)-[:FOLLOWS_PROCEDURE]->(procedure11)
MERGE (procedure11)-[:HAS_RECORD_METHOD]->(requirement18)
MERGE (procedure11)-[:HAS_EXCEPTION_HANDLING]->(handling1)
MERGE (handling1)-[:BASED_ON]->(task2)

MERGE (art31)-[:DEFINES_PROCEDURE]->(procedure11)
MERGE (art31)-[:INVOLVES]->(agent28)
MERGE (art31)-[:INVOLVES]->(agent29)

// 第三十二条
MERGE (art32:Article {number: "第三十二条", full_text: "县级以上人民政府根据法律、法规的规定和听证会等情况确定征地补偿安置方案后，应当组织测算并落实土地补偿费、安置补助费以及农村村民住宅、其他地上附着物和青苗等的补偿费用（以下统称征收土地补偿费用），以及被征地农民社会保障费用，由有关部门与拟征收土地的所有权人、使用权人签订征地补偿安置协议。涉及不同权利主体的，征地补偿安置协议中应当明确各权利主体利益，并附各权利主体签名或者盖章。征地补偿安置协议应当对交付土地的期限、条件、安置方式以及征收土地补偿费用支付期限等进行约定。征地补偿安置协议签订期限内，个别确实难以达成协议的，县级以上人民政府应当在申请征收土地时如实说明，并做好风险化解工作。"})
MERGE (art32)-[:PART_OF]->(chapter4)

// 补偿费用类型
MERGE (comp1:Object {name: "土地补偿费", type: "compensation_type", source_article: "第三十二条"})
MERGE (comp2:Object {name: "安置补助费", type: "compensation_type", source_article: "第三十二条"})
MERGE (comp3:Object {name: "农村村民住宅补偿", type: "compensation_type", source_article: "第三十二条"})
MERGE (comp4:Object {name: "其他地上附着物补偿", type: "compensation_type", source_article: "第三十二条"})
MERGE (comp5:Object {name: "青苗补偿", type: "compensation_type", source_article: "第三十二条"})
MERGE (comp6:Object {name: "被征地农民社会保障费用", type: "compensation_type", source_article: "第三十二条"})

// 征收土地补偿费用
MERGE (total_comp:Object {name: "征收土地补偿费用", type: "compensation_total", source_article: "第三十二条"})

// 补偿安置协议
MERGE (agreement1:Object {name: "征地补偿安置协议", type: "agreement", source_article: "第三十二条"})

// 协议内容
MERGE (content13:Object {name: "交付土地的期限", type: "agreement_content", source_article: "第三十二条"})
MERGE (content14:Object {name: "交付土地的条件", type: "agreement_content", source_article: "第三十二条"})
MERGE (content15:Object {name: "安置方式", type: "agreement_content", source_article: "第三十二条、第三十五条"})
MERGE (content16:Object {name: "征收土地补偿费用支付期限", type: "agreement_content", source_article: "第三十二条"})

// 特殊情况处理
MERGE (exception7:Object {name: "个别确实难以达成协议", type: "exception_condition", source_article: "第三十二条"})
MERGE (measure3:Object {name: "如实说明", condition: "申请征收土地时", source_article: "第三十二条"})
MERGE (measure4:Object {name: "做好风险化解工作", source_article: "第三十二条"})

// 义务
MERGE (duty85:Obligation {description: "组织测算并落实征收土地补偿费用", source_article: "第三十二条"})
MERGE (duty86:Obligation {description: "签订征地补偿安置协议", source_article: "第三十二条"})
MERGE (duty87:Obligation {description: "明确各权利主体利益", condition: "涉及不同权利主体", source_article: "第三十二条"})
MERGE (duty88:Obligation {description: "附各权利主体签名或者盖章", condition: "涉及不同权利主体", source_article: "第三十二条"})
MERGE (duty89:Obligation {description: "约定交付土地的期限、条件、安置方式以及征收土地补偿费用支付期限", source_article: "第三十二条"})
MERGE (duty90:Obligation {description: "如实说明难以达成协议的情况", condition: "征地补偿安置协议签订期限内，个别确实难以达成协议", source_article: "第三十二条"})
MERGE (duty91:Obligation {description: "做好风险化解工作", condition: "征地补偿安置协议签订期限内，个别确实难以达成协议", source_article: "第三十二条"})

// 关系建立
MERGE (agent25)-[:HAS_DUTY]->(duty85)
MERGE (agent25)-[:HAS_DUTY]->(duty86)
MERGE (agent25)-[:HAS_DUTY]->(duty90)
MERGE (agent25)-[:HAS_DUTY]->(duty91)

MERGE (total_comp)-[:INCLUDES]->(comp1)
MERGE (total_comp)-[:INCLUDES]->(comp2)
MERGE (total_comp)-[:INCLUDES]->(comp3)
MERGE (total_comp)-[:INCLUDES]->(comp4)
MERGE (total_comp)-[:INCLUDES]->(comp5)
MERGE (total_comp)-[:INCLUDES]->(comp6)

MERGE (duty85)-[:CALCULATES]->(total_comp)
MERGE (duty85)-[:CALCULATES]->(comp6)

MERGE (duty86)-[:CREATES]->(agreement1)
MERGE (agreement1)-[:INVOLVES]->(agent28)
MERGE (agreement1)-[:INVOLVES]->(agent29)

MERGE (duty87)-[:RELATED_TO]->(agreement1)
MERGE (duty88)-[:RELATED_TO]->(agreement1)
MERGE (duty89)-[:RELATED_TO]->(agreement1)

MERGE (agreement1)-[:CONTAINS]->(content13)
MERGE (agreement1)-[:CONTAINS]->(content14)
MERGE (agreement1)-[:CONTAINS]->(content15)
MERGE (agreement1)-[:CONTAINS]->(content16)

MERGE (duty90)-[:TRIGGERED_BY]->(exception7)
MERGE (duty91)-[:TRIGGERED_BY]->(exception7)
MERGE (exception7)-[:HANDLED_BY]->(measure3)
MERGE (exception7)-[:HANDLED_BY]->(measure4)

MERGE (art32)-[:DEFINES]->(total_comp)
MERGE (art32)-[:DEFINES]->(agreement1)
MERGE (art32)-[:INVOLVES]->(agent25)
MERGE (art32)-[:INVOLVES]->(agent28)
MERGE (art32)-[:INVOLVES]->(agent29)

// 第三十三条
MERGE (art33:Article {number: "第三十三条", full_text: "征收土地补偿费用、被征地农民社会保障费用实行预存制度。申请征收土地的县级以上人民政府在上报有批准权的人民政府审批前，应当将测算的征收土地补偿费用足额预存至土地补偿和安置补助费有关账户，将社会保障费用足额预存至收缴被征地农民社会保障资金过渡户，并保证专款专用。有关费用未足额预存到专门账户的，不得批准征收土地。"})
MERGE (art33)-[:PART_OF]->(chapter4)

// 预存制度
MERGE (system3:Object {name: "预存制度", type: "financial_system", source_article: "第三十三条"})

// 预存账户
MERGE (account1:Object {name: "土地补偿和安置补助费有关账户", type: "account", source_article: "第三十三条"})
MERGE (account2:Object {name: "收缴被征地农民社会保障资金过渡户", type: "account", source_article: "第三十三条"})

// 预存要求
MERGE (requirement19:Object {name: "足额预存", type: "financial_requirement", source_article: "第三十三条"})
MERGE (requirement20:Object {name: "专款专用", type: "financial_requirement", source_article: "第三十三条"})
MERGE (requirement21:Object {name: "上报审批前完成预存", type: "time_requirement", source_article: "第三十三条"})

// 审批限制
MERGE (restriction1:Object {name: "不得批准征收土地", condition: "有关费用未足额预存到专门账户", type: "approval_restriction", source_article: "第三十三条"})

// 义务
MERGE (duty92:Obligation {description: "足额预存征收土地补偿费用", source_article: "第三十三条"})
MERGE (duty93:Obligation {description: "足额预存社会保障费用", source_article: "第三十三条"})
MERGE (duty94:Obligation {description: "保证专款专用", source_article: "第三十三条"})

// 关系建立
MERGE (agent25)-[:HAS_DUTY]->(duty92)
MERGE (agent25)-[:HAS_DUTY]->(duty93)
MERGE (agent25)-[:HAS_DUTY]->(duty94)

MERGE (system3)-[:REQUIRES]->(duty92)
MERGE (system3)-[:REQUIRES]->(duty93)
MERGE (system3)-[:REQUIRES]->(duty94)

MERGE (duty92)-[:DEPOSITS_TO]->(account1)
MERGE (duty92)-[:INVOLVES]->(total_comp)
MERGE (duty93)-[:DEPOSITS_TO]->(account2)
MERGE (duty93)-[:INVOLVES]->(comp6)

MERGE (duty92)-[:MEETS_REQUIREMENT]->(requirement19)
MERGE (duty93)-[:MEETS_REQUIREMENT]->(requirement19)
MERGE (duty94)-[:MEETS_REQUIREMENT]->(requirement20)
MERGE (duty92)-[:HAS_DEADLINE]->(requirement21)
MERGE (duty93)-[:HAS_DEADLINE]->(requirement21)

MERGE (restriction1)-[:ENFORCED_BY]->(agent22)
MERGE (restriction1)-[:RELATED_TO]->(requirement19)

MERGE (art33)-[:ESTABLISHES]->(system3)
MERGE (art33)-[:INVOLVES]->(agent25)
MERGE (art33)-[:REGULATES]->(total_comp)
MERGE (art33)-[:REGULATES]->(comp6)

// 第三十四条
MERGE (art34:Article {number: "第三十四条", full_text: "征收土地申请经依法批准后，县级以上人民政府应当在收到批准文件之日起十五个工作日内，在拟征收土地所在的乡镇和村、村民小组范围内发布征收土地公告并组织实施，公告期不少于十个工作日，并采取拍照、录像、公证等方式留存记录。公告应当包括下列内容：（一）征地批准机关、文号、时间、用途和征收范围；（二）征地补偿安置方案；（三）征收土地补偿费用以及被征地农民社会保障等费用的支付方式和期限等；（四）其他需要公告的内容。"})
MERGE (art34)-[:PART_OF]->(chapter4)

// 公告要求
MERGE (requirement22:Object {name: "收到批准文件之日起十五个工作日内", type: "time_requirement", source_article: "第三十四条"})
MERGE (requirement23:Object {name: "公告期不少于十个工作日", type: "time_requirement", source_article: "第三十四条"})

// 公告内容
MERGE (content17:Object {name: "征地批准机关、文号、时间、用途和征收范围", type: "announcement_content", source_article: "第三十四条"})
MERGE (content18:Object {name: "征地补偿安置方案", type: "announcement_content", source_article: "第三十四条"})
MERGE (content19:Object {name: "征收土地补偿费用以及被征地农民社会保障等费用的支付方式和期限", type: "announcement_content", source_article: "第三十四条"})
MERGE (content20:Object {name: "其他需要公告的内容", type: "announcement_content", source_article: "第三十四条"})

// 公告范围
MERGE (scope2:Object {name: "拟征收土地所在的乡镇和村、村民小组范围", type: "announcement_scope", source_article: "第三十四条"})

// 义务
MERGE (duty95:Obligation {description: "发布征收土地公告", source_article: "第三十四条"})
MERGE (duty96:Obligation {description: "在规定时间内发布征收土地公告", source_article: "第三十四条"})
MERGE (duty97:Obligation {description: "在规定范围内发布征收土地公告", source_article: "第三十四条"})
MERGE (duty98:Obligation {description: "确保公告期不少于十个工作日", source_article: "第三十四条"})
MERGE (duty99:Obligation {description: "留存公告记录", source_article: "第三十四条"})
MERGE (duty100:Obligation {description: "组织实施征收土地", source_article: "第三十四条"})

// 关系建立
MERGE (agent25)-[:HAS_DUTY]->(duty95)
MERGE (agent25)-[:HAS_DUTY]->(duty96)
MERGE (agent25)-[:HAS_DUTY]->(duty97)
MERGE (agent25)-[:HAS_DUTY]->(duty98)
MERGE (agent25)-[:HAS_DUTY]->(duty99)
MERGE (agent25)-[:HAS_DUTY]->(duty100)

MERGE (duty95)-[:REQUIRES]->(procedure4)
MERGE (duty96)-[:MEETS_REQUIREMENT]->(requirement22)
MERGE (duty97)-[:APPLIES_TO_SCOPE]->(scope2)
MERGE (duty98)-[:MEETS_REQUIREMENT]->(requirement23)
MERGE (duty99)-[:USING_METHOD]->(requirement6)

MERGE (duty95)-[:INCLUDES_CONTENT]->(content17)
MERGE (duty95)-[:INCLUDES_CONTENT]->(content18)
MERGE (duty95)-[:INCLUDES_CONTENT]->(content19)
MERGE (duty95)-[:INCLUDES_CONTENT]->(content20)

MERGE (content17)-[:RELATED_TO]->(procedure4)
MERGE (content18)-[:RELATED_TO]->(agreement1)
MERGE (content19)-[:RELATED_TO]->(total_comp)
MERGE (content19)-[:RELATED_TO]->(comp6)

MERGE (art34)-[:DEFINES_TASK]->(task1)
MERGE (art34)-[:INVOLVES]->(agent25)
MERGE (art34)-[:REGULATES_PROCEDURE]->(procedure4)

// 第三十五条
MERGE (art35:Article {number: "第三十五条", full_text: "对个别未达成征地补偿安置协议的，由县级以上人民政府在征收土地公告期满后，依据征地补偿安置方案和补偿登记结果作出征地补偿安置决定，明确征收范围、土地现状、征收目的、补偿方式和标准、安置对象、安置方式、社会保障以及交地期限等内容，并依法组织实施。被征收土地的所有权人、使用权人未按照征地补偿安置协议交出土地，经催告后仍不履行的，或者在征地补偿安置决定规定的期限内不交出土地的，由县级以上人民政府作出责令交出土地的决定；拒不交出土地的，依法申请人民法院强制执行。"})
MERGE (art35)-[:PART_OF]->(chapter4)

// 特殊情况处理
MERGE (exception8:Object {name: "个别未达成征地补偿安置协议", type: "exception_condition", source_article: "第三十五条"})

// 补偿安置决定
MERGE (decision3:Object {name: "征地补偿安置决定", type: "administrative_decision", source_article: "第三十五条"})

// 决定内容
MERGE (content21:Object {name: "征收范围", type: "decision_content", source_article: "第三十五条"})
MERGE (content22:Object {name: "土地现状", type: "decision_content", source_article: "第三十五条"})
MERGE (content23:Object {name: "征收目的", type: "decision_content", source_article: "第三十五条"})
MERGE (content24:Object {name: "补偿方式和标准", type: "decision_content", source_article: "第三十五条"})
MERGE (content25:Object {name: "安置对象", type: "decision_content", source_article: "第三十五条"})
MERGE (content27:Object {name: "社会保障", type: "decision_content", source_article: "第三十五条"})
MERGE (content28:Object {name: "交地期限", type: "decision_content", source_article: "第三十五条"})

// 土地交出程序
MERGE (procedure12:Object {name: "责令交出土地的决定", type: "enforcement_procedure", source_article: "第三十五条"})
MERGE (procedure13:Object {name: "申请人民法院强制执行", type: "enforcement_procedure", source_article: "第三十五条"})

// 不履行情形
MERGE (violation1:Object {name: "未按照征地补偿安置协议交出土地，经催告后仍不履行", type: "violation_condition", source_article: "第三十五条"})
MERGE (violation2:Object {name: "在征地补偿安置决定规定的期限内不交出土地", type: "violation_condition", source_article: "第三十五条"})

// 义务
MERGE (duty101:Obligation {description: "作出征地补偿安置决定", condition: "个别未达成征地补偿安置协议", source_article: "第三十五条"})
MERGE (duty102:Obligation {description: "明确决定内容", source_article: "第三十五条"})
MERGE (duty103:Obligation {description: "依法组织实施征地补偿安置决定", source_article: "第三十五条"})
MERGE (duty104:Obligation {description: "作出责令交出土地的决定", condition: "未按照征地补偿安置协议交出土地，经催告后仍不履行或在征地补偿安置决定规定的期限内不交出土地", source_article: "第三十五条"})
MERGE (duty105:Obligation {description: "申请人民法院强制执行", condition: "拒不交出土地", source_article: "第三十五条"})

// 关系建立
MERGE (agent25)-[:HAS_DUTY]->(duty101)
MERGE (agent25)-[:HAS_DUTY]->(duty102)
MERGE (agent25)-[:HAS_DUTY]->(duty103)
MERGE (agent25)-[:HAS_DUTY]->(duty104)
MERGE (agent25)-[:HAS_DUTY]->(duty105)

MERGE (duty101)-[:TRIGGERED_BY]->(exception8)
MERGE (duty101)-[:BASED_ON]->(task4)
MERGE (duty101)-[:BASED_ON]->(procedure11)
MERGE (duty101)-[:CREATES]->(decision3)

MERGE (decision3)-[:CONTAINS]->(content21)
MERGE (decision3)-[:CONTAINS]->(content22)
MERGE (decision3)-[:CONTAINS]->(content23)
MERGE (decision3)-[:CONTAINS]->(content24)
MERGE (decision3)-[:CONTAINS]->(content25)
MERGE (decision3)-[:CONTAINS]->(content15)
MERGE (decision3)-[:CONTAINS]->(content27)
MERGE (decision3)-[:CONTAINS]->(content28)

MERGE (duty104)-[:TRIGGERED_BY]->(violation1)
MERGE (duty104)-[:TRIGGERED_BY]->(violation2)
MERGE (duty104)-[:FOLLOWS_PROCEDURE]->(procedure12)

MERGE (duty105)-[:TRIGGERED_BY]->(procedure12)
MERGE (duty105)-[:FOLLOWS_PROCEDURE]->(procedure13)

MERGE (violation1)-[:RELATED_TO]->(agreement1)
MERGE (violation2)-[:RELATED_TO]->(decision3)

MERGE (art35)-[:DEFINES_EXCEPTION]->(exception8)
MERGE (art35)-[:DEFINES_PROCEDURE]->(procedure12)
MERGE (art35)-[:DEFINES_PROCEDURE]->(procedure13)
MERGE (art35)-[:INVOLVES]->(agent25)
MERGE (art35)-[:INVOLVES]->(agent28)
MERGE (art35)-[:INVOLVES]->(agent29)

// 第三十六条
MERGE (art36:Article {number: "第三十六条", full_text: "征收土地应当给予公平、合理的补偿。征收农用地的土地补偿费、安置补助费标准由区片综合地价确定。地级以上市人民政府组织拟定区片综合地价时，一并拟定征收建设用地和未利用地的补偿标准，由省人民政府批准并公布实施。区片综合地价至少每三年调整或者重新公布一次。地级以上市人民政府应当组织拟定农村村民住宅、其他地上附着物以及青苗等补偿费用标准，由省人民政府批准并公布实施。县级以上人民政府应当将被征地农民纳入相应的养老等社会保障体系，依法安排被征地农民的社会保障费用。"})
MERGE (art36)-[:PART_OF]->(chapter4)

// 补偿原则
MERGE (principle1:Object {name: "公平、合理的补偿", type: "compensation_principle", source_article: "第三十六条"})

// 区片综合地价
MERGE (standard1:Object {name: "区片综合地价", type: "compensation_standard", source_article: "第三十六条"})
MERGE (standard2:Object {name: "征收建设用地补偿标准", type: "compensation_standard", source_article: "第三十六条"})
MERGE (standard3:Object {name: "征收未利用地补偿标准", type: "compensation_standard", source_article: "第三十六条"})
MERGE (standard4:Object {name: "农村村民住宅补偿费用标准", type: "compensation_standard", source_article: "第三十六条"})
MERGE (standard5:Object {name: "其他地上附着物补偿费用标准", type: "compensation_standard", source_article: "第三十六条"})
MERGE (standard6:Object {name: "青苗补偿费用标准", type: "compensation_standard", source_article: "第三十六条"})

// 调整要求
MERGE (requirement25:Object {name: "至少每三年调整或者重新公布一次", type: "update_requirement", source_article: "第三十六条"})

// 社会保障
MERGE (system4:Object {name: "养老等社会保障体系", type: "social_security_system", source_article: "第三十六条"})

// 义务
MERGE (duty106:Obligation {description: "给予公平、合理的补偿", source_article: "第三十六条"})
MERGE (duty107:Obligation {description: "组织拟定区片综合地价", source_article: "第三十六条"})
MERGE (duty108:Obligation {description: "一并拟定征收建设用地和未利用地的补偿标准", source_article: "第三十六条"})
MERGE (duty109:Obligation {description: "定期调整或重新公布区片综合地价", source_article: "第三十六条"})
MERGE (duty110:Obligation {description: "组织拟定农村村民住宅、其他地上附着物以及青苗等补偿费用标准", source_article: "第三十六条"})
MERGE (duty111:Obligation {description: "将被征地农民纳入相应的社会保障体系", source_article: "第三十六条"})
MERGE (duty112:Obligation {description: "依法安排被征地农民的社会保障费用", source_article: "第三十六条"})

// 关系建立
MERGE (agent25)-[:HAS_DUTY]->(duty106)
MERGE (agent24)-[:HAS_DUTY]->(duty107)
MERGE (agent24)-[:HAS_DUTY]->(duty108)
MERGE (agent24)-[:HAS_DUTY]->(duty109)
MERGE (agent24)-[:HAS_DUTY]->(duty110)
MERGE (agent25)-[:HAS_DUTY]->(duty111)
MERGE (agent25)-[:HAS_DUTY]->(duty112)

MERGE (duty106)-[:FOLLOWS_PRINCIPLE]->(principle1)
MERGE (duty107)-[:CREATES_STANDARD]->(standard1)
MERGE (duty108)-[:CREATES_STANDARD]->(standard2)
MERGE (duty108)-[:CREATES_STANDARD]->(standard3)
MERGE (duty109)-[:MEETS_REQUIREMENT]->(requirement25)
MERGE (duty110)-[:CREATES_STANDARD]->(standard4)
MERGE (duty110)-[:CREATES_STANDARD]->(standard5)
MERGE (duty110)-[:CREATES_STANDARD]->(standard6)
MERGE (duty111)-[:USES_SYSTEM]->(system4)
MERGE (duty112)-[:PAYS]->(comp6)

MERGE (standard1)-[:APPLIES_TO]->(land_type1)
MERGE (standard1)-[:DETERMINES]->(comp1)
MERGE (standard1)-[:DETERMINES]->(comp2)
MERGE (standard2)-[:APPLIES_TO]->(land_type2)
MERGE (standard3)-[:APPLIES_TO]->(land_type3)
MERGE (comp3)-[:BASED_ON_STANDARD]->(standard4)
MERGE (comp4)-[:BASED_ON_STANDARD]->(standard5)
MERGE (comp5)-[:BASED_ON_STANDARD]->(standard6)

MERGE (agent23)-[:HAS_AUTHORITY]->(standard1)
MERGE (agent23)-[:HAS_AUTHORITY]->(standard2)
MERGE (agent23)-[:HAS_AUTHORITY]->(standard3)
MERGE (agent23)-[:HAS_AUTHORITY]->(standard4)
MERGE (agent23)-[:HAS_AUTHORITY]->(standard5)
MERGE (agent23)-[:HAS_AUTHORITY]->(standard6)

MERGE (art36)-[:DEFINES_PRINCIPLE]->(principle1)
MERGE (art36)-[:DEFINES_STANDARD]->(standard1)
MERGE (art36)-[:INVOLVES]->(agent25)
MERGE (art36)-[:INVOLVES]->(agent24)
MERGE (art36)-[:INVOLVES]->(agent23)

// 第三十七条
MERGE (art37:Article {number: "第三十七条", full_text: "县级以上人民政府应当在征收土地公告期满之日起三个月内，足额支付征收土地补偿费用，并落实被征地农民社会保障费用。对个别未达成征地补偿安置协议的，支付征收土地补偿费用的期限自征地补偿安置决定作出之日起计算。征收土地补偿费用、被征地农民社会保障费用等未按照规定足额支付到位或者提存公证的，不得强行征收、占用被征收土地。禁止侵占、挪用征收土地补偿费用和其他有关费用。"})
MERGE (art37)-[:PART_OF]->(chapter4)

// 支付期限
MERGE (deadline3:Object {name: "征收土地公告期满之日起三个月内", type: "time_limit", source_article: "第三十七条"})
MERGE (deadline4:Object {name: "征地补偿安置决定作出之日起计算", condition: "个别未达成征地补偿安置协议", type: "time_limit", source_article: "第三十七条"})

// 支付要求
MERGE (requirement26:Object {name: "足额支付", type: "payment_requirement", source_article: "第三十七条"})
MERGE (requirement27:Object {name: "提存公证", alternative: true, source_article: "第三十七条"})

// 强制措施限制
MERGE (restriction2:Object {name: "不得强行征收、占用被征收土地", condition: "征收土地补偿费用、被征地农民社会保障费用等未按照规定足额支付到位或者提存公证", type: "enforcement_restriction", source_article: "第三十七条"})

// 禁止行为
MERGE (prohibition1:Object {name: "侵占征收土地补偿费用", type: "prohibited_action", source_article: "第三十七条"})
MERGE (prohibition2:Object {name: "挪用征收土地补偿费用", type: "prohibited_action", source_article: "第三十七条"})
MERGE (prohibition3:Object {name: "侵占其他有关费用", type: "prohibited_action", source_article: "第三十七条"})
MERGE (prohibition4:Object {name: "挪用其他有关费用", type: "prohibited_action", source_article: "第三十七条"})

// 义务
MERGE (duty113:Obligation {description: "足额支付征收土地补偿费用", source_article: "第三十七条"})
MERGE (duty114:Obligation {description: "落实被征地农民社会保障费用", source_article: "第三十七条"})
MERGE (duty115:Obligation {description: "在规定期限内支付征收土地补偿费用", source_article: "第三十七条"})

// 关系建立
MERGE (agent25)-[:HAS_DUTY]->(duty113)
MERGE (agent25)-[:HAS_DUTY]->(duty114)
MERGE (agent25)-[:HAS_DUTY]->(duty115)

MERGE (duty113)-[:PAYS]->(total_comp)
MERGE (duty114)-[:PAYS]->(comp6)
MERGE (duty115)-[:HAS_DEADLINE]->(deadline3)
MERGE (duty115)-[:HAS_ALTERNATIVE_DEADLINE]->(deadline4)
MERGE (duty115)-[:MEETS_REQUIREMENT]->(requirement26)

MERGE (restriction2)-[:TRIGGERED_BY]->(requirement26)
MERGE (restriction2)-[:ALTERNATIVE_TRIGGERED_BY]->(requirement27)

MERGE (prohibition1)-[:RELATED_TO]->(total_comp)
MERGE (prohibition2)-[:RELATED_TO]->(total_comp)
MERGE (prohibition3)-[:RELATED_TO]->(comp6)
MERGE (prohibition4)-[:RELATED_TO]->(comp6)

MERGE (agent25)-[:MUST_NOT]->(prohibition1)
MERGE (agent25)-[:MUST_NOT]->(prohibition2)
MERGE (agent25)-[:MUST_NOT]->(prohibition3)
MERGE (agent25)-[:MUST_NOT]->(prohibition4)

MERGE (art37)-[:REGULATES]->(total_comp)
MERGE (art37)-[:REGULATES]->(comp6)
MERGE (art37)-[:INVOLVES]->(agent25)
MERGE (art37)-[:DEFINES_RESTRICTION]->(restriction2)

// 第三十八条
MERGE (art38:Article {number: "第三十八条", full_text: "经批准收回国有农、林、牧、渔、盐场的土地，参照征收农民集体所有土地的标准给予公平、合理的补偿。法律、行政法规另有规定的，从其规定。"})
MERGE (art38)-[:PART_OF]->(chapter4)

// 特殊土地类型
MERGE (land_type5:Object {name: "经批准回收国有农、林、牧、渔、盐场的土地", type: "land_type", source_article: "第三十八条"})

// 补偿方式
MERGE (comp_method1:Object {name: "参照征收农民集体所有土地的标准", type: "compensation_method", source_article: "第三十八条"})

// 例外规定
MERGE (exception9:Object {name: "法律、行政法规另有规定", type: "legal_exception", source_article: "第三十八条"})

// 义务
MERGE (duty116:Obligation {description: "参照征收农民集体所有土地的标准进行补偿", condition: "收回国有农、林、牧、渔、盐场的土地", source_article: "第三十八条"})

// 关系建立
MERGE (agent22)-[:HAS_DUTY]->(duty116)

MERGE (duty116)-[:USES_METHOD]->(comp_method1)
MERGE (comp_method1)-[:REFERENCES]->(art36)

MERGE (exception9)-[:OVERRIDES]->(duty116)

MERGE (art38)-[:REGULATES]->(land_type5)
MERGE (art38)-[:REFERENCES]->(art36)
MERGE (art38)-[:HAS_EXCEPTION]->(exception9)