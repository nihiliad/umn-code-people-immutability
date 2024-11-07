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

* Fantastic data model, but each content types is a huge, 
complex tree, with sub-records, sub-sub-records, etc
* Attempting to load the JSON schema crashed some tools
* [JSON Schema code generators](https://json-schema.org/tools?query=&sortBy=name&sortOrder=ascending&groupBy=toolingTypes&licenses=&languages=&drafts=&toolingTypes=&environments=#schema-to-code) produce a mountain of mostly unneeded classes
---
## Pure research output content type

* 64 level 1 elements, many of which are sub-records
* Only using a fraction of them in my code
* Too many to put on a slide, so go to an editor... 
---
## It's all too much
---
## Simplicity of core data structures

For distributed code...
> we immediately say, "it's gonna be RESTful, it's gonna pass data, it's gonna return data structures,
> it's gonna use JSON". All these great ideas are good over here. Why are they not good inside your
> program? In fact, they are good inside your program.

-- [Simplicity Matters, Rich Hickey, 33:00](https://www.youtube.com/watch?v=rI8tNMsozo0&t=1531s)
---
## Complexity of custom classes

* Write or generate classes for everything
* How to access members?
  * Getters/setters?
  * Custom methods?
  * Inherit from Iterable, Sortable, etc to use core functions?
---
## Contrived example using Pure JSON

```python
pure_json_dict = client.get(pure_json_url).json()
extract_1 = extraction_1(pure_json_dict)
extract_2 = extraction_2(pure_json_dict)
extract_3 = extraction_3(pure_json_dict)

```
---
## Seems simpler, but...
### ...Python dictionaries are mutable...
...as are most Python data structures
---
### Add validation?
What happens if one of the extraction functions modifies `pure_json_dict`?

```python
@validate_pure_json
def extraction_1(pure_json_dict): ...

@validate_pure_json
def extraction_1(pure_json_dict): ...
```
---
## Lots of redundant validation

What if we could `pure_json_dict` immutable?
---
## Benefits of immutability

* Predictability
* Thread-safety for concurrency & parallelism
* Fewer side effects, fewer bugs
---
## pyrsistent

[pyrsistent](https://pyrsistent.readthedocs.io/) provides immutable versions of core data structures for Python
---
## Immutable dicts

```python
from pyrsistent import pmap
pure_json_dict = pmap(
    client.get(pure_json_url).json()
)
```
---
## But what about validation?

We know that immutable dicts will never change, but how do we know the dict is valid in the first place?
If we add validation, how do we know that the dict has been validated?
---
## Can we make a validated immutable dict?

Would like to do this:
```python
pure_json_dict = PureJson.create(pure_json_dict)
    client.get(pure_json_url).json()
)
extract_1 = extraction_1(PureJson: pure_json_dict)
...
```
---
## Problem

pyrsistent allows for validation with checked types, like [PRecord](), but it requires specifying the
entire data structure. Back to lots of unnecessary work!
---
## Solution: `pyrsistent_ext`

So at Campus Code Fest 2024, Karl Kaess and I created [pyrsistent-ext](https://github.com/UMNLibraries/pyrsistent-ext)
which allows for validating only certain parts of an immutable dict, ignoring the rest.
---
## Live demo!
---
## Thank you!
---
## Questions?

