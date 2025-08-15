# IT Business Analyst Manual

Repository with ready-to-use **BA templates**, guides, and KPI materials (EN/KA).

## Contents
- `/docs` — How-to guides (folder purpose, document catalog, i18n, KPI guides)
- `/templates/BA-Folder-3lang/` — Project templates in **en/ka/ru**
- `/templates/kpi/` — KPI register CSV template
- `/.github/workflows/i18n-sync.yml` — marks localized docs `needs-sync: true` on PR when EN changes

## Quick Start
1. Copy `templates/BA-Folder-3lang/` into your project.
2. Keep EN as canonical; use KA/RU as localized.
3. Define KPIs via `/docs/kpi-design.en.md` and `/docs/kpi-design.ka.md`, then list them in `/templates/kpi/kpi-register-template.csv`.
