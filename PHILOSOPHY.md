# Phreebox — Philosophy / Философия

> *"Your phone is a computer. It should belong to you."*
> *«Твой телефон — это компьютер. Он должен принадлежать тебе.»*

---

## English

### Why This Exists

When you buy a smartphone today, you do not buy a computer.
You buy a locked box.

The processor is closed. The firmware is proprietary. The bootloader resists you.
The hardware is designed to fail on a schedule set by someone else.
Repair is restricted. Modification is discouraged. Understanding is not the goal.

This is not an accident. It is a design decision — made by manufacturers, not users.

**Phreebox is a rejection of that decision.**

The name comes from *phone phreaking* — the practice of exploring and understanding
telephone systems at a time when that knowledge was considered dangerous.
We believe the same spirit applies today:
understanding your hardware should not be radical. It should be normal.

---

### The Architecture

The core insight is simple:

**The phone does not need to be the computer.**

The phone is a display, a touch surface, and a radio module.
The computer — the part that runs your software, stores your data, does your work —
lives in a separate unit: the Cube.

```
┌─────────────────────┐         ┌──────────────────────┐
│        CUBE         │         │        PHONE         │
│                     │         │                      │
│  x86_64 CPU         │◄───────►│  Display module      │
│  Open RAM           │  USB-C  │  Touch input         │
│  NVMe storage       │  Proto  │  4G/5G modem         │
│  Open drivers       │  -col   │  Camera module       │
│  Arch Linux         │         │  Battery             │
│  User-owned         │         │  Nothing hidden      │
└─────────────────────┘         └──────────────────────┘
```

The Cube runs standard desktop Arch Linux.
No compromises. No vendor blobs. No locked bootloader.
It is, simply, a PC — built from open hardware, documented in full.

The Phone becomes what it should always have been:
a portable interface to your computer.

This architecture solves three problems at once:

1. **Compatibility** — the Cube is a standard x86 PC. Every Arch Linux package works.
2. **Closed silicon** — we do not use Qualcomm or MediaTek for computation. We do not fight their restrictions. We route around them.
3. **Longevity** — the Phone is just a screen. It does not become obsolete when the CPU does.

---

### What Modularity Means Here

Every component in Phreebox is a module with a defined interface and a published specification.

This is not an engineering preference. It is a political stance.

When the display is a module — someone builds a better one.
When the compute board is a module — someone builds a faster one.
When the radio is a module — someone builds one that respects privacy.
When the protocol is open — someone builds a compatible phone from different parts entirely.

The specification is the contract. The implementation is the community's freedom.

We define the borders. We do not dictate what happens inside them.

---

### Licensing

| Layer         | License                         |
|---------------|---------------------------------|
| Hardware      | CERN Open Hardware License v2   |
| Software      | GNU General Public License v3   |
| Specification | Creative Commons CC-BY-SA 4.0   |
| Documentation | Creative Commons CC-BY-SA 4.0   |

These licenses are not formalities.
They are the legal guarantee that this platform cannot be enclosed.
Any fork must remain free. Any modification must be shareable.
The freedom is inherited, not optional.

---

### Principles

**1. Real problems only.**
We build for problems that exist now, not problems we imagine might exist.

**2. The simplest solution that works.**
Complexity is technical debt. We do not borrow against the future without reason.

**3. Borders, not implementations.**
Each module has a defined interface. How it is implemented internally is the contributor's decision.

**4. Document everything.**
Undocumented hardware is closed hardware, regardless of whether the files are public.
A schematic without explanation is a riddle, not a contribution.

**5. If it can be removed, remove it.**
Every unnecessary component is a failure mode, a repair cost, and a restriction on freedom.

**6. The device belongs to the person holding it.**
Every technical and organisational decision is evaluated against this sentence.

---

### What This Project Is Not

This is not a company. There is no product roadmap driven by revenue.
This is not a competitor to Android or iOS. We are not fighting for market share.
This is not a distribution of Linux. It is a hardware platform that runs standard Arch Linux.
This is not finished. It will never be finished. It will only grow.

---

### How to Contribute

You do not need permission to contribute to Phreebox.

- **Hardware module**: follow the module specification, submit to `community/modules/`
- **Software**: open a pull request against `software/`
- **New device port**: follow the porting guide in `docs/porting-guide.md`
- **Protocol change**: open an RFC in `spec/rfcs/` and start a discussion
- **Documentation**: any improvement is welcome

The only requirement: what you contribute must remain as free as what you received.

---
---

## Русский

### Зачем это существует

Когда ты покупаешь смартфон сегодня — ты не покупаешь компьютер.
Ты покупаешь закрытый ящик.

Процессор закрыт. Прошивка проприетарна. Загрузчик сопротивляется.
Железо спроектировано так, чтобы устареть по чужому расписанию.
Ремонт ограничен. Модификация не приветствуется. Понимание не является целью.

Это не случайность. Это проектное решение — принятое производителями, а не пользователями.

**Phreebox — это отказ от этого решения.**

Название происходит от *phone phreaking* — практики исследования и понимания
телефонных систем в то время, когда такое знание считалось опасным.
Мы считаем, что тот же дух актуален сегодня:
понимание своего железа не должно быть радикализмом. Это должно быть нормой.

---

### Архитектура

Ключевая идея проста:

**Телефону не обязательно быть компьютером.**

Телефон — это дисплей, сенсорная поверхность и радиомодуль.
Компьютер — та часть, которая запускает программы, хранит данные, выполняет вычисления —
находится в отдельном устройстве: Кубе.

```
┌─────────────────────┐         ┌──────────────────────┐
│        КУБ          │         │       ТЕЛЕФОН        │
│                     │         │                      │
│  CPU x86_64         │◄───────►│  Модуль дисплея      │
│  Открытая RAM       │  USB-C  │  Сенсорный ввод      │
│  NVMe хранилище     │  Прото  │  Модем 4G/5G         │
│  Открытые драйверы  │  -кол   │  Модуль камеры       │
│  Arch Linux         │         │  Батарея             │
│  Принадлежит тебе   │         │  Ничего скрытого     │
└─────────────────────┘         └──────────────────────┘
```

Куб запускает стандартный десктопный Arch Linux.
Без компромиссов. Без проприетарных блобов. Без заблокированного загрузчика.
Он просто является ПК — собранным из открытого железа, задокументированным полностью.

Телефон становится тем, чем всегда должен был быть:
портативным интерфейсом к твоему компьютеру.

Эта архитектура решает три проблемы одновременно:

1. **Совместимость** — Куб является стандартным x86 ПК. Работает весь каталог пакетов Arch Linux.
2. **Закрытый кремний** — мы не используем Qualcomm или MediaTek для вычислений. Мы не боремся с их ограничениями. Мы их обходим.
3. **Долговечность** — Телефон это просто экран. Он не устаревает когда устаревает CPU.

---

### Что означает модульность здесь

Каждый компонент Phreebox — это модуль с определённым интерфейсом и опубликованной спецификацией.

Это не инженерное предпочтение. Это политическая позиция.

Когда дисплей является модулем — кто-то создаёт лучший.
Когда вычислительная плата является модулем — кто-то создаёт более быструю.
Когда радиомодуль является модулем — кто-то создаёт тот, который уважает приватность.
Когда протокол открыт — кто-то собирает совместимый телефон из совершенно других компонентов.

Спецификация — это контракт. Реализация — это свобода сообщества.

Мы определяем границы. Мы не диктуем, что происходит внутри них.

---

### Лицензии

| Слой              | Лицензия                          |
|-------------------|-----------------------------------|
| Железо            | CERN Open Hardware License v2     |
| Программный код   | GNU General Public License v3     |
| Спецификация      | Creative Commons CC-BY-SA 4.0     |
| Документация      | Creative Commons CC-BY-SA 4.0     |

Эти лицензии — не формальность.
Это юридическая гарантия того, что платформа не может быть закрыта.
Любой форк должен оставаться свободным. Любая модификация должна быть доступна для распространения.
Свобода наследуется, а не выбирается опционально.

---

### Принципы

**1. Только реальные проблемы.**
Мы строим для проблем, которые существуют сейчас, а не для тех, которые могут возникнуть когда-нибудь.

**2. Простейшее решение, которое работает.**
Сложность — это технический долг. Мы не берём кредит у будущего без причины.

**3. Границы, а не реализации.**
Каждый модуль имеет определённый интерфейс. То, как он реализован внутри — решение контрибьютора.

**4. Документировать всё.**
Незадокументированное железо — закрытое железо, независимо от того, опубликованы ли файлы.
Схема без объяснения — это загадка, а не вклад.

**5. Если можно убрать — убери.**
Каждый лишний компонент — это точка отказа, стоимость ремонта и ограничение свободы.

**6. Устройство принадлежит тому, кто его держит.**
Каждое техническое и организационное решение оценивается по этой фразе.

---

### Чем этот проект не является

Это не компания. Здесь нет продуктовой дорожной карты, движимой выручкой.
Это не конкурент Android или iOS. Мы не боремся за долю рынка.
Это не дистрибутив Linux. Это аппаратная платформа, которая запускает стандартный Arch Linux.
Это не завершённый проект. Он никогда не будет завершён. Он будет только расти.

---

### Как внести вклад

Тебе не нужно разрешение для участия в Phreebox.

- **Аппаратный модуль**: следуй спецификации модуля, отправляй в `community/modules/`
- **Программный код**: открой pull request в `software/`
- **Портирование на новое устройство**: следуй руководству в `docs/porting-guide.md`
- **Изменение протокола**: открой RFC в `spec/rfcs/` и начни обсуждение
- **Документация**: любое улучшение приветствуется

Единственное требование: то, что ты вносишь, должно оставаться таким же свободным, каким ты это получил.

---

*Phreebox посвящается всем, кто когда-либо открывал устройство
и хотел понять, что внутри.*
