# A5 — Design Pattern Identification in a Laravel-Based Healthcare Management Application

**Course:** 23CSE455 — Design Patterns  
**Case study:** Healthcare Application using Laravel  
**Team:** A5  
**Study date:** 10 October 2026

## Team members

| Roll number | Name | Batch |
|---|---|---|
| AM.AL.U4AID23014 | Nemali Ashrith Reddy | 
| AM.AL.U4AID23062 | Akshay Reddy Velugati | 
| AM.SC.U4CSE23212 | B. Pravallika | 
| AM.SC.U4CSE23022 | Daripineni Manogna | 

## 1. Application and baseline

The case study examines [esteham/hospital-management](https://github.com/esteham/hospital-management), a Laravel-based healthcare management application, at baseline commit:

`1e7420e431771e3f5eec470d8a005e8255fa5fe8`

The inspected application uses PHP/Laravel, Eloquent ORM, MySQL, Vue 3 and Inertia. The archived source excerpts and `composer.json` are under `data/code/`. **This repository does not include a complete, runnable checkout of the upstream Laravel application.** Consequently, the application itself cannot be launched or regression-tested solely from this A5 folder. See the upstream repository for full setup instructions and dependencies.

The inspected scope includes patient and doctor models, appointments, diagnostic bookings, prescription/PDF/mail workflows, and payment-status fields. The scope is limited to source excerpts included under `data/code/`; absence of a pattern in those excerpts does not prove its absence from the entire upstream project. The upstream license and full dependency versions should be confirmed from the pinned commit before final submission.

## 2. Part 1 — Pattern identification

Part 1 documents architecture, participant mappings, and source-based pattern candidates. The submitted baseline inventory records **Active Record** and Laravel **Facade** collaborations. Adapter, Proxy, Strategy, Repository and Observer were not confirmed in the inspected baseline excerpts; a payment-method string alone does not constitute Strategy.

- Inventory: `Part1/patterns.csv`
- Counts: `Part1/Pattern_count.csv`
- Architecture diagram and source: `Part1/pattern_architecture/`
- LLM documentation: `Part1/llm.csv` and `Part1/llm/verification.md`

Pattern roles and source line references should be checked against the exact baseline commit before claiming full source verification.

## 3. Part 2 — Proposed evolution and standalone demonstrations

The case study considers three changes:

| ID | Change | Proposed approach | Supporting files |
|---|---|---|---|
| CH01 | External laboratory integration | Laboratory integration interface and service; isolate provider-specific communication | `Part2/code/LaboratoryIntegrationService.php`, `Part2/changes/Change1/` |
| CH02 | New billing provider | Strategy interface with interchangeable payment providers | `Part2/code/BillingService.php`, `Part2/changes/Change2/` |
| CH03 | New patient-data service | EHR provider interface and FHIR-style adapter | `Part2/code/PatientDataService.php`, `Part2/changes/Change3/` |

Evolution records are in `Part2/patterns_evolution.csv`; UML and evolved architecture diagrams are in `Part2/diagrams/`.

**Implementation boundary:** The PHP components in `Part2/code/` are standalone examples, **not integrations wired into the original Laravel controllers, routes, migrations or database**. The `diff.txt` files describe changes; they are not Git-generated source diffs. Tests exercise mock-based contracts rather than real vendor endpoints or end-to-end Laravel behavior.

From the `A5/` directory, run:

```bash
php Part2/tests/integration_contract_test.php
```

A recorded execution result is stored in `data/test_result/part2_standalone_php.txt`. Running this test requires a compatible local PHP CLI; it does not require the full Laravel application.

## 4. Part 3 — Cross-language implementations

Two patterns were selected for equivalent demonstrations across **Java, Python, JavaScript and C++**:

- **Adapter:** normalize an example patient-data/FHIR response to a consistent patient representation.
- **Strategy:** choose between example Stripe and PayPal payment strategies using the same payment interface.

Run commands from each language's own directory:

| Pattern | Language | Command |
|---|---|---|
| Adapter | Java | `javac AdapterDemo.java && java AdapterDemo` |
| Adapter | Python | `python3 adapter_demo.py` |
| Adapter | JavaScript | `node adapterDemo.js` |
| Adapter | C++ | `g++ -std=c++17 adapter_demo.cpp -o adapter_demo && ./adapter_demo` |
| Strategy | Java | `javac StrategyDemo.java && java StrategyDemo` |
| Strategy | Python | `python3 strategy_demo.py` |
| Strategy | JavaScript | `node strategyDemo.js` |
| Strategy | C++ | `g++ -std=c++17 strategy_demo.cpp -o strategy_demo && ./strategy_demo` |

Source directories are `Part3/adapter/{java,python,javascript,cpp}/` and `Part3/strategy/{java,python,javascript,cpp}/`. See their language-specific READMEs for additional details. Recorded output and timing evidence is under `data/test_result/`.

**Measurement rule:** For the corrected archive's recorded process timings, compilation was excluded; one warmup preceded five measured executions, and the median of the five elapsed process times was recorded. Timings include process startup and output, and are machine-dependent. The raw results are stored in the dated JSON files. **Maximum function cyclomatic complexity has not been measured**, and process-exit checks are not a comprehensive unit-test suite. Do not substitute estimated complexity values.

## 5. Datasets, report and LLM evidence

The consolidated dataset directory contains:

| File | Purpose |
|---|---|
| `data/patterns.csv` | Baseline pattern instances and mapped participants |
| `data/pattern_counts.csv` | Pattern counts and summaries |
| `data/cross_language.csv` | Language implementations, commands, results and available measurements |
| `data/llm.csv` | LLM-use records and verification references |

Part-specific CSVs and supporting evidence remain under `Part1/`, `Part2/` and `Part3/`. Paths in dataset cells are intended to be relative to the `A5/` folder. Prompts, outputs, and verification claims must be backed by actual saved evidence; copied LLM records have not been independently authenticated.

The final report artifacts are `A5_Report.tex` and `A5_Report.pdf`. **These report files were preserved from the original archive and have not been synchronized with the corrected CSVs and standalone examples.** Reconcile and recompile them before submission.

## 6. Repository layout

```text
A5/
├── README.md
├── A5_Report.tex
├── A5_Report.pdf
├── CORRECTIONS_AND_LIMITATIONS.md
├── data/
│   ├── code/                    # Inspected application source excerpts
│   ├── test_result/             # Recorded output and timing evidence
│   ├── patterns.csv
│   ├── pattern_counts.csv
│   ├── cross_language.csv
│   └── llm.csv
├── Part1/
│   ├── patterns.csv
│   ├── Pattern_count.csv
│   ├── pattern_architecture/
│   └── llm/
├── Part2/
│   ├── code/                    # Standalone PHP examples
│   ├── tests/
│   ├── changes/Change1/
│   ├── changes/Change2/
│   ├── changes/Change3/
│   ├── diagrams/
│   └── patterns_evolution.csv
└── Part3/
    ├── adapter/                 # Java, Python, JavaScript, C++
    └── strategy/                # Java, Python, JavaScript, C++
```

## 7. Contributions

| Member | Recorded contribution |
|---|---|
| Nemali Ashrith Reddy | Part 1: inspected modules, baseline pattern inventory, architecture |
| Akshay Reddy Velugati | Part 2: integration scenarios, proposed refactorings and UML |
| B. Pravallika | Part 3: Adapter demonstrations in four languages |
| Daripineni Manogna | Part 3: Strategy demonstrations in four languages |

Contributions are transcribed from the existing A5 README and should be confirmed by the team.

## 8. Limitations and reproducibility

1. Full upstream Laravel integration and regression testing have **not** been demonstrated.
2. No live external laboratory, billing, or EHR vendor calls have been verified.
3. Source-line mappings and pattern classifications require a final review against the pinned upstream commit.
4. Cyclomatic complexity remains unmeasured; runtime/compiler versions and all test assertions should be checked against recorded logs.
5. The report PDF/LaTeX must be updated to reflect corrected datasets and actual implementation scope.
6. Confirm official student batch labels, source license, and local environment versions before submission.

See `CORRECTIONS_AND_LIMITATIONS.md` for the change log and outstanding work. No unsupported implementation, test or measurement claim should be presented as verified.

## References

- [Original healthcare application](https://github.com/esteham/hospital-management)
- [Team case-study repository](https://github.com/Rashrith7/23CSE455_DP_CaseStudy)
- 23CSE455 Design Patterns Case Study Instructions (provided assignment PDF)
- 23CSE455 Design Patterns Case Study Report Template (provided template PDF)
