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

In unusual cases where metadata is updated client-side, we can allow script execution as follows:
```
const html = '<div itemscope itemtype="https://schema.org/SoftwareApplication">...</div>'
const options = { runScripts: "dangerously" };
console.log(microdataParse(html, options));
```

Note that you incur some risk when running unknown scripts. Warning from JSDOM docs:
> ...this is also highly dangerous when dealing with untrusted content. The jsdom sandbox is not foolproof, and code running inside the DOM's <script>s can, if it tries hard enough, get access to the Node.js environment, and thus to your machine.

All options passed will be relayed to JSDOM – as such, all JSDOM-supported options are available. Absence of the second `options` argument will skip JSDOM altogether, often yielding performance gains north of 50%.

