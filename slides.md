## Immutability for More Elegant Code
### David Naughton
#### Application Development, UMN Libraries
---
## Actually, immutable core language data structures...

...but that would make for too wordy a title.
---
## Why? How?
---
## Example: Pure API JSON

[Pure](https://www.elsevier.com/products/pure) is a vendor
product we use for [Experts@Minnesota](https://experts.umn.edu).
---
## Pure data model

Pure has a fantastic data model for research output metadata,
but it is huge, hierarchical, and complex, with many sub-records,
sub-sub-records, etc.
---
## Pure research output top-level elements

| 1                          | 2                    | 3                     | 4                    |
|----------------------------|----------------------|-----------------------|----------------------|
| managingOrganisationalUnit | totalNumberOfAuthors | numberOfPages         | totalScopusCitations |
| electronicVersions         | externalIdSource     | bibliographicalNote   | personAssociations   |
| category                   | electronicIsbns      | pages                 | language             |
| publisher                  | isbns                | openAccessPermission  | publicationStatuses  |
| title                      | additionalLinks      | confidential          | organisationalUnits  |
| keywordGroups              | info                 | externalOrganisations | visibility           |
| pureId                     | scopusMetrics        | hostPublicationTitle  | abstract             |
| type                       | workflow             | uuid                  | externalId           |
---
## MD Slide 1
A paragraph with some text and a [link](https://hakim.se).
---
## MD Slide 2

```python
@decorator
def function(int: x, int: y) -> int:
    return x + y
```
---
## MD Slide 3
