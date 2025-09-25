## Data Exchange Standard - Early thinking to start discussions

Status: Version 0.2 - refining our early thinking after various discussions

Effective Date: 2025-09-25

### Introduction
With regard to multiagency information sharing, we are aware of two dominant operating models currently in use across local authorities and their partners across health, education and the Police. These are:

- **Centralised "data lake" models**: Where copies of relevant datasets are taken from internal and external source systems, transferred to a central location, with apps then deployed on top for practitioners to view the data
- **Decentralised, API driven models**: Where connections are established between data sources, to allow for a temporary view of the other agencies' data for practitioners without the need to copy across or duplicate data

 The majority of "single view" tools in children's social care (CSC) currently deployed across the country are created as "data lake" models. However, these models have an intrinsic challenge with regard to scalability, governing duplicative data, and data ownership. It has also been historically very difficult for local authorities to access person level health data, as seen in the 2024 Supporting Families Data survey conducted by the Department for Education that found significantly fewer local authorities were able to access physical and mental health data for children and their families compared to children's services, education, financial, housing and crime data. Dispersed, API driven models are much more common across the NHS and adult social care, with shared care records generally being built on this principle.

 Given the challenges and limitations of "data lake" models, we are focusing the first version of our Data Exchange standard on supporting **Decentralised, API driven models**:

- We believe that both digitally mature and maturing local authorities will be able to benefit from this standard, through the introduction of a standardised way for common systems across the local authority, education, police and health to connect and share information between each other
- We believe that Integrated Care Boards and NHS trusts are more likely to agree to information sharing arrangements based on API driven models, due to them being able to retain greater control of the data being shared
- We believe that this is more closely aligned to the direction of travel for local authorities and their safeguarding partners, thus creating a more 'future proof' model

There will still be challenges to navigate, however through careful engagement with the sector over the coming months we hope to create a Data Exchange Standard which will present real value to local safeguarding partners and significantly reduce current barriers preventing multiagency information sharing in local contexts across children's and adult social care. We anticipate that future versions of the Data Exchange standard will be able to support both centralised and decentralised models.

## Purpose

This standard defines a FHIR-based API approach to automate critical components of multiagency data exchange.

This first release proposes a pattern by which one organisation can ask other organisations: "Do you have information about a person within your system?" and receive a set of standardised replies.

This applies to all agencies and organisations covered by relevant safeguarding and wellbeing legislation e.g. social care, health, welfare, education, etc.

It provides a profile of the [FHIR Parameters resource](https://hl7.org/fhir/parameters.html) as request and response payload:

- Constrained variant of [$match](https://hl7.org/fhir/operation-patient-match.html) operation.
- Extends query with "reason" code - with values from an agreed vocabulary / codelist.
- Response indicates whether the person is known to the system, and whether there is an active sevice involvement, with contact details for further information.

Around this technical specificiation, there are a set of conditions which are required to support trusted machine-to-machine data exchange that is proportionate and effective. These are being explored under [Information Governance](https://github.com/SocialCareData/taxonomy/blob/main/information_governance.md).


## Roadmap

Proposed content for initial release:
- Example FHIR Parameter resource API request and response payloads
- StructureDefinition for new profile of Parameter resource, describing extensions and constraints
- FHIR validation approach
- Test server and dummy data to test sending and responding to queries
- Links to the person standard, registry of participating organisations/systems, shared vocabularies.
- Audit and logging requirements


Subsequent releases will build on these capabilities to:

- define data linking / matching requirements, tests and expected performance. This will include thresholds for probability matching and agreed approaches for example in the case of multiple possible matches.
- facilitate data exchange where a relevant care record, service involvement, observation or event is found
- support data exchange between centralised and decentralised systems

## How it works

- Request includes person identifiers AND reason for request.
- Request issued by an autorised person using a recognised, validated system.
- An agreed decision rules process defines if a response can be shared automatically or not, or if an escalation required.
- If person known or 'open' on the system, returns contact details for further enquiry.

See: [docs/operation-definition.md](docs/operation-definition.md)

## Assumptions

- The request and response should be system agnostic.
- The implementation of the [match](https://build.fhir.org/patient-operation-match.html) operation may vary between systems.
- All participating systems will meet relevant data privacy and cyber security standards.

## Comparison with existing services

Several API based data exchange standards are already in production in Health and Social Care, however none fully meet the requirements for this use case. This is largely due to the range of partner organisations and systems and variations in the legal bases for sharing data.

### [National Record Locator (NRL)](https://digital.nhs.uk/services/national-record-locator/)
Allows users to find and access patient information shared by other health and social care organisations, to support the direct care of a patient.
The NRL does not hold a copy of the data, but 'pointers' to records in other organisations' systems.

There is no equivalent directory system for children's social care, but this is an idea that is being explored.
We assume that the pattern for data exchange described in this standard could be directly applied to such a directory system in the future.

### [Personal Demographics Service - FHIR API](https://digital.nhs.uk/developer/api-catalogue/personal-demographics-service-fhir)
Access patients' personal information, such as name, address, date of birth, related people, registered GP, nominated pharmacy and NHS number using the FHIR version of the Personal Demographics Service (PDS) API.

### [Digital Child Health - FHIR](https://digital.nhs.uk/developer/api-catalogue/digital-child-health-fhir)
Sharing information about a child's health between healthcare workers.

This integration uses a publish-subscribe model - the sending system publishes events to [National Events Management Service (NEMS)](https://digital.nhs.uk/services/national-events-management-service), and NEMS forwards the events to all subscribed systems via [Message Exchange for Social Care and Health (MESH)](https://digital.nhs.uk/developer/guides-and-documentation/api-technologies-at-nhs-digital#mesh).

Subscribed systems might be GPs, emergency departments, local authorities or some other care provider. Potentially, patients and carers could also share this information.

This integration can only be used where there is a legal basis to do so.

For details of the legal basis for sharing NEMS events, see the [NEMS controller catalogue](https://developer.nhs.uk/apis/ems-beta/controller_catalogue.html).

### [Child Protection - Information Sharing - HL7 V3 API](https://digital.nhs.uk/developer/api-catalogue/child-protection-information-sharing-hl7-v3)
Access child protection information from Child Protection - Information Sharing (CP-IS) from a healthcare setting.





