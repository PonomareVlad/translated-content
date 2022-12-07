---
title: URL-суффиксы
slug: conflicting/MDN
tags:
  - HTTP
  - Kuma
  - MDN Мета
  - URL
  - Параметры URL
  - инструменты
translation_of: MDN/Tools/Document_parameters
original_slug: MDN/Tools/Unsupported_GET_API
---

{{MDNSidebar}}

Вики-платформа MDN Kuma не имеет центрального API. Вместо этого наш общий подход заключается в том, чтобы предложить способы превращения доступных для человека ресурсов в удобные для машин данные.

## Параметры URL GET

Мы поддерживаем несколько полезных параметров запроса для каждого URL-адреса вики-документа Kuma при получении через HTTP GET или просмотре в браузере.

Несколько параметров запроса разделяются знаком <kbd>&#x26;</kbd> вместо начального <kbd>?</kbd>. (См. Примеры макроса.)

- `summary`

  - : Указывает Куме возвращать только сводку страницы. Если на странице есть контент, помеченный классом «Сводка SEO», этот контент возвращается. Если такого содержания нет, возвращается содержание раздела «Сводка». В противном случае возвращается содержимое первого блока.

    > **Примечание:** **Уведомление об ошибке:** В настоящее время существует ошибка, из-за которой сводный параметр возвращает весь документ, если вы также не укажете необработанный параметр. Обратите внимание, что вы также можете получить сводку из возвращённого JSON, [используя альтернативное представление $ json](/ru/docs/MDN/Tools/URL-suffix#json-view).

- `raw`

  - : Указывает Kuma вернуть необработанное содержимое страницы без какого-либо материала обложки, такого как верхние, нижние колонтитулы и т. д. При этом не выполняются шаблоны или сценарии, что удобно для редакторов сборки.

    **Пример:** [/ru/docs/HTML/HTML5?raw](/ru/docs/HTML/HTML5?raw)

- `macros`

  - : Поручает Kuma выполнить все шаблоны на странице. В сочетании с `?raw` это предлагает полностью визуализированный контент MDN без оболочки сайт . Поручает Kuma выполнить все шаблоны на странице. В сочетании с `?raw` это предлагает полностью визуализированный контент MDN без оболочки сайта. По умолчанию включено без `?raw` (то есть при обычном просмотре сайта), по умолчанию выключено, когда присутствует `?raw`.

    **Пример:** [/ru/docs/HTML/HTML5?raw\&macros](/ru/docs/HTML/HTML5?raw&macros)

- `nomacros`

  - : Указывает Kuma не выполнять шаблоны KumaScript на странице. Поскольку при обычном просмотре сайта для `?macros` по умолчанию установлено значение «включено», этот параметр отключает его.

    **Пример:** [/ru/docs/HTML/HTML5?nomacros](/ru/docs/HTML/HTML5?nomacros)

- `include`

  - : Говорит Kuma удалить все блоки, на которых есть класс `noinclude`. Это полезно для получения вывода таким, каким он был бы при включении на другую страницу, а не на отдельной странице. Часто это удаляет образец кода и тому подобное (хотя не всегда).

    **Пример:** [/ru/docs/Archive/Mozilla/XUL/Attribute/align?raw\&macros\&include](/ru/docs/Archive/Mozilla/XUL/Attribute/align?raw&macros&include)

- `section=id`

  - : Указывает Kuma вернуть содержимое только из раздела с указанным якорем/именем привязки.

    **Пример:**

    - [/ru/docs/MDN/Tools/URL-suffix?raw\&section=params](/ru/docs/MDN/Tools/URL-suffix?raw&section=params)
      (...и больше интересного...)
    - [/ru/docs/MDN/Tools/URL-suffix?raw\&macros\&section=params](/ru/docs/MDN/Tools/URL-suffix?raw&macros&section=params)

    > **Уведомление об ошибке:** В настоящее время существует ошибка, из-за которой параметр `section` возвращает весь документ, если вы также не укажете параметр `raw`.

- `expand`

  - : В сочетании с представлением `$children` расширяет ответ JSON с подробной информацией для каждой подстраницы. Он работает как комбинация `$children` и `$json` на каждой подстранице. Таким образом, можно узнать о тегах для подстраницы.

    **Пример:** [/ru/docs/MDN/About$children?expand](/ru/docs/MDN/About$children?expand)

## Ресурсы метаданных документа

Наряду с параметрами для настройки ответа URL-адреса документа существуют также некоторые альтернативные представления документов, заданные суффиксом URL-адреса:

- `$toc`

  - : Указывает Kuma вернуть только оглавление страницы в HTML. Он возвращается как упорядоченный список (то есть , {{HTMLElement("ol")}}).

    **Пример:** [/ru/docs/MDN/Tools/URL-suffix$toc](/ru/docs/MDN/Tools/URL-suffix$toc)

- `$json`

  - : Сообщает Kuma описать страницу в объекте JSON. Этот объект по сути тот же, что и при использовании подпрограммы KumaScript `wiki.getPage()`.

    **Пример:** [/ru/docs/MDN/About$json](/ru/docs/MDN/About$json)

- `$children`

  - : Говорит Kuma перечислить дочерние темы страницы в JSON. Этот объект по сути тот же, что и при использовании подпрограммы KumaScript `pages.subpages()`.

    **Пример:** [/ru/docs/MDN/Contribute$children](/ru/docs/MDN/Contribute$children)

    (`М`можно использовать с параметром `?expand` для получения более подробного ответа.)

- `$compare`

  - : Представляет различия строк исходного текста между ревизиями, указанными в требуемых параметрах запроса `?from` и `?to`.

    **Пример:** [/ru/docs/Web/API/KeyboardEvent/key/Key_Values$compare?locale=ru\&to=1651013\&from=1650680](/ru/docs/Web/API/KeyboardEvent/key/Key_Values$compare?locale=ru&to=1651013&from=1650680)

- `$edit`

  - : Редактирует текущую ревизию данного документа вместо его отображения.

    **Пример:** [/ru/docs/MDN/Tools/URL-suffix$edit](/ru/docs/MDN/Tools/URL-suffix$edit)

- `$history`

  - : Показывает историю последних десяти ревизий данного документа вместо его содержимого. Полную историю можно запросить с помощью значения параметра запроса `?limit=all`.

    **Пример:** [/ru/docs/MDN/Tools/URL-suffix$history?limit=all](/ru/docs/MDN/Tools/URL-suffix$history?limit=all)

- `$revision`

  - : Отображает номер ревизии документа, который необходимо указать после разделителя «/».

    **Пример:** [/ru/docs/MDN/Tools/URL-suffix$revision/1652169](/ru/docs/MDN/Tools/URL-suffix$revision/1652169)