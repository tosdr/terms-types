# Terms Types Definitions
| Name      | Description |
| ----------- | ----------- |
| Terms of Service      |  concerns end user’s service usage     |
| Privacy Policy   | concerns end user’s personal data        |
| Imprint | identification of content author and hosting service for official inquiries |
| Trackers Policy | concerns all tracking technologies, including cookies, session storage, fingerprints, etc. |
| Developer Terms | concerns APIs and programmatic access to content |
| Community Guidelines | concerns public behavior of the end user |
| Deceased Users | concerns handling of information of a deceased indiviudal |
| Acceptable Use Policy | concerns acceptable and unacceptable usage by the end user |
| Restricted Use Policy | concerns restrictions on specific usage by the end user |
| Commercial Terms | concerns business or commercial usage |
| Copyright Claims Policy | concerns how copyright complaints (DMCA…) will be handled |
| Law Enforcement Guidelines | concerns account records access |
| Human Rights Policy | concerns human rights |
| In-App Purchases Policy | concerns usage of virtual purchases |
| Review Guidelines | concerns review process of provided content |
| Brand Guidelines | concerns usage of the service provider’s brand |
| Quality Guidelines | concerns quality of content produced by means of the service |
| Data Controller Agreement | concerns treatment of end user personal data by data controllers (in the sense of GDPR) |
| Data Processor Agreement | concerns the status of the data processor (in the sense of GDPR) for the service provider |
| User Consent Policy | concerns user consent collection and storage by data controllers (in the sense of GDPR) |
| Closed Captioning Policy | concerns closed captioning on streamed content |
| Seller Warranty | concerns protection of end users that act as sellers |
| Single Sign-On Policy | concerns connecting user accounts to other services |
| Vulnerability Disclosure Policy | concerns how to report a security vulnerability or issue |
| Live Policy | concerns end user’s live service usage |
| Complaints Policy | concerns how generic complaints will be handled |
| Conditions of Carriage | concerns benefits and limitations associated with the transportation being provided by transportation operators such as airlines, railways, buses, etc.) |
| General Conditions of Sale | concerns the warranty, delivery, return of goods or services bought through a monetary transaction |
| Marketplace Buyers Conditions | concerns buying through a monetary transaction goods or services offered by sellers other than the marketplace itself |
| Marketplace Sellers Conditions | concerns selling through a monetary transaction goods or services to buyers other than the marketplace itself |
| Frequently Asked Questions | frequently asked questions about the service, its policies |
| Coporate Social Responsibility | concerns practices integrating social, environmental and profit-related considerations |
| Social Media Policy | service provider guidance on how employees should act on social media |
| Uniform Disclosure | used to disclose certain information to end users |
| Affiliate Disclosure | statement informing users that companies compensate you for promoting, reviewing, or recommending their products or services |
| Safety Guidelines | service provider protocols to ensure online safety |
| Telephone Communication Guidelines | restrictions on telephone solicitations (i.e. telemarketing) and the use of automated phone equipment |
| Records Keeping Policy | policies in handling of user records in the event of bankruptcy or data transfer |
| Service Level Agreement | outlines a commitment between a service provider and a client |
| Legal Information | documentation covering miscellaneous policies, notices, and disclaimers |
| Policy | generic policies not included in privacy policy coverage |
| About | generic information pages |
| Miscellaneous Agreement | various agreements published by the service |
| Ranking Parameters Description | concerns search engine or intermediation service provider parameters determining ranking and the reasons for their relative importance |
| Premium Partner Conditions | concerns sellers' eligibility criteria, limitations and benefits of a privileged seller status programme |
| Platform to Business Notice | concerns complaints handling, mediation, transparency and other rights and information mandated by the P2B regulation |
| Business Mediation Policy | concerns business users' eligibility and process of mediation after internal complaints handling failed |
| Business Privacy Policy | concerns personal data of business users and of people acting on their behalf |


# Terms Types

Terms Types are an ontology describing all known sorts of terms and conditions to the Open Terms Archive project.

It aims at unifying the many names that services give to similar documents to enable comparison of terms across services no matter how they are named by their provider.

## Installation

```bash
npm install @opentermsarchive/terms-types
```

## Usage

```js
import TERMS_TYPES from '@opentermsarchive/terms-types';

console.log(TERMS_TYPES['Terms of Service']); // Display `Terms of Service` details

console.log(Object.keys(TERMS_TYPES)); // Display all terms types
```

## Data structure

This repository contains a database of types of terms of service (“agreement”, “policy”, “guidelines”…) under which a service is delivered.

The `termsTypes.json` JSON file is a map of [title cased](https://en.wikipedia.org/wiki/Title_case) terms types.

The types might not always match the exact name given by the service provider. For example, some providers might call their document “Terms and Conditions” or “Terms of Use” instead of “Terms of Service”. The terms type does not have to match the exact name, it only has to match the commitment that is taken.

### Name

The name of each type is written with title capitalisation (every noun is capitalised).

It should be the most commonly used and most internationally understandable for this type.

### Tryptich

In order to guide usage and disambiguate synonyms, each terms type is characterised by a tryptich along the three dimensions of the `commitment` that is being taken in it:

- the `writer` of the document, in most cases the service provider itself;
- the targeted `audience` whose rights and duties are defined in the associated terms;
- the `object` of the commitment, i.e. the information or interaction whose handling will be constrained by the associated terms.

Each type thus has the following structure, where all fields are required:

```json
{
  "<Terms Type Name>": {
    "commitment": {
      "writer": "<writer>",
      "audience": "<audience>",
      "object": "<object>"
    }
  }
}
```

### References

It may also contain an optional `references` property which contains a map of related resources that may help to understand the purpose of this type, such as legal definitions, or the discussions that led to the choice of this name. Each reference must have a name and a URL.

```json
{
  "<Terms Type Name>": {
    "commitment": { … },
    "references": {
      "<reference name>": "<URL where the reference can be found>"
    }
  },
}
```

### Example

```json
{
  "Business Mediation Policy": {
    "commitment": {
      "writer": "intermediation service provider",
      "audience": "business users",
      "object": "mediation process after internal complaints handling failed"
    },
    "references": {
      "Open Terms Archive discussion": "https://github.com/OpenTermsArchive/engine/discussions/933",
      "P2B Regulation 2019/1150, Article 12": "https://eur-lex.europa.eu/eli/reg/2019/1150/oj#d1e1148-57-1"
    }
  },
}
```

## How to define the tryptich

To identify the tryptich of specific terms, answer the following questions:

1. Who is responsible for creating and maintaining those terms? Most often, it will be the `service provider` itself. Sometimes, while still being the service provider, it could be that only providers from a certain industry could write such terms, such as `transportation operator`.
2. Who is the target audience whose rights and duties are defined? Often, it will be the `end user`, but it can also be the `commercial partners` or `business users`, for example.
3. Which information or interaction precisely is constrained by those terms? For example, the `end users’ personal data`, or maybe the `privileged seller status programme`. Try to be as specific as possible, as this precision enables distinguishing between otherwise similar types.

After having answered these questions, if reading out loud the tryptich, it sounds right to say that **“these terms describe how the `<writer>` commits to handle the `<object>` for its `<audience>`”**.

## Add new terms types

Contributions to expand the list of known terms types are welcome, but need to follow a strict design, review and validation process in order to ensure consistency in the ontology. If you'd like to suggest a new type, please follow the process detailed in the [CONTRIBUTING file](CONTRIBUTING.md).

---

## License

The code for this software is distributed under the European Union Public Licence (EUPL) v1.2.
Contact the author if you have any specific need or question regarding licensing.
