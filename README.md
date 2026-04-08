# AI Agent Skills

Набор скиллов для AI-агентов, превращающий их в экспертов в различных технологиях и доменах.

Каждый скилл — это набор правил, best practices и паттернов, оптимизированных для автоматизации и консистентности AI-assisted разработки.

---

## Категории

### Frontend

| Скилл | Описание |
|-------|----------|
| [nextjs](nextjs/) | Next.js 16 App Router — бандл, кэширование, Server Components |
| [next-best-practices](next-best-practices/) | Best practices для Next.js |
| [react-best-practices](react-best-practices/) | React performance и паттерны |
| [react-hook-form](react-hook-form/) | React Hook Form — производительные формы |
| [react-hook-form-zod](react-hook-form-zod/) | Типобезопасные формы с Zod |
| [react-state-management](react-state-management/) | Redux, Zustand, Jotai, React Query |
| [nuqs](nuqs/) | Type-safe URL state для Next.js |
| [tailwind](tailwind/) | Tailwind CSS v4 |
| [daisyui](daisyui/), [daisyui-5](daisyui-5/) | DaisyUI компоненты |
| [motion](motion/) | Framer Motion анимации |
| [shadcn](shadcn/) | shadcn/ui компоненты |
| [design-system-patterns](design-system-patterns/) | Дизайн-системы и токены |
| [ui-design](ui-design/) | UI/UX лучшие практики |

### Backend

| Скилл | Описание |
|-------|----------|
| [nestjs-best-practices](nestjs-best-practices/) | NestJS архитектура, DI, безопасность |
| [nestjs-expert](nestjs-expert/) | Продвинутый NestJS |
| [drizzle-orm-d1](drizzle-orm-d1/) | D1 базы с Drizzle ORM |
| [python-*](python-code-style/) | Python best practices (7 скиллов) |

### Architecture & Code Quality

| Скилл | Описание |
|-------|----------|
| [architect-review](architect-review/) | Обзор архитектуры |
| [architecture-patterns](architecture-patterns/) | Паттерны: Clean, Hexagonal, DDD |
| [api-design-principles](api-design-principles/) | REST и GraphQL дизайн |
| [code-reviewer](code-reviewer/) | AI code review |
| [refactor](refactor/) | Рефакторинг паттерны (Martin Fowler) |
| [changelog-automation](changelog-automation/) | Автоматизация changelog |

### Other

| Скилл | Описание |
|-------|----------|
| [open-pencil](open-pencil/) | Figma интеграция |

---

## Структура скилла

```
skill-name/
├── SKILL.md          # Основное описание и применение
├── AGENTS.md         # Детальные правила для AI-агентов
├── README.md         # Документация
├── metadata.json     # Метаданные (версия, технология)
└── references/      # Дополнительные материалы
    ├── _sections.md  # Категории правил
    └── *.md          # Конкретные правила
```

---

## Использование

Скиллы интегрируются с AI-агентами (Claude, GPT, etc.) через формат `SKILL.md`. Каждый скилл содержит:

- **Когда применять** — триггеры и контекст
- **Правила** — приоритизированные рекомендации
- **Примеры** — incorrect vs correct implementations
- **Метрики** — impact measurements

---

## Статистика

- **40+** скиллов
- **500+** правил
- **10+** технологий

---

## Добавление скилла

1. Создай директорию с именем технологии
2. Добавь `SKILL.md` с frontmatter
3. Добавь `AGENTS.md` с детальными правилами
4. Опционально: `metadata.json`, `references/`

См. [nestjs-best-practices](nestjs-best-practices/) как референс.
