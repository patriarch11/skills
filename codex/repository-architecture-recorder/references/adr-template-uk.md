# Classical ADR Template (Ukrainian)

Use this template when drafting ADRs for this skill.

## Filename convention

Default to:

`NNNN-short-kebab-case-title.md`

Examples:
- `0001-monorepo-structure.md`
- `0002-api-versioning-strategy.md`

If the repository already has an ADR numbering or naming convention, follow the existing convention instead.

## Markdown template

```markdown
# [Коротка назва рішення]

- Статус: [Запропоновано | Погоджено | Замінено | Відхилено]
- Дата: [YYYY-MM-DD]
- Пов'язані ADR: [за потреби, відносні посилання]

## Контекст

[Яку проблему або обмеження ми маємо. Які сили, вимоги, ризики чи обставини впливають на вибір.]

## Рішення

[Що саме ми вирішили зробити. Сформулюй рішення однозначно, без двозначностей.]

## Альтернативи

- [Альтернатива 1] — [чому не обрали]
- [Альтернатива 2] — [чому не обрали]

## Наслідки

### Переваги

- [...]

### Недоліки / компроміси

- [...]

### Подальші дії

- [...]
```

## Guidance

- Keep the title short and decision-oriented.
- `Контекст` should explain why the decision exists now.
- `Рішення` should be the most concrete section.
- `Альтернативи` can be omitted only if there are no realistic alternatives worth recording.
- `Наслідки` should include both benefits and costs.
- Use Ukrainian throughout the ADR body.
