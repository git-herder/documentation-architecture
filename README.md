# Архитектурная модель Git Herder

SSOT **структуры приложения** в нотации ArchiMate. Исполняемый код и
прикладные HTTP-контракты здесь **не** дублируются — см.
[спецификации](../specifications/README.md) и [ADR-26110801][adr-layout].

Канонический артефакт — [git-herder.archimate](git-herder.archimate) (редактор
Archi или совместимый инструмент). Резервная копия `.bak` — не SSOT.

## Навигация: view → документы

| View в модели | Содержание | Документы |
| ------------- | ---------- | --------- |
| **SCM Listing & Enrichment** | ScmClientFactory, Builder'ы, runtime-интерфейсы ScmListing / ScmEnrich, platform-адаптеры, ScmHttpTransport | [scm/index.md § ArchiMate][scm-archimate], [ADR-26110801][adr-layout] |
| **Report command flow** | Процесс «Загрузка из SCM и обогащение карточек» (`id-649305ae`) в сценарии report | [scm/index.md][scm-index], [cli/report/index.md](../specifications/cli/report/index.md) |
| **sync** | Sync command flow (`id-ac49f18a`): отбор копий, граница ретрая sync, pull и push через GitCliRunner | [cli/sync/index.md][cli-sync] |

Оркестрация фаз listing → enrichment → enumeration — SSOT в
[scm/index.md][scm-index]. Раскладка hub / listing / enrichment /
enumeration — [ADR-26102201][adr-hub].

## ArchiMate → пакеты Go

Таблица «компонент → пакет» и дерево `application/` — только в
[ADR-26110801][adr-layout] (имена интерфейсов в Go: `Listing`, `ListingBuilder`;
в модели: **ScmListing**, **ScmListingBuilder**).

## HTTP-контракты SCM

Не описывать в README модели. Server-side list и обогащение — per `upstream`:

- `documentation/specifications/scm/<upstream>/repository-listing/`
- `documentation/specifications/scm/<upstream>/repository-enrichment/`

<!-- LINKS -->
[scm-index]: ../specifications/scm/index.md
[scm-archimate]: ../specifications/scm/index.md#archimate-scm-application
[adr-layout]: ../../ADR/ADR-26110801-go-package-layout.md
[adr-hub]: ../../ADR/ADR-26102201-scm-selection-hub-extension-specs.md
[cli-sync]: ../specifications/cli/sync/index.md
