## [datamodel-code-generator](https://github.com/koxudaxi/datamodel-code-generator/) reproducible example for [issue #2460](https://github.com/koxudaxi/datamodel-code-generator/issues/2460)

|Inputs|Outputs|
|-|-|
|[inputs/aaaschema.json](inputs/aaaschema.json)|[outputs/aaaschema.py](outputs/aaaschema.py)|
|[inputs/commons.json](inputs/commons.json)|[outputs/commons.py](outputs/commons.py)|
|[inputs/bug.json](inputs/bug.json)|[outputs/bug.py](outputs/bug.py)|

[Debug logs HERE](debug_logs.txt)

### Description of the problem

- I define `allowedAnimals` in `aaaschema.json` as an array of objects
- I generate the code. A RootModel is generated and it works.
- I define `allowedAnimals` as object with `additionalProperties: false` in `bug.json`
- I generate the code. The model of the first schema has been edited and now the RootModel has `extra: forbid` (which is not valid)
- I rename `allowedAnimals` in `bug.json` with a different name
- Now the generated code of `aaaschema.json` is correct again.

### Goal

We don't want `bug.json` definitions to interfere with the generation of the models for `aaaschema.json`

### Issue

Somehow, `allowedAnimals` definition in `bug.json` add `extra: false` to `allowedAnimals` `RootModel` generated for `aaaschema.json` which result in an:

- Incorrect behavior
- Invalid output

### Generate models

```sh
$ pip install -r requirements.txt
$ datamodel-codegen
```