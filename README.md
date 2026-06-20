Опис проєкту

Цей проєкт реалізує систему генерації документів з підтримкою різних форматів виводу: Markdown, HTML та plain text. Документ будується як ієрархічна структура елементів (дерево), де секції можуть містити інші елементи, такі як параграфи, списки та вкладені секції.
Форматування виводу повністю відокремлене від структури документа і реалізоване через рендерери.

Архітектура

Проєкт побудований із використанням двох структурних патернів:
Composite
Патерн реалізовано в класі Section, який виступає контейнером для інших елементів документа. Усі елементи реалізують інтерфейс DocNode, що дозволяє формувати деревоподібну структуру документа.

Основні характеристики:
Section може містити інші DocNode
Підтримується вкладеність будь-якої глибини
Усі елементи мають однаковий інтерфейс render()

Bridge
Патерн реалізовано через відокремлення структури документа від способу його форматування.

Основні компоненти:
DocRenderer — інтерфейс форматування
BaseRenderer — базовий клас рендерерів
HTMLRenderer, MarkdownRenderer, PlainTextRenderer — конкретні реалізації
Документи не знають, у якому форматі вони будуть відображені — це визначається рендерером.

Структура проєкту
src/
├── interfaces/
│ ├── DocNode.ts
│ └── DocRenderer.ts
├── renderers/
│ ├── BaseRenderer.ts
│ ├── HTMLRenderer.ts
│ ├── MarkdownRenderer.ts
│ └── PlainTextRenderer.ts
├── nodes/
│ ├── List.ts
│ ├── Paragraph.ts
│ └── Section.ts
├── factories/
│ └── RendererFactory.ts
└── main.ts

Встановлення
npm install

Запуск проєкту
Запуск з вибором формату:
npx ts-node src/main.ts markdown
npx ts-node src/main.ts html
npx ts-node src/main.ts plain

Вивід у файл
npx ts-node src/main.ts markdown output.md
npx ts-node src/main.ts html output.html
npx ts-node src/main.ts plain output.txt
