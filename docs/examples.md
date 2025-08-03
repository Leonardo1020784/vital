# Vital Language Examples

This document showcases practical examples of how to use the Vital language to solve real health data problems, automate workflows, and ensure interoperability across global health standards.

---

## Table of Contents

1. [Basic Syntax](#basic-syntax)
2. [Health Code Validation](#health-code-validation)
3. [Encrypting and Saving Data](#encrypting-and-saving-data)
4. [Role-Based Access Control](#role-based-access-control)
5. [Using Adapters (FHIR, ATC, ICD, etc.)](#using-adapters-fhir-atc-icd-etc)
6. [Mapping Codes](#mapping-codes)
7. [Automated Alerts and Reporting](#automated-alerts-and-reporting)
8. [Custom Health Workflows](#custom-health-workflows)
9. [Composing Logic with Modules](#composing-logic-with-modules)
10. [Advanced: Integrating with External Systems](#advanced-integrating-with-external-systems)

---

## 1. Basic Syntax

```vital
# Declare variables
let patient_name = "Ana Maria"
let patient_age = 32

# Simple logic
if patient_age > 65:
    category = "elderly"
else:
    category = "adult"
```

---

## 2. Health Code Validation

```vital
import "adapters/icd" as icd
let diagnosis_code = "E11"
let is_valid = icd.validate(diagnosis_code)
if not is_valid:
    alert("Invalid ICD code!")
```

---

## 3. Encrypting and Saving Data

```vital
import "stdlib/crypto"
let patient_record = {name: "Luis", dob: "1970-01-01", id: "P-001"}
let encrypted = crypto.encrypt(patient_record, key=ENV.SECRET_KEY)
save(encrypted)
```

---

## 4. Role-Based Access Control

```vital
if require_role("clinician"):
    show_full_record()
else:
    show_limited_view()
```

---

## 5. Using Adapters (FHIR, ATC, ICD, etc.)

**FHIR Example:**
```vital
import "adapters/fhir" as fhir
let patient = fhir.get_patient("P-123")
let encounters = fhir.get_encounters(patient)
```

**ATC Example:**
```vital
import "adapters/atc" as atc
let med_code = "A10BA02"
let is_valid_med = atc.validate(med_code)
let med_name = atc.description(med_code)
```

---

## 6. Mapping Codes

```vital
import "adapters/icd" as icd
let icd_code = "I10"
let snomed_codes = icd.map_to_snomed(icd_code)
```

---

## 7. Automated Alerts and Reporting

```vital
let bp = 150
if bp > 140:
    alert("Hypertension detected")
    report_to_registry({patient: patient_name, bp: bp})
```

---

## 8. Custom Health Workflows

```vital
import "adapters/loinc" as loinc

# Validate and process a lab result
let loinc_code = "4548-4"
if loinc.validate(loinc_code):
    process_lab_result(loinc_code, value=7.2)
else:
    alert("Unknown LOINC code")
```

---

## 9. Composing Logic with Modules

```vital
import "modules/triage_rules"
import "adapters/fhir" as fhir

let patient = fhir.get_patient("P-987")
let triage_decision = triage_rules.evaluate(patient)
```

---

## 10. Advanced: Integrating with External Systems

**Firebase Example:**
```vital
import "adapters/firebase" as fb

let record = {id: "P-002", status: "active"}
fb.save("patients", record)
```

**Google Healthcare Example:**
```vital
import "adapters/google_healthcare" as ghc

let patient_data = {...}
ghc.upload_patient(patient_data)
```

---

## See Also

- [language_spec.md](language_spec.md)
- [adapters.md](adapters.md)
- [architecture.md](architecture.md)

---

Vital: **Programmable health for everyone, everywhere.**