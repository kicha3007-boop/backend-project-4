# Загрузчик страниц (JS)

[![hexlet-check](https://github.com/kicha3007-boop/backend-project-4/actions/workflows/hexlet-check.yml/badge.svg)](https://github.com/kicha3007-boop/backend-project-4/actions)
[![CI](https://github.com/kicha3007-boop/backend-project-4/actions/workflows/main.yml/badge.svg)](https://github.com/kicha3007-boop/backend-project-4/actions/workflows/main.yml)

`page-loader` скачивает веб-страницу вместе с локальными ресурсами (картинки, стили, скрипты с того же
хоста) и переписывает ссылки на скачанные файлы — страницу можно открыть без интернета. Ресурсы
качаются параллельно, прогресс выводится в терминал.

Учебный проект Хекслета: https://ru.hexlet.io/programs/nodejs

## Требования

- Node.js 22 или новее
- npm, make

## Установка

```bash
git clone https://github.com/kicha3007-boop/backend-project-4.git
cd backend-project-4
make install
npm link
```

## Запуск

```bash
page-loader --output /var/tmp https://ru.hexlet.io/courses
# Page was downloaded as '/var/tmp/ru-hexlet-io-courses.html'
```

Страница сохраняется как `ru-hexlet-io-courses.html`, ресурсы — в `ru-hexlet-io-courses_files/`.
Без `--output` файлы кладутся в текущую директорию. При ошибке (сеть, ответ не 200, нет директории
или прав) утилита печатает сообщение в stderr и завершается с кодом 1.

Как библиотека:

```javascript
import pageLoader from '@hexlet/code';

pageLoader('https://ru.hexlet.io/courses', '/var/tmp').then(({ filepath }) => console.log(filepath));
```

Отладочный лог: `DEBUG=page-loader page-loader https://ru.hexlet.io/courses`
(`DEBUG=page-loader,axios,nock.*` — вместе с запросами axios и моками nock в тестах).

## Разработка

```bash
make test            # vitest, сеть подменяется nock
make test-coverage   # тесты с порогом покрытия 90%
make lint            # oxlint + проверка форматирования oxfmt
```
