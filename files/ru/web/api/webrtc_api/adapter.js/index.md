---
title: Увеличиваем совместимость с WebRTC adapter.js
slug: Web/API/WebRTC_API/adapter.js
tags:
  - adapter.js
translation_of: Web/API/WebRTC_API/adapter.js
---
{{WebRTCSidebar}}

Несмотря на то, что WebRTC [спецификация](http://www.w3.org/TR/webrtc/) относительно стабильна, не все ещё браузеры полностью реализуют её функциональность. Некоторые реализации в браузерах все ещё содержат префиксы производителей в некоторых, или даже всех WebRTC интерфейсах, и разработчик может самостоятельно, в ручную, учесть вопросы несовместимости в своём коде. Но есть более простой выход. Организация WebRTC [предлагает библиотеку adapter.js](https://github.com/webrtc/adapter/) для обработки вопросов несовместимостей в различных браузерных реализациях WebRTC. Эта библиотека является JavaScript клином, позволяющим писать код в соответствии со спецификацией, чтобы он работал во всех браузерах с различным уровнем поддержки WebRTC. С ней нет необходимости условно использовать префиксные интерфейсы или реализовывать обходные пути

> **Примечание:** **Примечание :** Поскольку функциональность и названия API-терминов в WebRTC и поддерживаемых браузерах постоянно изменяются, обычно рекомендуется использовать этот адаптер.

Адаптер предоставляется по лицензии [BSD-style license](https://github.com/webrtc/adapter/blob/master/LICENSE.md).

## Как работает adapter.js

Для каждой версии браузера, поддерживающего WebRTC, `adapter.js` реализует необходимые полизаполнители, устанавливает имена API без префиксов и применяет любые другие изменения, необходимые для того, чтобы браузер выполнял код, в соответствии со спецификацией WebRTC.

Например, в версиях Firefox старше 38 адаптер добавляет свойство {{domxref ("RTCPeerConnection.urls")}}; Firefox изначально не поддерживает это свойство до Firefox 38, а в Chrome адаптер добавляет поддержку API {{jsxref ("Promise")}}, если он отсутствует. Это всего лишь пара примеров. Вот в кратце, какие корректировки производит библиотека.

В настоящее время адаптер WebRTC поддерживает Mozilla Firefox, Google Chrome, Apple Safari и Microsoft Edge.

## Использование adapter.js

Для того чтобы использовать `adapter.js`, вам нужно включить `adapter.js` в любую страницу, которая использует API WebRTC:

1. Скопируйте [последнюю версию adapter.js](https://github.com/webrtc/adapter/tree/master/release) с GitHub.
2. Поместите копию в структурную директорию вашего сайта (к примеру, в корневую директорию скриптов).
3. Поместите элемент скрипта со ссылкой на библиотеку `adapter.js` в ваш проект: `<script src="adapter.js"></script>`
4. При кодировании, используйте интерфейсы WebRTC как указано в спецификации (без всяких префиксов производителей) , будучи уверенным, что он будет работать во всех браузерах .
5. Помните, что даже присутствие хорошего клина, не означает отмену тестирования вашего кода на различных браузерах (а идеально, и в различных версиях каждого браузера).

## Смотрите также

- [Проект WebRTC adapter.js на GitHub](https://github.com/webrtc/adapter)