# Vital Language Specification

## Introduction

**Vital** is the world’s first programming language designed specifically for global health.  
It enables interoperable, transparent, and auditable health logic—bridging clinical standards, public health protocols, digital health apps, and global governance.

This document provides the core specification for the Vital language: syntax, semantics, types, modules, and health-specific features.

---

## Table of Contents

1. [Design Philosophy](#design-philosophy)
2. [Basic Syntax](#basic-syntax)
3. [Types and Data Structures](#types-and-data-structures)
4. [Modules and Imports](#modules-and-imports)
5. [Functions and Procedures](#functions-and-procedures)
6. [Control Flow](#control-flow)
7. [Health Data Types](#health-data-types)
8. [Adapters and Interoperability](#adapters-and-interoperability)
9. [Security & Privacy](#security--privacy)
10. [Examples](#examples)
11. [Extending the Language](#extending-the-language)

---

## 1. Design Philosophy

- **Purpose-built for health:** Natively supports health data, workflows, and standards.
- **Readable & auditable:** Syntax is simple, transparent, and reviewable by all stakeholders.
- **Interoperable:** Integrates with major health data standards (FHIR, DICOM, HL7, ICD, SNOMED, etc.).
- **Extensible:** Modular by design—adapters, plugins, and SDKs.
- **Secure:** Emphasizes privacy, access control, and data integrity.

---

## 2. Basic Syntax

### Comments
```vital
# This is a single-line comment
```

### Variables and Constants
```vital
let patient_age = 42
const MAX_DOSE = 10.0
```

### Primitive Types
- `int`, `float`, `bool`, `string`, `date`, `datetime`, `list`, `map`

### Example
```vital
let name = "Jane Doe"
let diagnoses = ["E11", "I10"]
let is_minor = patient_age < 18
```

---

## 3. Types and Data Structures

### Built-in Types
- `int`, `float`, `bool`, `string`, `date`, `datetime`

### Lists & Maps
```vital
let meds = ["paracetamol", "insulin"]
let codes = {"ATC": "A10", "ICD": "E11"}
```

### Records (Structs)
```vital
record Patient:
    id: string
    name: string
    birthdate: date
    conditions: list

let p = Patient(id="123", name="Jane Doe", birthdate="1980-05-10", conditions=["E11"])
```

---

## 4. Modules and Imports

### Importing Standard Library or Adapters
```vital
import "stdlib/crypto"
import "adapters/fhir"
import "adapters/icd"
```

---

## 5. Functions and Procedures

### Function Definition
```vital
func bmi(weight: float, height: float) -> float:
    return weight / (height * height)
```

### Procedure (no return)
```vital
proc alert_if_high_bp(bp: float):
    if bp > 140:
        alert("Hypertension detected!")
```

### Lambda/Anonymous Functions
```vital
let square = (x) => x * x
```

---

## 6. Control Flow

### If/Else
```vital
if patient_age < 18:
    category = "child"
else:
    category = "adult"
```

### For Loop
```vital
for med in meds:
    print(med)
```

### While Loop
```vital
while glucose > 200:
    alert("Hyperglycemia")
    glucose = measure_glucose()
```

---

## 7. Health Data Types

- `code`: Standardized code (ICD, ATC, LOINC, etc.)
- `record`: Strongly-typed health record
- `bundle`: Collection of health resources (FHIR bundles)
- `concept`: SNOMED/ontology concepts

### Example
```vital
let icd_code: code = "E11"
let rx = record Medication(name="Metformin", code="A10BA02")
let encounter = bundle([rx, diagnosis])
```

---

## 8. Adapters and Interoperability

Vital supports adapters for health data standards and external systems.

### Using an Adapter
```vital
import "adapters/fhir" as fhir

let patient = fhir.get_patient("123")
let conditions = fhir.get_conditions(patient)
```

### Custom Adapter
Adapters may be written in Python, Rust, Go, etc., and exposed as modules.

---

## 9. Security & Privacy

- Built-in encryption: `encrypt()`, `decrypt()`
- Data masking: `mask()`
- Access control: `require_role("clinician")`
- Audit trails: `audit_log("accessed patient data")`

### Example
```vital
if require_role("clinician"):
    let encrypted = encrypt(patient_record)
    save(encrypted)
```

---

## 10. Examples

### Validate Medication Codes
```vital
import "adapters/atc"
let valid = atc.validate(med_code)
if not valid:
    alert("Invalid medication code")
```

### Encrypt and Store Record
```vital
import "stdlib/crypto"
let encrypted = crypto.encrypt(patient_data)
save(encrypted)
```

### Access Control
```vital
if require_role("admin"):
    show_all_records()
else:
    show_limited_view()
```

---

## 11. Extending the Language

- **Add new adapters** (e.g., for new code sets, EHRs, blockchains)
- **Write plugins** (e.g., for analytics, machine learning)
- **Community modules**: Share and reuse logic globally

---

## See Also

- [README.md](../README.md)
- [adapters.md](adapters.md)
- [roadmap.md](roadmap.md)

---

Vital: **Health access made easy. More years, less pain.**