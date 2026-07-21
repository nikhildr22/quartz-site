# History Tables and Historization

This document explains how historization is implemented in CafFallfuhrung.

## 1. Core Approach

The project uses SQL Server temporal tables through Entity Framework Core.

At configuration level, historized entities are marked with temporal mapping:

```csharp
builder.ToTable(x => x.IsTemporal());
```

Example:
- `AddressEntityConfiguration` enables temporal mode for addresses.

## 2. Database-Level Representation

In migrations and snapshot metadata, temporal tables are represented with:

- A base table, for example `Addresses`
- A history table, for example `AddressesHistory`
- Two period columns:
  - `PeriodStart`
  - `PeriodEnd`

You can see this in migration designer/snapshot output where EF emits:

- `IsTemporal(...)`
- `UseHistoryTable("<TableName>History")`
- `HasPeriodStart("PeriodStart")`
- `HasPeriodEnd("PeriodEnd")`

This means inserts/updates/deletes automatically produce history rows at DB level.

## 3. Domain History Contract

Historized list models inherit from a shared base model:

- `HistoryModel`

Common fields are:

- `Id`
- `UpdateUserFullName`
- `UpdateDate`
- `PeriodStart`
- `PeriodEnd`

Filtering/paging for history is based on:

- `HistoryFilterPagingModel` with `Id`

So each history request is scoped to one entity id and then paged/sorted/filtered.

## 4. Query Pattern in Application Services

History queries follow a consistent pattern. Example (`AddressService.GetHistoryPagedAsync`):

1. Start from the DbSet in temporal mode:
   - `.TemporalAll()`
2. Scope to a concrete aggregate/entity id:
   - `.Where(x => x.Id == filterPaging.Id)`
3. Project into `...HistoryListModel`
4. Apply `.Sort(filterPaging)` and `.Filter(filterPaging)`
5. Return paged result via `ToPagedListAsync(...)`

The same pattern exists for:

- `PersonService`
- `AddressService`
- `ContactInformationService`
- `InstitutionService`
- `ExpertService`
- `ConsultingGoalService`
- `ConsultingActivityTaskService`
- `CaseCoreTopicService`
- `CaseReferenceService` (person/expert/institution variants)
- `DocumentService`
- `TimeEntryService`

## 5. Temporal Join Consistency (Important)

For history projections, related entities are also read temporally via `TemporalProjections`.

`TemporalProjections.JoinEntityQuery<TMainEntity, TJoinEntity>(...)` does the following:

- Reads the join set with `.TemporalAll()`
- Ensures the joined record is valid for the main record period using `PeriodStart` comparison
- Orders by descending `PeriodStart`

This avoids mixing a historic row of the main entity with a non-matching current state of related entities (for example, user names, translated names, contact types).

## 6. API Surface

History is exposed consistently in controllers, typically with two actions:

- `HistoryPaged...` (POST): returns paged history list
- `HistoryExport...` (POST): exports the same data to Excel

Example routes:

- `/api/Address/HistoryPaged`
- `/api/Address/HistoryExport`

Equivalent history endpoints exist for the entities listed above.

## 7. Angular Integration (Frontend)

The Angular frontend has a consistent history UX pattern across features.

### 7.1 Generated API client

History endpoints are consumed through generated services in:

- `src/app/core/services/api-services.ts`

Per entity, the generated client exposes methods like:

- `historyPaged(filterPaging)`
- `historyExport(filterPaging, timeZone)`

### 7.2 How users open history

In list/detail screens, a history action is shown (usually with a `history` icon):

- grid menu action or detail header button calls `onShowHistory(...)`
- that method opens a dedicated history dialog

Representative examples:

- `person-grid-table.component.ts` -> `PersonHistoryDialogComponent.open(...)`
- `person-detail.component.ts` -> `onShowHistoryOfPerson(...)`
- similar pattern in address/contact-information/institution/expert/document/time-entry/case-reference features

### 7.3 Dialog container pattern

Each entity has a history dialog container component that:

- extends `BaseDialogComponent`
- receives the entity id through `MAT_DIALOG_DATA`
- renders the matching history grid component

Example pattern:

- `person-history-dialog.component.ts`
- `person-history-dialog.component.html`

The dialog template passes the entity id and a small default page size to the grid, e.g. `[personId]="data.personId"` and `[initialPageSize]="5"`.

### 7.4 History grid component pattern

Each entity has a dedicated `*-history-grid-table.component.ts` that:

- extends `BaseGridComponent<HistoryListModel, PagedListModel<...>, HistoryFilterPagingModel>`
- provides entity id as `@Input()`
- calls `historyPaged(...)` in the `BaseGridComponent` constructor callback
- sets `filterPaging.id` in `setDefaultFilterPaging(...)`
- supports export through `historyExport(...)` and `DownloadHelper.downloadFile(...)`

Example:

- `person-history-grid-table.component.ts`

### 7.5 Shared grid behavior from `BaseGridComponent`

Because history grids inherit `BaseGridComponent`, they automatically get:

- paging/sorting/filter wiring to backend filter paging models
- local storage restore of grid state
- standard filter components (string/date/enum/etc.)
- unified load/reload behavior

This keeps all history screens behaviorally consistent.

### 7.6 Frontend export behavior

History export uses:

- `historyExport(this.getExportParameters(), DateTimeHelper.getTimeZone())`
- `DownloadHelper.downloadFile(...)`

`timeZone` is passed from the browser so exported date values match the user context.

## 8. Forcing a History Entry on Related Changes

When a related entity changes but you still need a history record on the main entity, extension method support exists:

- `SetStateToModifiedWhenUnchanged(...)`

This changes an unchanged tracked entity to `Modified`, which can force update timestamps and temporal history generation when needed.

## 9. How to Add Historization for a New Entity

Use this checklist:

1. In entity configuration, enable temporal mapping:
   - `builder.ToTable(x => x.IsTemporal());`
2. Create and apply migration so EF/SQL builds history table and period columns.
3. Add history list/filter models inheriting:
   - `HistoryModel`
   - `HistoryFilterPagingModel`
4. Add service method `GetHistoryPagedAsync(...)` using the standard temporal query pattern.
5. Add projection for `...HistoryListModel` and include:
   - `UpdateDate`
   - `UpdateUserFullName` (via temporal join if needed)
   - `PeriodStart`
   - `PeriodEnd`
6. Add controller endpoints:
   - `HistoryPaged...`
   - `HistoryExport...` (optional but used broadly in this codebase)
7. Regenerate/update Angular API client and wire UI history flow:
   - add `*-history-dialog` container
   - add `*-history-grid-table` component inheriting `BaseGridComponent`
   - open dialog from list/detail via `onShowHistory(...)`
   - set filter id in `setDefaultFilterPaging(...)`
   - call `historyExport(..., DateTimeHelper.getTimeZone())`

## 10. Notes and Caveats

- Temporal data fidelity depends on using temporal joins in projections, not only on main-entity `.TemporalAll()`.
- `PeriodStart` and `PeriodEnd` are the reliable DB-level validity interval; use them for auditing semantics.
- Export formatting is centralized in `HistoryExportHelper`.
