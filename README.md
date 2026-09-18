# architect-skills

ชุด 8 skill สำหรับ Claude Code ที่ครอบคลุม production software lifecycle ทั้งหมด ตั้งแต่การตัดสินใจ
ระดับ architecture ไปจนถึง deployment — แต่ละตัวใช้ audit rubric เชิงวัตถุวิสัยของตัวเอง (เทียบเท่า
normalization audit ของฝั่ง DB) ไม่ใช่แค่ checklist ลอยๆ

## รายการ skill (เรียงตามลำดับที่ควรใช้)

| Skill | ใช้ทำอะไร | Audit Rubric |
|---|---|---|
| `system-design-architect` | ตัดสินใจ architecture ระดับ macro (monolith/microservices, service boundary) | Bounded Context, Data Ownership, Coupling Mode, Consistency Model, Fallacies of Distributed Computing |
| `db-architect` | ออกแบบ/ตรวจ database schema | Normalization (1NF–BCNF) |
| `api-architect` | ออกแบบ/ตรวจ REST API | Richardson Maturity Model + HTTP semantics |
| `security-architect` | ตรวจความปลอดภัย, threat modeling | OWASP Top 10 (6 มิติ) |
| `test-architect` | ออกแบบ test suite | Equivalence/Boundary/State-Transition + FIRST + Test Smells |
| `resilience-architect` | ทนต่อความล้มเหลวของ dependency ภายนอก | Timeout/Retry/Circuit Breaker/Fallback/Bulkhead |
| `observability-architect` | logging/metrics/tracing/alerting | Structured Logging/RED-USE Metrics/Tracing/SLO Alerting |
| `deployment-architect` | CI/CD, release strategy | Pipeline Gate/Env Parity/Release Strategy/Rollback/Secret Mgmt/Deploy Observability |

`system-design-architect` ควรใช้ก่อนตัวอื่นเสมอ เพราะเป็นการตัดสินใจที่แก้ทีหลังแพงที่สุด ส่วนอีก 7
ตัวอ้างอิงกันข้ามชั้นได้ (เช่น `resilience-architect` ใช้ Idempotency-Key pattern จาก
`api-architect`, `deployment-architect` ปกป้อง secret ตาม pattern เดียวกับ `security-architect`)

## ติดตั้ง

```
/plugin marketplace add <github-owner>/architect-skills
/plugin install architect-skills@architect-skills
```

หลังติดตั้ง เรียกใช้ผ่าน `/architect-skills:<ชื่อ skill>` เช่น `/architect-skills:db-architect`
(namespace ตามชื่อ plugin เพราะ skill ที่มาจาก plugin จะมี prefix เสมอ ต่างจากตอนวางไฟล์ไว้ใน
`~/.claude/commands/` ส่วนตัวที่เรียกด้วย `/db-architect` ตรงๆ ได้)

## อัปเดตเป็นเวอร์ชันล่าสุด

```
/plugin marketplace update architect-skills
```

## โครงสร้าง repo

```
architect-skills/
├── .claude-plugin/
│   └── marketplace.json          ← marketplace catalog
├── plugins/
│   └── architect-skills/
│       ├── .claude-plugin/
│       │   └── plugin.json       ← plugin manifest
│       └── skills/
│           ├── system-design-architect/SKILL.md
│           ├── db-architect/SKILL.md
│           ├── api-architect/SKILL.md
│           ├── security-architect/SKILL.md
│           ├── test-architect/SKILL.md
│           ├── resilience-architect/SKILL.md
│           ├── observability-architect/SKILL.md
│           └── deployment-architect/SKILL.md
└── README.md
```
