# Vital Adapters Specification

Vital adapters are modules that connect the Vital language to external health data standards, clinical code sets, APIs, and third-party systems.  
They power interoperability, enabling Vital programs to read, validate, transform, and write data across the global health ecosystem.

---

## Table of Contents

1. [What is an Adapter?](#what-is-an-adapter)
2. [Supported Adapters & Standards](#supported-adapters--standards)
3. [Adapter Structure](#adapter-structure)
4. [Example: Using an Adapter in Vital](#example-using-an-adapter-in-vital)
5. [Building Your Own Adapter](#building-your-own-adapter)
6. [Best Practices](#best-practices)
7. [Roadmap](#roadmap)
8. [Resources](#resources)

---

## 1. What is an Adapter?

An **adapter** in Vital is a plug-in module that allows the language to work with:

- Health data standards (FHIR, DICOM, HL7, ICD, SNOMED, LOINC, ATC, etc.)
- External APIs and databases (e.g., Google Healthcare, OpenMRS, hospital EHRs)
- Code lists, mappings, and ontologies (e.g., JSON files for ATC, CPT, LOINC, etc.)

Adapters expose functions, types, and transformations that can be imported and used in `.vital` programs.

---

## 2. Supported Adapters & Standards

Vital aims to support all major health data standards.  
Initial adapters include (but are not limited to):

| Adapter    | Description                          | Location                |
|------------|--------------------------------------|-------------------------|
| FHIR       | HL7 Fast Healthcare Interoperability Resources | `adapters/fhir/`   |
| DICOM      | Digital Imaging and Communications in Medicine | `adapters/dicom/`  |
| HL7        | HL7 v2/v3 Messaging                  | `adapters/hl7/`         |
| ICD        | International Classification of Diseases | `adapters/icd/`     |
| SNOMED     | SNOMED CT Clinical Terms             | `adapters/snomed/`      |
| LOINC      | Logical Observation Identifiers Names and Codes | `adapters/loinc/` |
| ATC        | Anatomical Therapeutic Chemical Classification | `adapters/atc/`    |
| CPT        | Current Procedural Terminology       | `adapters/cpt/`         |
| Custom     | Any local or global code set         | `adapters/`             |

Adapters may be implemented in Python, Rust, Go, C#, TypeScript, or other languages.

---

## 3. Adapter Structure

A typical adapter contains:

- **Loader**: Reads data from JSON, API, or DB.
- **Validator**: Checks if codes/entries are valid.
- **Mapper**: Converts between code systems or formats.
- **Functions/Types**: Exposes usable functions/types to `.vital` scripts.

**Example: adapters/icd/icd_adapter.py**
```python
def validate(code: str) -> bool:
    # Checks if code exists in ICD JSON file
    ...

def description(code: str) -> str:
    # Returns human-readable description
    ...

def map_to_snomed(icd_code: str) -> list:
    # Returns possible SNOMED CT equivalents
    ...
```

---

## 4. Example: Using an Adapter in Vital

**Importing and using ICD and ATC adapters:**
```vital
import "adapters/icd" as icd
import "adapters/atc" as atc

let valid_icd = icd.validate("E11")
let med_name = atc.description("A10BA02")

if not valid_icd:
    alert("Invalid ICD code")
```

**FHIR Adapter Example:**
```vital
import "adapters/fhir" as fhir

let patient = fhir.get_patient("12345")
let conditions = fhir.get_conditions(patient)
```

---

## 5. Building Your Own Adapter

1. **Create a new directory in `/adapters/`** for your standard or API.
2. **Implement loader functions** for your data source (JSON, API, DB).
3. **Expose functions** for validation, mapping, and transformation.
4. **Document** usage in a `README.md` in your adapter’s folder.
5. **Add tests** to `/tests/` to ensure reliability.

**Minimal example:**
```python
# adapters/loinc/loinc_adapter.py
def validate(loinc_code: str) -> bool:
    ...
def description(loinc_code: str) -> str:
    ...
```

---

## 6. Best Practices

- **Keep adapters stateless** where possible—pure functions are easier to test and maintain.
- **Cache large code sets** in memory for performance, but reload as needed.
- **Document** all public functions and provide usage examples.
- **Write tests** for all validation/mapping functions.
- **Follow privacy and security best practices**: Never expose sensitive data unintentionally.

---

## 7. Roadmap

- Expand coverage for more standards and regions.
- Enable real-time adapters for streaming APIs.
- Foster community-built adapters for local code sets and emerging standards.
- Support adapters for blockchain, AI models, and privacy-preserving computation.

---

## 8. Resources

- [Vital Language Specification](language_spec.md)
- [FHIR Standard](https://www.hl7.org/fhir/)
- [ICD Codes](https://www.who.int/standards/classifications/classification-of-diseases)
- [SNOMED CT](https://www.snomed.org/)
- [LOINC](https://loinc.org/)
- [DICOM](https://www.dicomstandard.org/)
- [HL7](https://www.hl7.org/)

---

Vital Adapters: Powering global health interoperability.