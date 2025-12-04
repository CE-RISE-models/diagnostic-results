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
- **Component inventory documentation** - Discovery of any product components, serial tracking, configuration
- **Data sanitization records** - Secure erasure certificates for any data-bearing components
- **Quality grading assessments** - Condition grades, functional assessments, market categorization

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
│   ├── DiagnosticType (service/self-test/predictive/calibration/inspection)
│   ├── PerformedBy (technician ID or system ID)
│   ├── ProductReference (link to product-profile)
│   ├── LocationReference (facility/field location)
│   ├── EventTrigger (scheduled/failure/request/periodic)
│   ├── UnitIdentifier (internal tracking ID)
│   ├── BatchIdentifier (batch/lot reference)
│   ├── AssetReference (asset management ID)
│   ├── DiagnosticSoftware
│   │   ├── ToolName
│   │   ├── ToolVersion
│   │   ├── ToolVendor
│   │   ├── ToolCertification
│   │   └── ToolConfiguration
│   ├── EnvironmentalConditions
│   │   ├── AmbientTemperature
│   │   ├── Humidity
│   │   ├── Pressure
│   │   ├── TestEnvironment (lab/field/factory/customer)
│   │   └── OtherConditions
│   ├── SessionMetadata
│   │   ├── SessionDuration
│   │   ├── TestSequence
│   │   ├── TestsCompleted
│   │   ├── TestsAborted
│   │   └── AbortReasons
│   └── QualityMetadata
│       ├── DataCompleteness
│       ├── ResultConfidence (high/medium/low)
│       └── AnomaliesDetected
├── 2. ComponentInventory
│   ├── ComponentIdentifier
│   ├── ComponentType (generic classification)
│   ├── ComponentCategory
│   ├── Manufacturer
│   ├── Model
│   ├── PartNumber
│   ├── SerialNumber
│   ├── Version/Revision
│   ├── ComponentSpecifications (key-value pairs)
│   ├── SubComponents (nested components)
│   │   ├── SubComponentID
│   │   ├── SubComponentType
│   │   ├── SubComponentModel
│   │   ├── SubComponentSerial
│   │   └── SubComponentSpecs
│   └── ComponentHierarchy (parent-child relationships)
├── 3. ComponentTestResults
│   ├── TestIdentifier
│   ├── TestTimestamp
│   ├── ComponentReference (links to ComponentInventory)
│   ├── TestType (functional/performance/safety/compliance)
│   ├── TestName
│   ├── TestResult (pass/fail/warning/not-tested/inconclusive)
│   ├── MeasuredValues (with units)
│   ├── ReferenceValues
│   ├── TestStandard (if applicable)
│   ├── TestProtocolReference
│   ├── ComplianceStandard (ISO/IEC/ASTM/proprietary)
│   ├── TestParameters
│   ├── Deviations
│   ├── ObservationCodes
│   ├── ObservationNotes
│   ├── TestComparison
│   │   ├── ReferenceBaseline
│   │   ├── PeerComparison
│   │   └── SpecificationCompliance
│   ├── TestQuality
│   │   ├── RetestRequired
│   │   ├── InconclusiveReason
│   │   └── DiagnosticErrors
│   └── CalibrationTraceability
│       ├── TestEquipmentID
│       ├── LastCalibrationDate
│       └── CalibrationCertificate
├── 4. ConditionMetrics
│   ├── MetricIdentifier
│   ├── ComponentReference
│   ├── MetricType (health/wear/performance/capacity)
│   ├── MetricName
│   ├── CurrentValue
│   ├── NominalValue
│   ├── Unit
│   ├── HealthScore (0-100%)
│   ├── DegradationIndicators
│   │   ├── WearLevel
│   │   ├── UsageCycles
│   │   ├── OperatingHours
│   │   └── PerformanceDegradation
│   └── EstimatedRemainingLife
├── 5. DataSanitization
│   ├── SanitizationIdentifier
│   ├── DataBearingComponents (list)
│   │   ├── ComponentReference
│   │   ├── ComponentType
│   │   ├── DataCapacity
│   │   ├── SanitizationMethod
│   │   ├── SanitizationStandard
│   │   ├── SanitizationResult (success/failed/partial)
│   │   ├── VerificationMethod
│   │   ├── SanitizationTimestamp
│   │   ├── PerformedBy
│   │   └── CertificateReference
│   └── ComplianceCertification
├── 6. QualityAssessment
│   ├── QualityGrade
│   ├── GradingScale
│   ├── CosmeticCondition
│   ├── FunctionalCondition
│   ├── PerformanceScore
│   ├── AssessmentCriteria
│   └── QualityCheckResults
├── 7. ServiceActions
│   ├── ActionIdentifier
│   ├── ActionType (repair/replace/adjust/clean/update)
│   ├── ActionDescription
│   ├── ComponentsAffected
│   ├── PartsReplaced
│   │   ├── OldPartNumber
│   │   ├── NewPartNumber
│   │   └── Quantity
│   ├── ActionOutcome
│   ├── TimeSpent
│   └── TechnicianNotes
└── 8. PredictiveAnalytics
    ├── PredictionIdentifier
    ├── PredictionModel
    ├── ComponentReference
    ├── FailureProbability
    ├── TimeToFailure
    ├── ConfidenceLevel
    ├── RecommendedActions
    ├── MaintenanceUrgency
    └── CostBenefitAnalysis
```

### Workflow Sequence

#### **Step 1: DiagnosticEvent**
Foundation for all diagnostic activities with complete context:
- **EventIdentifier**: Unique UUID for each diagnostic event
- **EventTimestamp**: When the diagnostic occurred (ISO 8601 with timezone)
- **DiagnosticType**: Classification (SERVICE/SELF_TEST/PREDICTIVE/CALIBRATION/INSPECTION)
- **PerformedBy**: Who/what performed it (technician ID, system ID, diagnostic software)
- **ProductReference**: Link to product-profile identifiers
- **LocationReference**: Where performed (facility GLN, service center, field location)
- **EventTrigger**: What initiated it (SCHEDULED/FAILURE/REQUEST/QUALITY_CHECK/INTAKE)
- **UnitIdentifier**: Internal tracking ID for the specific unit
- **BatchIdentifier**: Batch or lot reference for grouped processing
- **AssetReference**: Asset management tag for enterprise tracking
- **DiagnosticSoftware**: Critical software/tool information
  - ToolName, ToolVersion, ToolVendor for reproducibility
  - ToolCertification status if validated/certified
  - ToolConfiguration settings used
- **EnvironmentalConditions**: Test environment parameters
  - Temperature, humidity, pressure during testing
  - Test environment type (lab/field/factory/customer-site)
- **SessionMetadata**: Diagnostic session tracking
  - Total session duration, test sequence order
  - Tests completed vs aborted with reasons
- **QualityMetadata**: Result quality indicators
  - Data completeness percentage
  - Result confidence level (high/medium/low)
  - Anomalies detected during diagnostic

#### **Step 2: ComponentInventory**
Generic component discovery and documentation (hardware or software):
- **ComponentIdentifier**: Unique identifier for the component
- **ComponentType**: Generic classification (processor/memory/storage/sensor/actuator/module/assembly)
- **ComponentCategory**: Higher-level categorization
- **Manufacturer**: Component manufacturer name
- **Model**: Specific model designation
- **PartNumber**: Manufacturer part number
- **SerialNumber**: Component serial number
- **Version/Revision**: Firmware or hardware revision
- **ComponentSpecifications**: Flexible key-value pairs for any specifications
- **SubComponents**: Nested components with full tracking
- **ComponentHierarchy**: Parent-child relationships between components

#### **Step 3: ComponentTestResults**
Generic component testing outcomes for any component type:
- **TestIdentifier**: Unique test batch ID
- **ComponentReference**: Links to specific component being tested
- **TestType**: FUNCTIONAL/PERFORMANCE/SAFETY/COMPLIANCE
- **TestName**: Specific test performed
- **TestResult**: PASS/FAIL/WARNING/NOT_TESTED/INCONCLUSIVE
- **MeasuredValues**: Actual measurements with units
- **ReferenceValues**: Expected/nominal values
- **TestStandard**: Reference standard (ISO/IEC/ASTM)
- **TestProtocolReference**: Which test protocol was followed
- **ComplianceStandard**: Applicable compliance requirements
- **TestComparison**: Baseline, peer, and specification compliance
- **TestQuality**: Retest requirements, inconclusive reasons, diagnostic errors
- **CalibrationTraceability**: Test equipment calibration status
- **ObservationCodes**: Standardized defect or issue codes
- **ObservationNotes**: Technician notes on observed issues

#### **Step 4: ConditionMetrics**
Generic condition and health assessment for any component:
- **MetricIdentifier**: Unique metric ID
- **ComponentReference**: Which component is being measured
- **MetricType**: HEALTH/WEAR/PERFORMANCE/CAPACITY
- **MetricName**: Specific metric (e.g., "battery_capacity", "bearing_vibration")
- **CurrentValue**: Current measured value
- **NominalValue**: Expected/design value
- **Unit**: Measurement unit
- **HealthScore**: Overall health percentage (0-100%)
- **DegradationIndicators**: Wear level, usage cycles, operating hours
- **EstimatedRemainingLife**: Predicted useful life remaining

#### **Step 5: DataSanitization**
Secure data erasure for any data-bearing component:
- **SanitizationIdentifier**: Unique sanitization event ID
- **DataBearingComponents**: List of any components containing data
  - ComponentReference linking to ComponentInventory
  - ComponentType (storage/memory/cache/firmware)
  - DataCapacity of the component
  - **SanitizationMethod**: Method appropriate to component type
  - **SanitizationStandard**: NIST 800-88, DoD 5220.22-M, etc.
  - **SanitizationResult**: SUCCESS/FAILED/PARTIAL/SKIPPED
  - **VerificationMethod**: How sanitization was verified
  - **SanitizationTimestamp**: When completed
  - **PerformedBy**: Technician or system
  - **CertificateReference**: Audit trail certificate
- **ComplianceCertification**: Reference to formal compliance certificate

#### **Step 6: QualityAssessment**
Quality assessment for any product:
- **QualityGrade**: Overall grade using defined scale
- **GradingScale**: Scale being used (A-F, 1-10, custom)
- **CosmeticCondition**: Physical appearance assessment
- **FunctionalCondition**: Operational capability assessment
- **PerformanceScore**: Benchmark or performance metrics
- **RefurbishmentActions**: List of refurbishment activities performed
- **QualityCheckResults**: Final quality control outcomes

#### **Step 7: ServiceActions**
Service and repair actions performed:
- **ActionIdentifier**: Unique action ID
- **ActionType**: REPAIR/REPLACE/ADJUST/CLEAN/UPDATE/CALIBRATE
- **ActionDescription**: What was done
- **ComponentsAffected**: Which components were serviced
- **PartsReplaced**: Old and new part numbers with quantities
- **ActionOutcome**: SUCCESS/PARTIAL/FAILED
- **TimeSpent**: Duration of the action
- **TechnicianNotes**: Service notes and observations

#### **Step 8: PredictiveAnalytics**
Predictive maintenance and failure analysis:
- **PredictionIdentifier**: Unique prediction ID
- **PredictionModel**: Model/algorithm used
- **ComponentReference**: Component being analyzed
- **FailureProbability**: Likelihood of failure (0-100%)
- **TimeToFailure**: Estimated time until failure
- **ConfidenceLevel**: Statistical confidence in prediction
- **RecommendedActions**: Preventive measures suggested
- **MaintenanceUrgency**: IMMEDIATE/HIGH/MEDIUM/LOW
- **CostBenefitAnalysis**: Economic impact assessment

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
| **1** | **DiagnosticEvent** | • Need for event tracking and context<br>• Diagnostic software tracking<br>• Environmental conditions<br>• Session quality metadata<br>• Multi-identifier tracking | • UUID-based event IDs<br>• DiagnosticSoftware with version/vendor/certification<br>• Environmental conditions capture<br>• Session metadata tracking<br>• Quality/confidence indicators<br>• Data completeness metrics | **TODO** | • Event correlation<br>• Software validation APIs |
| **2** | **ComponentInventory** | • Generic component model<br>• Hierarchical relationships<br>• Product-agnostic design<br>• Flexible specifications | • Generic component classification<br>• Nested sub-components support<br>• Key-value specifications<br>• Component hierarchy tracking<br>• Version/revision management | **TODO** | • Component database<br>• Auto-discovery APIs |
| **3** | **ComponentTestResults** | • Test standards traceability<br>• Calibration tracking<br>• Result confidence<br>• Comparison baselines | • Test protocol references<br>• Compliance standards<br>• Calibration traceability<br>• Baseline comparisons<br>• Test quality indicators<br>• Inconclusive result handling | **TODO** | • Test automation<br>• Standards library |
| **4** | **ConditionMetrics** | • Generic metrics framework<br>• Health scoring<br>• Degradation tracking<br>• Life estimation | • Flexible metric types<br>• Unit-agnostic values<br>• Health percentage scale<br>• Degradation indicators<br>• Remaining life estimation | **TODO** | • Predictive models<br>• Trend analysis |
| **5** | **DataSanitization** | • Any data-bearing component<br>• Method verification<br>• Standards compliance<br>• Audit trails | • Generic component support<br>• Method-appropriate techniques<br>• Verification tracking<br>• Certificate generation<br>• Compliance documentation | **TODO** | • Automated verification<br>• Blockchain certificates |
| **6** | **QualityAssessment** | • Flexible grading scales<br>• Assessment criteria<br>• Quality checks<br>• Performance scoring | • Custom scale support<br>• Criteria documentation<br>• Cosmetic/functional split<br>• Performance metrics<br>• Quality check results | **TODO** | • ML-based assessment<br>• Criteria automation |
| **7** | **ServiceActions** | • Service tracking<br>• Parts replacement<br>• Action outcomes<br>• Time documentation | • Action type classification<br>• Component linkage<br>• Parts tracking<br>• Outcome recording<br>• Time spent tracking | **TODO** | • Service automation<br>• Parts inventory |
| **8** | **PredictiveAnalytics** | • Failure prediction<br>• Confidence levels<br>• Cost-benefit analysis<br>• Urgency classification | • Prediction models<br>• Probability calculations<br>• Time-to-failure estimates<br>• Action recommendations<br>• Economic analysis | **TODO** | • AI/ML integration<br>• Real-time updates |

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
