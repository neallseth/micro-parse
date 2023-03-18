# micro-parser

Easily parse & consume [microdata](https://developer.mozilla.org/en-US/docs/Web/HTML/Microdata)

## Installation

`npm i micro-parse`

## Usage

```
import microdataParse from "micro-parse";
const html = '<div itemscope itemtype="https://schema.org/SoftwareApplication">...</div>'
console.log(microdataParse(html));
```

The above should produce an object with the following structure, mapping identically to the microdata hierarchy of its source data:
```
{ scope: 'https://schema.org/SoftwareApplication', metadata: {...}, children: [...] }
```

In the above, `scope` indicates a defined [microdata scope](https://schema.org/docs/gs.html#microdata_itemscope_itemtype), `metadata` represents all data associated with the given scope level, and `children` includes all sub-scopes (array members are objects repeating the above structure)
