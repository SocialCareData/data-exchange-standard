## Data Exchange Standard v0.1 - Early thinking to start discussions

### Introduction
With regard to multiagency information sharing, we are aware of two dominant operating models currently in use across local authorities and their partners across Health and the Police. These are:

- **Centralised "data lake" models**: Where copies of relevant datasets are taken from internal and external source systems, transferred to a central location, with apps then deployed on top for practitioners to view the data
- **Decentralised, API driven models**: Where connections are established between data sources, to allow for a temporary view of the other agencies' data for practitioners without the need to copy across or duplicate data

 The majority of "single view" tools currently deployed across the country are created as "data lake" models. However, these models have an intrinsic challenge with regard to scalability, governing duplicative data and data ownership. It has also been historically very difficult for local authorities to access person level health data, with the 2024 Supporting Families Data survey conducted by the Department for Education finding that significantly fewer local authorities were able to access physical and mental health data for children and their families compared to children's services, education, financial, housing and crime data. Dispersed, API driven models are much more common across the NHS, with shared care records generally being built on this principle.

 We are therefore focusing the first version of our Data Exchange standard on supporting **Decentralised, API driven models**:

- We believe that both digitally mature and maturing local authorities will be able to benefit from this standard, through the introduction of a standardised way for common systems across the local authority, police and health to connect and share information between each other
- We believe that Integrated Care Boards and NHS trusts are more likely to agree to information sharing arrangements based on API driven models, due to them being able to retain greater control of the data being shared
- We believe that this is more closely aligned to the direction of travel for local authorities and their safeguarding partners, thus creating a more 'future proof' model

There will still be challenges to navigate, however through careful engagement with the sector over the coming months we hope to create a Data Exchange Standard which will present real value to local safeguarding partners and significantly reduce current barriers preventing multiagency information sharing in local contexts. We anticipate that future versions of the Data Exchange standard will be able to support both centralised and decentralised models.

## Purpose

This standard defines a FHIR-based API approach to automate the first critical component of multiagency data exchange. It defines a pattern by which one organisation can ask other organisations: "Do you have information about a child within your system?" and receive a set of standardised replies.

It demonstrates the use of the [FHIR Parameters resource](https://hl7.org/fhir/parameters.html) as input and response payload, supports validation, and will  include a test environment to test sending and responding to queries.

## Proposed Features

- Example FHIR Parameter resource API call
- Example request and response payloads
- FHIR validation approach
- Test server

## Comparison with existing standards

### [Digital Child Health - FHIR](https://digital.nhs.uk/developer/api-catalogue/digital-child-health-fhir)
Sharing information about a child's health between healthcare workers.

This integration uses a publish-subscribe model - the sending system publishes events to [National Events Management Service (NEMS)](https://digital.nhs.uk/services/national-events-management-service), and NEMS forwards the events to all subscribed systems via [Message Exchange for Social Care and Health (MESH)](https://digital.nhs.uk/developer/guides-and-documentation/api-technologies-at-nhs-digital#mesh).

Subscribed systems might be GPs, emergency departments, local authorities or some other care provider. Potentially, patients and carers could also share this information.

For details of the legal basis for sharing NEMS events, see the [NEMS controller catalogue](https://developer.nhs.uk/apis/ems-beta/controller_catalogue.html).

### [Child Protection - Information Sharing - HL7 V3 API](https://digital.nhs.uk/developer/api-catalogue/child-protection-information-sharing-hl7-v3)
Access child protection information from Child Protection - Information Sharing (CP-IS) from a healthcare setting.




