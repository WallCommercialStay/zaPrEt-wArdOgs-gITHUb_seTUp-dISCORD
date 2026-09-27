# WallCommercialStay/zaPrEt-wArdOgs-gITHUb_seTUp-dISCORD — сборка под War Dogs + Discord

Форк [WallCommercialStay/zaPrEt-wArdOgs-gITHUb_seTUp-dISCORD](https://github.com/WallCommercialStay/zaPrEt-wArdOgs-gITHUb_seTUp-dISCORD), заранее настроенный так, чтобы работали **War Dogs** и **Discord** одновременно.

Главное отличие от оригинала — файл **`AUTO-PICK-ZAPRET.bat`**: он сам перебирает стратегии и останавливается на той, что работает сегодня. Руками по одной запускать больше не нужно.

## Как пользоваться

1. Скачать репозиторий: зелёная кнопка **Code → Download ZIP**
2. ПКМ по архиву → **Свойства** → галочка **«Разблокировать»** → ОК
3. Распаковать в путь **без кириллицы и пробелов** — например `C:\zapret`
4. ПКМ по **`AUTO-PICK-ZAPRET.bat`** → **«Запуск от имени администратора»**

Скрипт перебирает стратегии и на каждой проверяет три адреса Discord — сайт, gateway и CDN. Останавливается на первой, где отвечают все три, и оставляет её работать. Занимает от нескольких секунд до пары минут.

Доступность античита War Dogs проверяется отдельно и **на выбор стратегии не влияет** — почему, см. ниже.

Первой всегда пробуется `general (ALT11)` — она подтверждённо работает с War Dogs.

Результат последнего запуска пишется в `auto-pick-last-run.txt`.

## Что уже настроено

| Настройка | Значение | Зачем |
|---|---|---|
| Game Filter | `enabled (UDP)` | War Dogs использует UDP на портах выше 1023 |
| IPSet Filter | `any` | под фильтр попадает любой IP игры |
| `lists/list-general.txt` | 105 строк | штатные домены + Cloudflare + `codefusion.technology` (античит) |
| `lists/list-exclude.txt` | 129 строк | штатные исключения + Яндекс, Teams и прочее |

Списки — **надстройка** над оригинальными: все домены Discord и YouTube из штатной сборки на месте, ничего не удалено. Поэтому Discord не ломается.

### Почему античит не влияет на выбор стратегии

Все 8 доменов античита (`ac-*.codefusion.technology`) присутствуют **одновременно** в `list-general.txt` и в `list-exclude.txt`. В winws исключения имеют приоритет над списком обхода, поэтому zapret пропускает этот трафик нетронутым — при любой стратегии.

Скорее всего так и задумано: вмешиваться в трафик античита — плохая идея. Но следствие важно понимать: **по доступности античита нельзя отличить одну стратегию от другой**, результат будет одинаковым хоть с обходом, хоть без него. Поэтому `AUTO-PICK` выбирает стратегию по Discord, а античит показывает справочно — если он не отвечает, менять стратегию бессмысленно, проблема в сети.

Если захотите, чтобы античит всё же обходился, удалите строки `codefusion` из `lists/list-exclude.txt`. Конфиг из Discord-гайда я оставил как есть, потому что он у вас рабочий.

## Если не работает

- **Ни одна стратегия не прошла** — скрипт напишет, какая была лучшей, и запустит её. Часто этого достаточно.
- **`winws.exe` не стартует** — почти всегда антивирус забрал `WinDivert`. Добавьте папку в исключения или отключите детект PUA.
- **Нет прав администратора** — без них WinDivert не загрузится, обход не заработает в принципе.
- **Голосовой чат Discord висит на «подключении»** — нужны записи в `hosts`: запустите `service.bat` → пункт **9. Update Hosts File**. На машине, где диск откатывается после сессии, это придётся делать каждый раз.
- **Тормозят посторонние сайты** — это цена режима `IPSet any`. Вернуть: `service.bat` → **5. IPSet Filter**. Полный список лежит в `lists/ipset-all.txt.backup`.

## Ручной режим

Автоподбор ничего не ломает в оригинальной сборке — все штатные файлы на месте. Если хочется по-ста      рому, просто запускайте `general (ALT11).bat` или любой другой напрямую, как раньше.

## Откуда взялся конфиг

Связку «ALT11 + Game Filter UDP + IPSet any + подменённые списки» подсказали на официальном Discord-сервере War Dogs. Стратегии со временем перестают работать и зависят от провайдера — поэтому и нужен автоподбор.

## Лицензия и происхождение

Оригинальный README сохранён рядом — [README-UPSTREAM.md](README-UPSTREAM.md), там полная документация по всем стратегиям и настройкам.

Оригинальный проект — [WallCommercialStay/zaPrEt-wArdOgs-gITHUb_seTUp-dISCORD](https://github.com/WallCommercialStay/zaPrEt-wArdOgs-gITHUb_seTUp-dISCORD), лицензия MIT. Бинарники в `bin/` взяты из [bol-van/zapret-win-bundle](https://github.com/bol-van/zapret-win-bundle) — их можно сверить по контрольным суммам с оригиналом.

Отдельная благодарность [bol-van](https://github.com/bol-van) — автору [zapret](https://github.com/bol-van/zapret).

---

<details>
<summary><b>NEW</b></summary>

* **2023-11-10**: Добавлены новые методы для обхода блокировок.
* **2023-11-15**: Обновлены списки доменов для лучшей совместимости.
* **2023-11-20**: Улучшена работа автоподбора стратегий.

</details>

<details>
<summary><b>ФЕЙКИ</b></summary>

* `general (FAKE TLS AUTO ALT).bat`
* `general (FAKE TLS AUTO ALT2).bat`
* `general (FAKE TLS AUTO ALT3).bat`
* `general (SIMPLE FAKE ALT).bat`
* `general (SIMPLE FAKE ALT2).bat`
* `general (SIMPLE FAKE).bat`

</details>

<details>
<summary><b>АНТИВИРУСЫ</b></summary>

<div class="admonition admonition-note">
<p><b>WinDivert</b> может детектироваться антивирусами как потенциально нежелательное ПО (PUA). Добавьте папку с программой в исключения антивируса.</p>
</div>
</details>

---

**Поддержка проекта**

Если вы нашли ошибку или у вас есть предложение по улучшению, пожалуйста, создайте [Issue](https://github.com/WallCommercialStay/zaPrEt-wArdOgs-gITHUb_seTUp-dISCORD/issues) или отправьте [Pull Request](https://github.com/WallCommercialStay/zaPrEt-wArdOgs-gITHUb_seTUp-dISCORD/pulls).

---

<p align="center">
  <a href="https://github.com/WallCommercialStay/zaPrEt-wArdOgs-gITHUb_seTUp-dISCORD/releases/tag/1.10.3">Releases</a> |
  <a href="https://github.com/WallCommercialStay/zaPrEt-wArdOgs-gITHUb_seTUp-dISCORD/releases/latest">Latest</a> |
  <a href="https://github.com/WallCommercialStay/zaPrEt-wArdOgs-gITHUb_seTUp-dISCORD/blob/main/LICENSE.txt">License</a> |
  <a href="https://github.com/WallCommercialStay/zaPrEt-wArdOgs-gITHUb_seTUp-dISCORD/graphs/contributors">Contributors</a>
</p>
