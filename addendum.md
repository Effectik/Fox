# Приложение

* [Шапка](header.md)
  * [FAQ](header.md#user-content-faq)
  * [Аддоны](header.md#user-content-Аддоны)
* **Приложение**
  * [Настройки about:config](addendum.md#user-content-Настройки-aboutconfig)
  * [Продвинутые аддоны](addendum.md#user-content-Продвинутые-аддоны)
  * [Интересные ссылки](addendum.md#user-content-Интересные-ссылки)
    * [Безопасность](addendum.md#user-content-Безопасность)
    * [Приватность](addendum.md#user-content-Приватность)
* [Серый список аддонов](greylist.md)

Эта часть для тех, кто хочет настроить свой браузер еще больше. Настройки для повышения удобства, производительности, безопасности и отключения различных зондов, полезные аддоны, интересные ссылки и т.п.

**Важное замечание**: Это памятка с интересными настройками и аддонами. Здесь пока (?) нет готового рецепта для максимальной анонимности. Если вы пришли за этим, проследуйте [сюда](https://anonymous-proxy-servers.net/en/jondofox.html) или [сюда](https://www.torproject.org/).

<sub>Стандартный дисклеймер раз: я включил краткие пояснения к каждой настройке и аддону, но если вы четко не понимаете за что они отвечают и что у вас может отвалиться в результате их установки, лучше не трогайте.</sub>

<sub>Стандартный дисклеймер два: следует помнить, что меры для достижения анонимности и безопасности зачастую противоположны друг другу, ибо чем больше вы меняете дефолтное поведение браузера и отключаете включенных по умолчанию механизмов, тем уникальнее становится его отпечаток. Если в приоритете именно анонимность, а не безопасность с анонимностью по остаточному принципу, многие зонды лучше не выключать, а скармливать им ложную информацию, маскирующую вас под типичного юзера. Думайте сами, что вам нужнее.</sub>

## Настройки about:config
Поддерживаемые на данный момент версии Firefox: **45 - 57**. <br>

Приведенные здесь настройки условно разделены на следующие категории:

1. [Настройки](prefs/prefs_1.js) относительно безопасные - меняя их, ничего нужного не отвалится, и кое-что улучшится.
2. [Настройки](prefs/prefs_2.js), ломающие не особо нужную функциональность.
3. [Настройки](prefs/prefs_3.js), ломающие нужную некоторым функциональность.
4. [Настройки](prefs/prefs_4.js), еще больше ломающие функциональность. Их отключают либо для повышения безопасности, либо для повышения анонимности. А также все, что не подошло в первые три категории.
5. [Настройки](prefs/prefs_exp.js) для энтузиастов. Ничего особо не ломают, но рассчитаны на тех, кто использует браузер нетривиальными способами.

**Не следует** бездумно копировать себе все целиком из четвертой категории. Внимательно посмотрите и решите, что именно вам нужно. Из второй - можно, но все же рекомендуется прочитать перед этим.

Применить эти настройки можно, дописав их в конец находящегося в профиле `prefs.js`, либо создав там же файл `user.js` и записав их в него. Но не забудьте, что вы это сделали, потому что записанные в `user.js` настройки будут откатываться на указанные там значения при каждом перезапуске браузера, даже если вы меняли их другими способами (about:config, Preferences, etc). Подробнее [здесь](http://kb.mozillazine.org/User.js_file).

Кроме того, `user.js` можно (и нужно) создавать в еще ни разу не запускавшемся профиле. Т.е.: создаем профиль в Profile Manager, но **не** нажимаем Start Firefox, когда профиль уже создан. Идем в пустую папку свежесозданного профиля и записываем туда `user.js` с нужными настройками. Он применится при запуске и в результате у вас с самого начала не будет никаких нежелательных соединений и загрузок вроде БД Safebrowsing, OpenH264-кодека и т.п.

##### Список ломающихся от применения настроек сайтов

* Спуфинг заголовка Referer -- Avito.ru (показ телефонов), сервисы Яндекса (при использовании вместе с Decentraleyes), qiwi.com (авторизация), simplenote.com (авторизация), rapidgator.net (капча).
* `dom.event.clipboardevents.enabled` -- GitHub (копирование текста из редактора).
* `security.ssl.require_safe_negotiation` -- Instagram, Mega.nz, многие другие.
* `dom.enable_performance` -- pornhub.com (авторизация).
* `dom.indexedDB.enabled` -- **Violentmonkey** ([аддон](https://bugzilla.mozilla.org/show_bug.cgi?id=1335919)), Twitter, Google Drive, Mega.nz. Поломка может быть частично исправлена [юзерскриптом](userjs/no-indexed-db.user.js).
* `security.ssl3.rsa_des_ede3_sha` -- https://login.skype.com/login
* `geo.enabled` -- citilink.ru (панель фильтров).
* `general.useragent.override` -- Неправдоподобно выглядящий useragent ломает maps.yandex.ru и много что еще.
* `svg.disabled` -- youtube.com (плеер).

## Продвинутые аддоны
<sub>`E10S` - совместимые с Electrolysis расширения. <br>
<s>`E10S`</s> - не совместимые, либо работающие через прослойку для совместимости (interposition). <br>
`WE` - Web Extensions, совместимы с E10S. <br>
`WE, E10S` - есть как Web Extension, так и старая версия расширения, которую можно использовать на Firefox 52 ESR.
</sub>

* [HTTPS Everywhere](https://addons.mozilla.org/en-us/firefox/addon/https-everywhere/)
<sup>WE, E10S</sup>
Содержит список сайтов, поддерживающих как HTTP, так HTTPS, и автоматически меняет все HTTP-ссылки, ведущие к этим сайтам, на HTTPS. Аддон вернули на AMO, но на всякий случай - [ссылка](https://www.eff.org/https-everywhere/) на официальный сайт. Правила обновляются редко, актуальную версию правил можно получить [на GitHub](https://github.com/EFForg/https-everywhere), там же можно отправить новое правило.

* [MixedContentHunter](https://addons.mozilla.org/en-US/firefox/addon/mixedcontenthunter/)
<sup>WE</sup>
Аддон меняет HTTP на HTTPS в запросах ресурсов документом, загруженным через HTTPS. Есть белый список на случай ломки сайта от такого поведения.

* [SSleuth](https://addons.mozilla.org/en-US/firefox/addon/ssleuth/)
<sup>E10S</sup>
([GitHub](https://github.com/sibiantony/ssleuth)) Показывает информацию об используемых криптопримитивах и фичах TLS/SSL в шифрованных соединениях.

* [RefControl](https://addons.mozilla.org/en-US/firefox/addon/refcontrol/)
<sup><s>E10S</s></sup>
Резалка [рефереров](https://en.wikipedia.org/wiki/HTTP_Referer). Можно тонко тюнить, а можно рубить только рефереры при переходе на другой домен (Block (3rd party)), оставляя внутридоменные, что просто, эффективно для 99% случаев и не ломает так много сайтов как полный запрет.

* [CleanLinks](https://github.com/diegocr/CleanLinks)
<sup><s>E10S</s></sup>
Чистит ссылки от редирект-префиксов Гугла и т.п. Имеет белый список как доменов, так и рэгэкспов, чтобы пропускать ссылки со всякими нужными префиксами вроде auth, ServiceLogin и т.п.

* [Skip Redirect](https://addons.mozilla.org/en-US/firefox/addon/skip-redirect/)
<sup>WE</sup>
Альтернатива CleanLinks. Также имеет белый список для исключений, позволяющий пропускать ссылки с нужными префиксами.

* [Google search link fix](https://addons.mozilla.org/en-US/firefox/addon/google-search-link-fix/)
<sup>WE, E10S</sup>
Более простая альтернатива CleanLinks для тех, кого он по каким-то причинам не устраивает. Работает только на Google, Yandex и Yahoo.

* [Neat URL](https://addons.mozilla.org/en-US/firefox/addon/neat-url/)
<sup>WE</sup>
Чистит ссылки, удаляя из них мусорные параметры вроде utm_source, использующиеся для трекинга. Список параметров настраивается - можно добавлять как глобальные правила, так и для определенных доменов.

* [Cookie Monster](https://addons.mozilla.org/en-US/firefox/addon/cookie-monster/)
<sup><s>E10S</s></sup>
Режет cookies и DOM Storage для сайтов, не внесенных в белый список.

* [Cookie Controller](https://addons.mozilla.org/en-US/firefox/addon/cookie-controller/)
<sup>E10S</sup>
Альтернатива Cookie Monster. После установки следует вручную вытащить кнопки на тулбар через Customize. Настройки находятся в меню Tools (Alt+T) -> Cookie Controller.

* [Self-Destructing Cookies](https://addons.mozilla.org/en-US/firefox/addon/self-destructing-cookies/)
<sup><s>E10S</s></sup>
Самоуничтожение кук после закрытия всех вкладок с соответствующим сайтом. Может быть удобнее чем полная блокировка.

* [Cookies Exterminator](https://addons.mozilla.org/en-US/firefox/addon/cookies-exterminator/)
<sup><s>E10S</s></sup>
Еще один аддон для автоматического удаления cookies и DOM Storage после закрытия использующих их вкладок.

* [BetterPrivacy](https://addons.mozilla.org/en-US/firefox/addon/betterprivacy/)
<sup>E10S</sup>
Менее актуально с понижением числа пользователей Flash, но все же. Уничтожает [LSO](https://en.wikipedia.org/wiki/Local_shared_object), которые не может заблокировать или уничтожить сам браузер.

* [NoScript](https://addons.mozilla.org/en-US/firefox/addon/noscript/)
<sup>WE, E10S</sup>
Блокировщик JS с возможностью работы в режиме белого или черного списка. Поможет тем, у кого в простое вкладки с тяжелым JS отжирают ресурсы CPU.

	* **ВАЖНО:** См. [информацию о NoScript в сером списке](greylist.md#user-content-noscript).

* [RequestPolicy Continued](https://addons.mozilla.org/en-US/firefox/addon/requestpolicy-continued/)
<sup><s>E10S</s></sup>
Резалка кросс-доменных запросов. Можно (и рекомендуется самим автором) использовать в связке с NoScript.

* [uMatrix](https://addons.mozilla.org/en-US/firefox/addon/umatrix/)
<sup>WE, E10S</sup>
Самая многофункциональная из резалок кросс-доменных запросов. Может блокировать запросы в зависимости от типа контента. Также умеет блокировать XHR (отдельно от обычных запросов), скрипты, куки, рефереры, плагины, медиа (HTML5 аудио и видео) и вебсокеты. Документацию еще не перенесли целиком из старого проекта, на котором основан uMatrix, так что если что непонятно, смотреть не только [здесь](https://github.com/gorhill/uMatrix/wiki), но и [здесь](https://github.com/gorhill/httpswitchboard/wiki).

	* <sub>Алгоритм блокирования кук несколько отличается от того, что у Cookie Monster и Cookie Controller - первые два не дают сайтам устанавливать куки, а uMatrix дает ставить, но не дает читать, убирая из всех HTTP-запросов заголовок Cookie (но при этом через document.cookie установленные куки все еще видны), а через некоторое время - подчищает. Также в отличие от CM/CC, uMatrix не умеет запрещать писать в DOM Storage, а может только периодически его очищать.</sub>

* [NoRedirect](https://addons.mozilla.org/en-US/firefox/addon/noredirect/)
<sup><s>E10S</s></sup>
Рубит редиректы по рэгэкспам исходного или целевого URL.

* [Redirect Control](https://addons.mozilla.org/en-US/firefox/addon/redirect-control/)
<sup><s>E10S</s></sup>
Еще один блокировщик редиректов. Развивается в отличие от давно не обновлявшегося NoRedirect.

* [Redirector](https://addons.mozilla.org/en-US/firefox/addon/redirector/)
<sup>WE, E10S</sup>
Позволяет задавать пользовательские редиректы по паттернам или регулярным выражениям.

* [HttpFox](https://addons.mozilla.org/en-US/firefox/addon/httpfox/)
<sup><s>E10S</s></sup>
Мониторит все HTTP-запросы браузера. Показывает заголовки, параметры GET/POST и статус запроса (в т.ч. был ли он выполнен, взят из кэша, или отменен (NS_BINDING_ABORTED) самим браузером/другим аддоном).

* [User Agent Switcher](https://addons.mozilla.org/en-US/firefox/addon/user-agent-switcher/)
<sup><s>E10S</s></sup>
и [списки к нему](http://techpatterns.com/downloads/firefox/useragentswitcher.xml).

* [Random Agent Spoofer](https://addons.mozilla.org/en-US/firefox/addon/random-agent-spoofer/)
<sup><s>E10S</s></sup>
Меняет юзер-агенты по таймеру и с дополнительными фичами, препятствующими фингерпринтингу. Версия с GitHub имеет расширенную функциональность по сравнению с версией с AMO (см. описание на AMO).

* [CanvasBlocker](https://addons.mozilla.org/en-US/firefox/addon/canvasblocker/)
<sup>WE, E10S</sup>
Предотвращает фингерпринтинг через [анализ особенностей рендеринга элемента &lt;canvas&gt;](https://en.wikipedia.org/wiki/Canvas_fingerprinting), зависящих от ОС, железа, драйверов, шрифтов и т.п. Также см. [Bug 967895](https://bugzilla.mozilla.org/show_bug.cgi?id=967895).

* [Decentraleyes](https://addons.mozilla.org/en-US/firefox/addon/decentraleyes/)
<sup>WE, E10S</sup>
Аддон содержит популярные библиотеки (AngularJS, Backbone.js, Dojo, Ember.js, Ext Core, jQuery, jQuery UI, Modernizr, MooTools, Prototype, Scriptaculous, SWFObject, Underscore.js) и предотвращает обращения сайтов за ними ко внешним 3rd-party CDN, предоставляя вместо этого локальные копии.

	* Расширение экспериментальное и может ломать некоторые сайты. Известны проблемы с Yandex.Disk.

* [No Resource URI Leak](https://addons.mozilla.org/en-US/firefox/addon/no-resource-uri-leak/)
<sup>E10S</sup>
Предотвращает фингерпринтинг по внутренним URL браузера со схемой resource://, запрещая веб-страницам доступ к ним. Может сломать некоторые другие расширения. Подробнее о проблеме: [Ghacks](https://www.ghacks.net/2016/06/12/firefox-resource-leak/), [Bug 863246](https://bugzilla.mozilla.org/show_bug.cgi?id=863246), [Bug 903959](https://bugzilla.mozilla.org/show_bug.cgi?id=903959). Протестировать можно на Browserleaks: https://browserleaks.com/firefox
<br> **UPD:** В Firefox 57 [баг 863246](https://bugzilla.mozilla.org/show_bug.cgi?id=863246) исправлен, и необходимости в этом расширении больше нет.

* [Privacy Badger](https://addons.mozilla.org/en-US/firefox/addon/privacy-badger17/)
<sup>WE, E10S</sup>
Аналог Ghostery от EFF. Актуально для тех, кто хочет поставить и забыть, чтоб оно там автоматом боролось с трекингом.

## Разное

### Пользовательские стили

#### Полезные стили

* [Dim Unloaded Tabs](https://userstyles.org/styles/71928/dim-unloaded-tabs). Затемнение незагруженных после перезапуска браузера вкладок.

* [Custom CSS tweaks for Firefox 57+](https://github.com/Aris-t2/CustomCSSforFx). Сборник различных стилей от автора аддона Classic Theme Restorer.

#### О написании собственных стилей

В качестве изкоробочной альтернативы меняющим стили аддонам, можно использовать файлы [userChrome.css](http://kb.mozillazine.org/UserChrome.css) и [userContent.css](http://kb.mozillazine.org/UserContent.css). Если редактировать их из [Browser Toolbox](https://developer.mozilla.org/en-US/docs/Tools/Browser_Toolbox), изменения вступают в силу без перезапуска браузера. Также через Browser Toolbox удобно инспектировать элементы интерфейса самого браузера.

Некоторая пригождающаяся информация есть в [Stylish Wiki](https://github.com/stylish-userstyles/stylish/wiki).

#### Опасность юзерстилей с -moz-binding
В мозилловском CSS есть специальное предназначенное для использования с XUL свойство [-moz-binding](https://developer.mozilla.org/en-US/docs/Web/CSS/-moz-binding), при помощи которого можно привязать к элементу обработчики различных событий. Для CSS веб-страниц вытекающие из этого уязвимости давно закрыли: [bug 324253](https://bugzilla.mozilla.org/show_bug.cgi?id=324253), [bug 379959](https://bugzilla.mozilla.org/show_bug.cgi?id=379959).

Однако стили в user**Chrome**.css могут модифицировать интерфейс Firefox. Поэтому они обладают всеми возможностями стилей самого браузера и аддонов, соответственно, встроенные в них через -moz-binding обработчики выполнятся уже с правами chrome, а не content. При этом код обработчика, который обычно находится по адресу chrome:// для стилей самого браузера, может быть задан и в самом стиле в виде Data URI, так что проверку на same-origin он пройдет успешно. В результате подобные стили представляют из себя не меньшую опасность чем непроверенные аддоны.

Вот, например, самое простое, что можно сделать - поменять настройки прокси в браузере. Биндинг в нижеприведенном стиле меняет их на 127.0.0.1:8888. Работает с указанием namespace XUL и без него (с namespace HTML - не работает).

```
@namespace url(http://www.mozilla.org/keymaster/gatekeeper/there.is.only.xul);

#main-window {
  -moz-binding: url("data:text/xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIj8+CjxiaW5kaW5ncyB4bWxucz0iaHR0cDovL3d3dy5tb3ppbGxhLm9yZy94YmwiCiAgICB4bWxuczp4dWw9Imh0dHA6Ly93d3cubW96aWxsYS5vcmcva2V5bWFzdGVyL2dhdGVrZWVwZXIvdGhlcmUuaXMub25seS54dWwiCiAgICB4bWxuczp4Ymw9Imh0dHA6Ly93d3cubW96aWxsYS5vcmcveGJsIj4KICAgIDxiaW5kaW5nIGlkPSJleHBsb2l0Ij4KICAgICAgICA8aW1wbGVtZW50YXRpb24+CiAgICAgICAgICAgIDxjb25zdHJ1Y3Rvcj4KICAgICAgICAgICAgICAgIC8vIDwhW0NEQVRBWwogICAgICAgICAgICAgICB2YXIgcHJlZnMgPSBDb21wb25lbnRzLmNsYXNzZXNbIkBtb3ppbGxhLm9yZy9wcmVmZXJlbmNlcy1zZXJ2aWNlOzEiXS5nZXRTZXJ2aWNlKENvbXBvbmVudHMuaW50ZXJmYWNlcy5uc0lQcmVmU2VydmljZSkuZ2V0QnJhbmNoKCJuZXR3b3JrLnByb3h5LiIpOwogICAgICAgICAgICAgICBwcmVmcy5zZXRJbnRQcmVmKCJ0eXBlIiwgMSk7CiAgICAgICAgICAgICAgIHByZWZzLnNldENoYXJQcmVmKCJzb2NrcyIsICIxMjcuMC4wLjEiKTsKCSAgICAgICBwcmVmcy5zZXRJbnRQcmVmKCJzb2Nrc19wb3J0IiwgODg4OCk7CiAgICAgICAgICAgICAgICAvLyBdXT4KICAgICAgICAgICAgPC9jb25zdHJ1Y3Rvcj4KICAgICAgICA8L2ltcGxlbWVudGF0aW9uPgogICAgPC9iaW5kaW5nPgo8L2JpbmRpbmdzPgo=");
}
```

Userstyles.org [не пропускает](https://github.com/stylish-userstyles/stylish/issues/159) стили, содержащие свойство -moz-binding, поэтому внимательно проверять нужно только стили, устанавливаемые из  других источников.

### Хак для отключения требования подписей аддонов
Изобретен пользователями форума Mozilla Russia[[1]](https://forum.mozilla-russia.org/viewtopic.php?id=70321)[[2]](https://forum.mozilla-russia.org/viewtopic.php?id=70326). После применения может потребоваться переустановка отключенных браузером неподписанных аддонов.

Создайте файл `config.js` в папке с установленным Firefox: `C:\Program Files\Mozilla Firefox`
```
//
try {
    Components.utils.import("resource://gre/modules/addons/XPIProvider.jsm", {})
        .eval("SIGNED_TYPES.clear()");
} catch(ex) {}
```

Создайте файл `config-prefs.js` в папке `C:\Program Files\Mozilla Firefox\defaults\pref`
```
pref("general.config.obscure_value", 0);
pref("general.config.filename", "config.js");
```

## Интересные ссылки
* [Release Notes](https://www.mozilla.org/en-US/firefox/notes) и [Developer Release Notes](https://developer.mozilla.org/en-US/Firefox/Releases).
* [Ghacks](https://www.ghacks.net/category/firefox/) - сайт, на котором попадаются неплохие статьи и обзоры грядущих нововведений в Firefox.
* [Здесь](http://kb.mozillazine.org/About:config_entries) и [здесь](http://kb.mozillazine.org/Category:Preferences) приведены подробные описания настроек, жаль, не всех.
* [user.js -- Firefox hardening stuff](https://github.com/pyllyukko/user.js) - репозиторий настроек вроде этого, но с несколько другим подходом к организации.
* [Блог](https://cat-in-136.github.io/tags.html#tag_pref%20diff) автора аддона Configuration Mania, который выкладывает разницу между дефолтными конфигами предыдущей и новой версии Firefox. **UPD:** Настройки могут меняться и в более поздних бетах, чем там сравниваются, поэтому целиком полагаться на него не стоит.

#### Безопасность
* [Список исправленных уязвимостей](https://www.mozilla.org/en-US/security/known-vulnerabilities/firefox/)
* [Описание](https://developer.mozilla.org/en-US/Add-ons/AMO/Policy/Reviews) процедуры ревью аддонов на AMO.
* Атаки через подмену содержимого буфера обмена
  * С использованием JavaScript:
    * https://www.opennet.ru/opennews/art.shtml?num=44481
    * https://security.love/Pastejacking/
  * Без использования JavaScript, на чистом HTML: https://thejh.net/misc/website-terminal-copy-paste

#### Приватность
* [Неплохой обзор от Mozilla](https://support.mozilla.org/en-US/kb/how-stop-firefox-making-automatic-connections) с описаниями механизмов, из-за которых Firefox может инициировать соединения без прямого приказа пользователя. Еще: [соединения](http://kb.mozillazine.org/Connections_established_on_startup_-_Firefox), устанавливающиеся при запуске браузера. Настройки для отключения подобной самодеятельности есть здесь, в разделе "Настройки".
* [PrivacyTools.io](https://www.privacytools.io) - сайт, посвященный инструментам для обеспечения приватности. Можно предлагать дополнения и улучшения в их [репозитории на GitHub](https://github.com/privacytoolsIO/privacytools.io).
* [Evercookie](http://samy.pl/evercookie/). Собирательное название для техник помещения трекинг-идентификаторов в разные труднодоступные места помимо cookies, LSO и DOM Storage.
* Фингерпринтинг
  * Такие методы обнаружения, для которых не требуется запись уникального идентификатора на машину пользователя.
  * [Обзор](https://wiki.mozilla.org/Fingerprinting) методов фингерпринтинга в Mozilla Wiki и [предложения](https://wiki.mozilla.org/Security/Anonymous_Browsing) по улучшению анонимности браузера.
  * [Обзор](https://www.chromium.org/Home/chromium-security/client-identification-mechanisms) способов идентификации на сайте проекта Chromium.
  * [Tor Uplft](https://wiki.mozilla.org/Security/Tor_Uplift/Tracking) - проект по переносу патчей Tor Browser в основную ветку Firefox.
  * Проверить себя на уникальность отпечатка можно на следующих ресурсах:
    * https://panopticlick.eff.org/
    * http://ip-check.info/?lang=en
    * https://amiunique.org/
    * https://whoer.net/
    * https://browserleaks.com/
    * http://browserspy.dk/
  * Статьи по теме:
    * [Как Tor Project борется с фингерпринтингом](https://geektimes.ru/post/244484/) (более свежая [английская версия статьи](https://github.com/KOLANICH/Article-2015-Dull-captaincy-or-the-way-Tor-Project-fights-browser-fingerprinting)).
    * [Флаги HSTS и их использование для фингерпринтинга](https://geektimes.ru/post/244065/)
