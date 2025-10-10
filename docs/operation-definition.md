# NOTE: This page needs updating to reflect v0.3

# Operation: Check relevant record exists

Based on [FHIR $match](https://hl7.org/fhir/operation-patient-match.html), returning basic details of service involvments

## Example endpoint

`POST [base]/Patient/$person-info-query`

## Request

A FHIR [Parameters](https://hl7.org/fhir/parameters.html) resource:
- `resource`: a Patient resource (person details – identifiers, DoB, names)
- `reason`: URI string for legal justification (e.g., Children Act s47 investigation)

```json
{
  "resourceType": "Parameters",
  "parameter": [
    {
      "name": "resource",
      "resource": { "resourceType": "Patient",
        "identifier": [
          { "system": "https://fhir.nhs.uk/Id/nhs-number", "value": "1234567890"}
        ],
        "name": [{ "family": "Smith", "given": ["Jane"] }],
        "birthDate": "2015-05-01"
      }
    },
    { "name": "reason", "valueUri": "https://www.legislation.gov.uk/ukpga/1989/41/section/47" }
  ]
}
```

Reason Code Example

`https://www.legislation.gov.uk/ukpga/1989/41/section/47` (Children's Act 1989, Section 47)


## Response
A FHIR Parameters resource:
- match: boolean
- contact (if match=true): Organization and ContactPoint details, for lawful follow-up by requester.

### Example Match Response
```json
{
  "resourceType": "Parameters",
  "parameter": [
    { "name": "match", "valueBoolean": true },
    { "name": "contact",
      "resource": {
          "resourceType": "Organization",
          "name": "Southshire Council Safeguarding",
          "telecom": [{
              "system": "phone", "value": "01234 567890", "use": "work"
          }],
          "address": [{
              "line": ["123 Civic Centre"],
              "city": "Southshire",
              "postalCode": "AB12 3CD",
              "country": "UK"
          }]
      }
    }
  ]
}
```

### Example No Match Response

```json
{
  "resourceType": "Parameters",
  "parameter": [
    { "name": "match", "valueBoolean": false }
  ]
}
```




