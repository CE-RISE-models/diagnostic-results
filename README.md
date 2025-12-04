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
│   └── AssetReference (asset management ID)
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
│   ├── TestResult (pass/fail/warning/not-tested)
│   ├── MeasuredValues (with units)
│   ├── ReferenceValues
│   ├── TestStandard (if applicable)
│   ├── TestParameters
│   ├── Deviations
│   ├── ObservationCodes
│   └── ObservationNotes
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
- **LocationReference**: Where performed (facility GLN, servicefurbishment center, field location)
- **EventTrigger**: What initiated it (SCHEDULED/FAILURE/REQUEST/QUALITY_CHECK/INTAKE)
- **UnitIdentifier**: Internal tracking ID for the specific unit
- **LotIdentifier**: Batch or lot reference for grouped processing
- **AssetTag**: Asset management tag for enterprise tracking

#### **Step 2: HardwareInventory**
Complete hardware configuration discovery and documentation:
- **ProductType**: Device category (LAPTOP/DESKTOP/TABLET/PHONE/SERVER)
- **Manufacturer**: OEM manufacturer name
- **Model**: Specific model designation
- **SerialNumber**: Manufacturer serial number
- **ProcessorDetails**: CPU model, speed, generation, socket type
- **MemoryConfiguration**: Total RAM and individual DIMM/SODIMM details (model, serial, type, size)
- **StorageDevices**: Up to 4 storage devices with type, size, model, serial
- **DisplaySpecifications**: Screen size and resolution
- **MotherboardInfo**: Board manufacturer, model, serial, BIOS/UEFI version

#### **Step 3: ComponentTestResults**
Individual component functional testing outcomes:
- **TestIdentifier**: Unique test batch ID
- **ComponentTests**: Pass/Fail/Not-Tested status for each component:
  - CMOS, Speaker, USB Ports, LAN Port, Optical Drive
  - Display/LCD, Keyboard, Touchpad, WiFi adapter
  - Webcam (primary and secondary), Touchscreen, Microphone
  - Storage devices (individual test results)
- **ObservationCodes**: Standardized defect or issue codes
- **ObservationNotes**: Technician notes on observed issues

#### **Step 4: BatteryDiagnostics**
Comprehensive battery health assessment:
- **BatteryModel**: Battery part number/model
- **BatteryTest**: Pass/fail status of battery test
- **DesignCapacity**: Original design capacity in mAh
- **CurrentCapacity**: Current maximum capacity in mAh
- **BatteryHealth**: Percentage of design capacity remaining
- **CycleCount**: Number of charge/discharge cycles
- **BatteryDuration**: Runtime test result in minutes
- **SecondaryBattery**: If present, same metrics for second battery

#### **Step 5: DataSanitization**
Secure data erasure and certification:
- **StorageDevices**: For each storage device (up to 4):
  - Device identification (type, size, model, serial)
  - **ErasureMethod**: NIST 800-88, DoD 5220.22-M, Secure Erase, etc.
  - **ErasureResult**: SUCCESS/FAILED/PARTIAL/SKIPPED
  - **ErasureTimestamp**: When erasure completed
  - **ErasureUser**: Technician who performed erasure
  - **ErasureID**: Certificate or report ID for audit trail
- **DataDestructionCertificate**: Reference to formal certificate

#### **Step 6: GradingAssessment**
Quality grading for refurbished products:
- **Grade**: Overall grade (A/B/C/D/F or custom scale)
- **CosmeticCondition**: Physical appearance assessment
- **FunctionalCondition**: Operational capability assessment
- **PerformanceScore**: Benchmark or performance metrics
- **RefurbishmentActions**: List of refurbishment activities performed
- **QualityCheckResults**: Final quality control outcomes

#### **Step 7: SoftwareValidation**
Operating system and licensing verification:
- **OperatingSystem**: OS installed, version, restoration status
- **COAInformation**: Certificate of Authenticity presence and numbers
- **HardwareID**: Unique hardware identifier for activation
- **IMEI**: For mobile devices with cellular capability
- **LicenseStatus**: Valid/Invalid/Not-applicable

#### **Step 8: AuditTraceability**
Process tracking and audit trail:
- **AuditStatus**: Whether unit has been audited
- **AuditDate**: When audit was performed
- **ExportStatus**: Export readiness status
- **ExportDate**: When exported from system
- **TechnicianUser**: User who performed diagnostics
- **PictureID**: Reference to product images
- **ProcessingLotID**: Batch processing reference

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
| **1** | **DiagnosticEvent** | • Need for event tracking and context<br>• Asset management integration<br>• Batch processing support<br>• Multi-identifier tracking | • UUID-based event IDs<br>• Unit/Lot/Asset identifiers<br>• ISO 8601 timestamps<br>• Trigger enumeration<br>• Refurbishment type added | **TODO** | • Event correlation<br>• Workflow automation |
| **2** | **HardwareInventory** | • Complete hardware discovery<br>• Component serialization<br>• Multi-storage support<br>• Memory slot tracking | • Comprehensive component fields<br>• Up to 4 RAM slots<br>• Up to 4 storage devices<br>• Processor details structure<br>• Motherboard information | **TODO** | • Auto-discovery APIs<br>• Component database |
| **3** | **ComponentTestResults** | • Individual component testing<br>• Pass/fail tracking<br>• Observation recording<br>• Defect coding | • 15+ component test types<br>• Tri-state results<br>• Observation codes<br>• Technician notes field | **TODO** | • Test automation<br>• Defect analytics |
| **4** | **BatteryDiagnostics** | • Battery health metrics<br>• Capacity tracking<br>• Multi-battery support<br>• Runtime testing | • Design vs current capacity<br>• Health percentage<br>• Cycle counting<br>• Duration testing<br>• Secondary battery support | **TODO** | • Predictive degradation<br>• Chemistry detection |
| **5** | **DataSanitization** | • Secure erasure tracking<br>• Multi-drive support<br>• Certification generation<br>• Audit compliance | • NIST/DoD methods<br>• Per-drive tracking<br>• Result enumeration<br>• Certificate IDs<br>• User attribution | **TODO** | • Automated certificates<br>• Blockchain verification |
| **6** | **GradingAssessment** | • Quality grading<br>• Condition assessment<br>• Refurbishment tracking<br>• Market categorization | • A-F grade scale<br>• Cosmetic/functional split<br>• Performance scoring<br>• Action tracking | **TODO** | • ML-based grading<br>• Market pricing |
| **7** | **SoftwareValidation** | • OS verification<br>• License tracking<br>• COA management<br>• Activation status | • OS restoration status<br>• COA number tracking<br>• Hardware ID capture<br>• IMEI for mobile | **TODO** | • License automation<br>• Activation APIs |
| **8** | **AuditTraceability** | • Process tracking<br>• Export management<br>• Image documentation<br>• Batch processing | • Audit status/date<br>• Export tracking<br>• Picture references<br>• Lot ID system<br>• User attribution | **TODO** | • Workflow integration<br>• Image storage |

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
