# CE-RISE Diagnostic Results

[![DOI](https://zenodo.org/badge/DOI/TOBEOBTAINED.svg)](https://doi.org/TOBEOBTAINED) [![Schemas](https://img.shields.io/badge/Generated%20Schema%20Files-JSON%2C%20SHACL%2C%20OWL-32CD32)](https://ce-rise-models.codeberg.page/diagnostic-results/)

The Diagnostic Results data model captures **structured outputs from diagnostic, repair, service, and condition-assessment operations** throughout a product's lifecycle. These are event-bound results that provide point-in-time assessments of product health, performance, and maintenance needs.


---

## Data Model Structure

This model is designed to capture **time-stamped diagnostic events and their results**, complementing the dynamic supply chain events in the Traceability model. Built using [LinkML](https://linkml.io/), it generates multiple schema formats (JSON Schema, SHACL, OWL) for maximum interoperability.

**Core Philosophy**: This model answers critical questions about product condition and maintenance:
- **"What is the current health status?"** → Device self-diagnostics and condition monitoring
- **"What issues were found?"** → Error codes, fault detection, anomaly identification
- **"What was done about it?"** → Service reports, repair actions, calibrations
- **"What might happen next?"** → Predictive maintenance, remaining useful life estimates
- **"Is it performing to spec?"** → Performance metrics, compliance tests, quality assessments

This model focuses exclusively on diagnostic outputs and assessment results. Static product specifications are in the Product Profile model, while the actual maintenance schedules and instructions are in the Usage and Maintenance model.

## Model Boundaries Within CE-RISE Architecture

### What This Model INCLUDES:
- **Service and repair reports** - Technician assessments, repair documentation, service completion records
- **Automated diagnostic outputs** - Self-test results, built-in diagnostics, IoT sensor assessments
- **Performance test results** - Benchmark tests, stress tests, compliance verifications
- **Predictive analytics outputs** - Remaining useful life, failure probability, maintenance predictions
- **Calibration and certification results** - Calibration certificates, accuracy verifications
- **Error and fault records** - Error codes, fault trees, failure mode identifications
- **Condition monitoring snapshots** - Battery health, component wear levels, degradation metrics
- **Quality control test results** - Production tests, acceptance tests, periodic inspections

### What This Model EXCLUDES (handled by other CE-RISE models):
- **Static product specifications** → `product-profile` model (design specs, nominal values)
- **Supply chain events** → `traceability-and-life-cycle-events` model (logistics, ownership)
- **Maintenance schedules and instructions** → `usage-and-maintenance` model (how-to guides, intervals)
- **Environmental impact data** → `integrated-lca` model (carbon footprint, resource use)
- **Compliance certifications** → `compliance-and-standards` model (regulatory approvals)

### Key Design Principles

1. **Event-Bound Results**: Every diagnostic output is tied to a specific timestamp and diagnostic event
2. **Structured Data Capture**: Results follow standardized formats for machine readability
3. **Traceability Linkage**: Each diagnostic event references the product and can link to supply chain events
4. **Multi-Source Support**: Accommodates human technicians, automated systems, and IoT devices
5. **Standards Alignment**: Uses established vocabularies (ISO 13374, MIMOSA, IEC 61508, IEEE standards)
6. **Severity Classification**: Clear categorization of issue severity and urgency
7. **Action Tracking**: Links findings to corrective actions and follow-up requirements
8. **Evidence Management**: Supports attachments, images, sensor data, and measurement records


### Core Hierarchy

```
DiagnosticResults (root)
├── 1. DiagnosticEvent
│   ├── EventIdentifier (UUID)
│   ├── EventTimestamp (ISO 8601)
│   ├── DiagnosticType (service/self-test/predictive/calibration)
│   ├── PerformedBy (technician ID or system ID)
│   ├── ProductReference (link to product-profile)
│   ├── LocationReference (facility/field location)
│   └── EventTrigger (scheduled/failure/request)
├── 2. ServiceReport
│   ├── ReportIdentifier
│   ├── TechnicianIdentifier
│   ├── ServiceType (repair/maintenance/inspection)
│   ├── ServiceActions (list of performed actions)
│   ├── PartsReplaced (component identifiers)
│   ├── ServiceDuration
│   ├── ServiceOutcome (completed/partial/failed)
│   └── NextServiceRecommendation
├── 3. DiagnosticOutput
│   ├── TestIdentifier
│   ├── TestType (functional/performance/safety)
│   ├── TestParameters
│   ├── MeasuredValues
│   ├── ReferenceValues
│   ├── PassFailStatus
│   ├── Deviations
│   └── TestStandard (ISO/IEC reference)
├── 4. ErrorFaultRecord
│   ├── ErrorCode
│   ├── ErrorDescription
│   ├── ErrorSeverity (critical/major/minor/warning)
│   ├── ErrorTimestamp
│   ├── AffectedComponents
│   ├── RootCause
│   ├── CorrectiveAction
│   └── ResolutionStatus
├── 5. ConditionAssessment
│   ├── AssessmentIdentifier
│   ├── ComponentIdentifier
│   ├── HealthScore (0-100%)
│   ├── DegradationIndicators
│   │   ├── WearLevel
│   │   ├── FatigueIndex
│   │   └── PerformanceDegradation
│   ├── BatteryHealth (for electronics)
│   │   ├── StateOfCharge
│   │   ├── StateOfHealth
│   │   ├── CycleCount
│   │   └── Capacity
│   └── EstimatedRemainingLife
├── 6. PredictiveMaintenance
│   ├── PredictionIdentifier
│   ├── PredictionModel
│   ├── FailureProbability
│   ├── TimeToFailure
│   ├── ConfidenceLevel
│   ├── RecommendedActions
│   ├── MaintenanceUrgency
│   └── CostBenefitEstimate
└── 7. CalibrationCertificate
    ├── CertificateIdentifier
    ├── CalibrationDate
    ├── CalibrationStandard
    ├── CalibrationEquipment
    ├── MeasurementPoints
    ├── Uncertainties
    ├── AdjustmentsMade
    ├── CalibrationInterval
    └── AccreditationReference
```

### Workflow Sequence

#### **Step 1: DiagnosticEvent**
Foundation for all diagnostic activities with complete context:
- **EventIdentifier**: Unique UUID for each diagnostic event
- **EventTimestamp**: When the diagnostic occurred (ISO 8601 with timezone)
- **DiagnosticType**: Classification (SERVICE/SELF_TEST/PREDICTIVE/CALIBRATION/INSPECTION)
- **PerformedBy**: Who/what performed it (technician GLN, system ID, IoT device ID)
- **ProductReference**: Link to product-profile identifiers (GTIN + serial)
- **LocationReference**: Where performed (facility GLN, field location, remote)
- **EventTrigger**: What initiated it (SCHEDULED/FAILURE/REQUEST/ALERT)

#### **Step 2: ServiceReport**
Human technician service and repair documentation:
- **ReportIdentifier**: Unique service report number
- **TechnicianIdentifier**: Certified technician ID/license
- **ServiceType**: REPAIR/PREVENTIVE_MAINTENANCE/CORRECTIVE_MAINTENANCE/INSPECTION
- **ServiceActions**: Detailed list of actions performed
- **PartsReplaced**: Component identifiers and quantities
- **ServiceDuration**: Time spent (ISO 8601 duration)
- **ServiceOutcome**: COMPLETED/PARTIAL/FAILED/DEFERRED
- **NextServiceRecommendation**: Follow-up requirements

#### **Step 3: DiagnosticOutput**
Structured test results from automated or manual testing:
- **TestIdentifier**: Unique test ID
- **TestType**: FUNCTIONAL/PERFORMANCE/SAFETY/COMPLIANCE
- **TestParameters**: Input conditions and settings
- **MeasuredValues**: Actual measurements with units
- **ReferenceValues**: Expected/nominal values
- **PassFailStatus**: Clear pass/fail determination
- **Deviations**: Percentage or absolute deviations
- **TestStandard**: Reference to ISO/IEC/IEEE standard

#### **Step 4: ErrorFaultRecord**
Capture and classification of errors and faults:
- **ErrorCode**: Standardized error code (OBD, proprietary)
- **ErrorDescription**: Human-readable description
- **ErrorSeverity**: CRITICAL/MAJOR/MINOR/WARNING
- **ErrorTimestamp**: When error occurred
- **AffectedComponents**: Which parts are impacted
- **RootCause**: Identified or suspected cause
- **CorrectiveAction**: Required or recommended action
- **ResolutionStatus**: OPEN/IN_PROGRESS/RESOLVED/DEFERRED

#### **Step 5: ConditionAssessment**
Current state and health evaluation:
- **HealthScore**: Overall health percentage (0-100%)
- **DegradationIndicators**: Wear, fatigue, performance metrics
- **BatteryHealth**: For electronic products (SoC, SoH, cycles)
- **ComponentStatus**: Individual component assessments
- **EstimatedRemainingLife**: Predicted useful life remaining

#### **Step 6: PredictiveMaintenance**
Analytics-driven maintenance predictions:
- **FailureProbability**: Statistical likelihood of failure
- **TimeToFailure**: Estimated time until failure
- **ConfidenceLevel**: Statistical confidence in prediction
- **RecommendedActions**: Preventive measures
- **MaintenanceUrgency**: IMMEDIATE/HIGH/MEDIUM/LOW
- **CostBenefitEstimate**: Economic impact analysis

#### **Step 7: CalibrationCertificate**
Calibration and accuracy verification:
- **CalibrationDate**: When calibrated
- **CalibrationStandard**: Reference standard used
- **MeasurementPoints**: Tested points and results
- **Uncertainties**: Measurement uncertainties
- **AdjustmentsMade**: Corrections applied
- **CalibrationInterval**: Next calibration due
- **AccreditationReference**: Lab accreditation details

### Data Properties

Each class has a corresponding value property (e.g., `event_id_value`, `health_score_value`) that holds the actual data. All value properties are string type except where specified otherwise (integers for counts, floats for measurements, datetime for timestamps).

#### SQL Identifiers

Every data point in the model includes a `sql_identifier` annotation that serves as a unique, machine-friendly database identifier. These identifiers follow a structured namespace pattern to ensure uniqueness across the entire data model:

**Pattern**: `diag_[category]_[specific_name]`

**Features:**
- **Diagnostic Prefix**: All identifiers start with `diag_` to clearly identify them as belonging to the Diagnostic Results data model
- **Hierarchical Namespacing**: Uses category prefixes (`event_`, `service_`, `test_`, `error_`, `condition_`, `predict_`, `calib_`) to provide context and prevent naming conflicts
- **Database-Friendly**: Uses underscores and avoids special characters for SQL compatibility
- **Unique Across Model**: No duplicate identifiers, even when similar concepts appear in different parts of the hierarchy
- **Reasonable Length**: Abbreviated but meaningful names that balance clarity with practical database usage

**Examples:**
- `diag_event_id` - Event identifier in DiagnosticEvent
- `diag_service_technician` - Technician ID in ServiceReport
- `diag_test_result` - Test result in DiagnosticOutput
- `diag_error_code` - Error code in ErrorFaultRecord
- `diag_condition_health_score` - Health score in ConditionAssessment
- `diag_predict_failure_prob` - Failure probability in PredictiveMaintenance
- `diag_calib_certificate_id` - Certificate ID in CalibrationCertificate

This identifier system enables seamless integration with databases and ensures clear data model composition when combining with other CE-RISE data models.

---

## Development Roadmap

| Step | Component | Criticalities Identified | Solutions Implemented | Status | Missing/TODO |
|------|-----------|-------------------------|----------------------|--------|--------------|
| **1** | **DiagnosticEvent** | • Need for event tracking and context<br>• Link to product identity<br>• Trigger classification<br>• Performer identification | • UUID-based event IDs<br>• ISO 8601 timestamps<br>• Product reference system<br>• Trigger enumeration<br>• Multi-source performer IDs | **TODO** | • Event correlation<br>• Blockchain anchoring |
| **2** | **ServiceReport** | • Technician documentation<br>• Service action tracking<br>• Parts replacement records<br>• Outcome classification | • Structured service types<br>• Action list format<br>• Component tracking<br>• Outcome enumeration | **TODO** | • Digital signatures<br>• Photo attachments |
| **3** | **DiagnosticOutput** | • Test result structure<br>• Pass/fail determination<br>• Standards reference<br>• Measurement units | • Test type classification<br>• Value/reference pairs<br>• Standards alignment<br>• Unit ontology | **TODO** | • Uncertainty calculation<br>• Statistical analysis |
| **4** | **ErrorFaultRecord** | • Error classification<br>• Severity assessment<br>• Root cause tracking<br>• Resolution workflow | • Error code systems<br>• Severity levels<br>• Component mapping<br>• Status tracking | **TODO** | • Fault tree analysis<br>• FMEA integration |
| **5** | **ConditionAssessment** | • Health scoring<br>• Degradation metrics<br>• Battery specifics<br>• Life estimation | • 0-100% health scale<br>• Multi-indicator system<br>• Battery standards<br>• RUL algorithms | **TODO** | • ML model integration<br>• Trend analysis |
| **6** | **PredictiveMaintenance** | • Failure prediction<br>• Confidence levels<br>• Action recommendations<br>• Cost-benefit analysis | • Probability models<br>• Urgency classification<br>• Action templates<br>• Economic models | **TODO** | • AI/ML pipelines<br>• Real-time updates |
| **7** | **CalibrationCertificate** | • Calibration tracking<br>• Standards compliance<br>• Uncertainty reporting<br>• Interval management | • Certificate structure<br>• ISO 17025 alignment<br>• Uncertainty format<br>• Schedule integration | **TODO** | • Digital certificates<br>• Auto-scheduling |

### Integration Opportunities

**Within CE-RISE Architecture:**
- **Product Profile Integration**: References product identifiers, specifications, and nominal values
- **Traceability Events Linkage**: Diagnostic events can trigger supply chain events (recalls, returns)
- **Usage and Maintenance Sync**: Results inform maintenance schedules and update usage patterns
- **Compliance Updates**: Test results feed into compliance status and certification renewals
- **LCA Impact**: Component replacements and failures inform environmental impact calculations

**External System Integration:**
- **CMMS/EAM Systems**: Computerized Maintenance Management System integration
- **IoT Platforms**: Real-time diagnostic data ingestion from connected devices
- **MIMOSA Standards**: OSA-CBM (Condition-Based Maintenance) and OSA-EAI alignment
- **Industry Standards**: ISO 13374 (Condition Monitoring), IEC 61508 (Functional Safety)
- **OBD/Diagnostic Protocols**: Automotive (OBD-II), Industrial (OPC UA), Building (BACnet)
- **Predictive Analytics**: Integration with Azure ML, AWS SageMaker, Google AutoML
- **Service Management**: Field service platforms (ServiceNow, Salesforce Field Service)



---

## Publishing

Release artifacts for each version (`schema.json`, `shacl.ttl`, `model.owl`)  
are served directly from this URL:
```
https://ce-rise-models.codeberg.page/diagnostic-results/
```


---

## Accessing Previous Releases

If you want to view the files published for version `v1.2.0`, open:

```
https://codeberg.org/CE-RISE-models/diagnostic-results/src/tag/pages-v1.2.0/generated/
```

Files available in that directory typically include:

- schema.json
- shacl.ttl
- model.ttl
- index.html


---
<a href="https://europa.eu" target="_blank" rel="noopener noreferrer">
  <img src="https://ce-rise.eu/wp-content/uploads/2023/01/EN-Funded-by-the-EU-PANTONE-e1663585234561-1-1.png" alt="EU emblem" width="200"/>
</a>

Funded by the European Union under Grant Agreement No. 101092281 — CE-RISE.  
Views and opinions expressed are those of the author(s) only and do not necessarily reflect those of the European Union or the granting authority (HADEA).  
Neither the European Union nor the granting authority can be held responsible for them.

© 2025 CE-RISE consortium.  
Licensed under [Creative Commons Attribution–NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/).  
Attribution: CE-RISE project (Grant Agreement No. 101092281) and the individual authors/partners as indicated.

<a href="https://www.nilu.com" target="_blank" rel="noopener noreferrer">
  <img src="https://nilu.no/wp-content/uploads/2023/12/nilu-logo-seagreen-rgb-300px.png" alt="NILU logo" width="40"/>
</a>

Developed by NILU (Riccardo Boero — ribo@nilu.no) within the CE-RISE project.
