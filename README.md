# Programme Budget Optimiser — V0.9

A browser-based application for planning programme budgets, allocating resources across projects, exploring alternative allocations, and reporting planned costs.

## Quick start

1. Download `Programme_Budget_Optimiser_V0.9.html` and keep it in a folder on your computer.
2. Open the HTML file in a current version of Chrome or Edge.
3. On **Portfolio**, review the example programme and overall budget position.
4. Select a programme and open **Setup** to configure its budget, dates, projects, priorities, and demand.
5. Open **Resources** to enter resource names, cost rates, capacity, and project dedication (or shared programme availability).
6. Open **Plan** and choose **Optimise selected** to generate an allocation. Review coverage, planned cost, and utilisation before making decisions.
7. Use **Download Excel** for an Excel report, and **Save to computer** to download a JSON backup of your plans.

> **Important:** This is a standalone, local-first HTML prototype. It is not a multi-user server application or a substitute for enterprise-grade database backup and access controls.

## Main areas

| Area | What it does |
| --- | --- |
| Portfolio | Summarises programmes, budgets, planned costs, and demand gaps; includes executive visualisations. |
| Setup | Defines programme settings, projects, priorities, budgets, planning months, and demand. |
| Resources | Manages available people/resources, monthly costs, capacities, and shared or dedicated assignments. |
| Plan | Generates and reviews resource allocations, lets users explore alternatives, edit allocation cells, and lock projects or months. |

The interface includes a collapsible left navigation and selectable colour palettes.

## Planning workflow

1. **Set up a programme.** Enter its overall budget, first month, number of months, and effort/rate unit.
2. **Add projects.** Enter project budgets, monthly demand, and priorities (higher values indicate higher priority).
3. **Add resources.** Enter cost and available capacity. Assign a resource to a specific project if it should not be shared across the programme.
4. **Optimise.** Select the months and projects to recalculate, then run optimisation.
5. **Review.** Check budget consumption, resource utilisation, uncovered demand, and monthly allocation details.
6. **Refine.** Try another allocation, lock a project or month, or edit unlocked allocation cells. Recheck the results after any changes.
7. **Export and back up.** Download an Excel report and a JSON backup.

### What “optimise” means here

V0.9 generates multiple candidate allocations using cost and project-ordering heuristics and ranks them using weighted uncovered demand and cost. **It does not guarantee a globally optimal mathematical solution.** Always review capacity, budgets, and uncovered demand before approving a plan. Manual edits can also introduce conflicts, so check utilisation warnings.

## Saving and restoring data

- The application uses browser-local persistence (including IndexedDB where supported, with browser-storage fallback). Data is tied to the browser/profile and can be lost if site data is cleared or storage is restricted.
- **Save to computer** downloads a JSON backup file. Keep backups in a secure, known folder and make a new backup after important changes.
- **Open saved file** imports a previously saved JSON backup. Importing replaces the currently open set of programmes after confirmation: back up your current work first.
- Saving does **not** write directly into the HTML file or create a shared company database.
- For heavy daily use, a future local SQLite-backed or managed-server version is recommended, with named workspaces, audit history, and regular backups.

## Excel export

Click **Download Excel** to create `programme-cost-plan.xlsx`. The workbook includes:

- **Portfolio:** programme budgets, allocated budgets, planned costs, utilisation of budget, and uncovered demand.
- **Projects:** project budgets, priorities, costs, remaining budget, average effort, and lock status.
- **Allocation:** resource assignments by programme, month, and project, with effort and cost.
- **Resources:** resource costs, capacity, and project dedication.

**Internet requirement:** V0.9 loads the SheetJS/XLSX library from a CDN. The Excel export may not work without internet access or when a corporate firewall blocks that script. If the download fails, check the browser console and network access. A fully offline package should bundle the library locally.

## Important limitations

- **Single-user/browser-local:** no central collaboration, role-based access, or automatic cross-device synchronisation is guaranteed.
- **Planning units:** review whether rates and effort are entered per month (FTE) or per day; the selected unit affects the calculations.
- **Cross-programme duplication:** a person listed in more than one programme can be counted more than once; the app warns about matching names but does not enforce a global resource capacity constraint.
- **Optimisation:** uses heuristics rather than a formal constraint solver; outputs require business review.
- **Data sensitivity:** avoid entering confidential personal or commercial data on an unmanaged/shared device. Browser storage is not a secured enterprise database.
- **Testing:** this version has not been certified through comprehensive browser, security, or business acceptance testing.

## Troubleshooting

**Excel download does nothing:** Use Chrome or Edge, allow downloads, confirm internet access to the XLSX CDN, and look for errors in the browser developer console (F12).

**Changes disappeared:** Make sure you opened the application in the same browser profile and did not clear browser data. Restore your most recent JSON backup using **Open saved file**.

**Plan looks outdated:** Changes to budgets, demand, or resource inputs can make an existing plan stale. Re-run optimisation and review the results.

**Resource is over capacity:** Check manual allocations, locked projects/months, and whether the same resource was entered in multiple programmes.

## Suggested next release

For a production-oriented V1, prioritise local SQLite workspaces, named and versioned scenarios, validated allocation constraints, a fully offline Excel library, and explicit save/recovery status.
