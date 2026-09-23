---
name: toast-labor-and-analytics
description: Read and write Toast employee, job, shift and time-entry data for a payroll or workforce
  integration, and pull management-group reporting through the analytics API. Use for payroll, HR,
  scheduling, and business-intelligence integrations with Toast.
api: Toast Labor API 1.9.0, Toast Analytics API 1.0.0
generated: '2026-08-27'
method: generated
source: openapi/toast-employees-api-openapi.yml, openapi/toast-shifts-api-openapi.yml,
  openapi/toast-jobs-api-openapi.yml, openapi/toast-time-entries-api-openapi.yml,
  openapi/toast-analytics-openapi.yaml,
  https://doc.toasttab.com/doc/devguide/apiAnalyticsUnderstandingProcess.html,
  https://doc.toasttab.com/doc/devguide/apiUnarchivingAnEmployee.html
operations:
- employeesGet
- employeesPost
- employeesEmployeeIdGet
- employeesEmployeeIdPatch
- employeesEmployeeIdDelete
- employeesEmployeeIdUnarchivePut
- employeesEmployeeIdExternalIdPut
- employeesEmployeeIdJobsPut
- employeesEmployeeIdWageOverridesPut
- shiftsGet
- shiftsPost
- shiftsShiftIdPut
- shiftsShiftIdDelete
- jobsGet
- timeEntriesGet
- postMetricsReportingDataCustomTimeRangeRequest
- getMetricsReportingData
- postLaborReportingDataSpecificTimeRangeRequest
- getLaborReportingData
- getManagementGroupRestaurantsInformation
scopes:
- labor:read
- labor.employees:read
- labor.employees:write
- labor.jobs:write
- labor.shifts:write
---

# Toast labor and analytics

## Two different scopes for one API

The labor API splits its read scope in two, and this is the most common 403 in a payroll integration:

- `labor:read` — everything **except** employees (shifts, jobs, time entries).
- `labor.employees:read` — employee records specifically.

A payroll sync almost always needs both. Writes are split three ways: `labor.employees:write`,
`labor.jobs:write`, `labor.shifts:write`.

## Bind your own identifiers

Toast gives you a first-class place to store your system's key rather than maintaining a side table:

- `PUT /labor/v1/employees/{employeeId}/externalId` (`employeesEmployeeIdExternalIdPut`)
- `PUT /labor/v1/jobs/{jobId}/externalId` (`jobsJobIdExternalIdPut`)

Do this at creation time. Most of the labor operations accept either the Toast GUID or the external
identifier, so binding once removes a lookup from every later call.

## Employee lifecycle — delete is reversible

- Create: `POST /labor/v1/employees` (`employeesPost`).
- Update: `PATCH /labor/v1/employees/{employeeId}` (`employeesEmployeeIdPatch`).
- Assign jobs: `PUT /labor/v1/employees/{employeeId}/jobs` (`employeesEmployeeIdJobsPut`).
- Wage overrides: `PUT /labor/v1/employees/{employeeId}/wageOverrides`
  (`employeesEmployeeIdWageOverridesPut`).
- **Archive:** `DELETE /labor/v1/employees/{employeeId}` (`employeesEmployeeIdDelete`). This archives —
  it does not destroy the record.
- **Restore:** `PUT /labor/v1/employees/{employeeId}/unarchive` (`employeesEmployeeIdUnarchivePut`).
  No stated time limit. Unarchiving an employee who is not archived returns 400.

This makes employee deletion one of only two reversible writes Toast publishes. Use it rather than
building your own soft-delete.

## A dated, breaking change to plan for

From **2026-09-14** the labor API validates employee passcode values on create and update. If your
integration writes employee records with passcodes, validate them on your side before that date or the
writes will start failing.

## Shifts and time entries

`shiftsGet` / `shiftsPost` / `shiftsShiftIdPut` / `shiftsShiftIdDelete` manage scheduled shifts.
`timeEntriesGet` and `timeEntriesTimeEntryIdGet` read worked time; each `TimeEntry` carries a
`breaks` array of `TimeEntryBreak`, which since 2026-03-25 includes a boolean `waived` indicating the
employee waived the break — material for a compliance calculation.

## Analytics: a different shape entirely

The analytics API (`/era/v1`) is **not** another view of the labor graph. It is a denormalised reporting
projection, it operates on a **management group** rather than a single restaurant, and it is
**production only** — there is no sandbox for it, and it needs its own credentials.

Every report follows the same two-step async pattern:

1. **POST** the request — `postLaborReportingDataSpecificTimeRangeRequest`,
   `postMetricsReportingDataCustomTimeRangeRequest`, `postCheckReportingDataSpecificTimeRangeRequest`,
   `postMenuReportSpecificTimeRange`, `postPayoutReportSettledDateSpecificTimeRange`,
   `postGuestReportPaymentDateSpecificTimeRange`. You get back a `reportRequestGuid`.
2. **GET** the result by that GUID — `getLaborReportingData`, `getMetricsReportingData`,
   `getCheckReportingData`, and so on.

Poll the GET with backoff. A **504** on the GET means Toast's internal services took too long; retry the
**GET**, do not resubmit the POST. A **409** means the `reportRequestGuid` can no longer be processed —
request a new one.

`getManagementGroupRestaurantsInformation` (`GET /era/v1/restaurants-information`) lists the locations in
the group, including inactive ones — start there rather than assuming your location list is current.

## Limits

A custom time range for aggregated sales reporting may span at most **366 days** between
`startBusinessDate` and `endBusinessDate` (since 2026-03-06). Longer histories must be split into
multiple requests.
