# Test generator for Visual Studio Code

## Description

Test generator is a VSCode Extension which quickly generate test files from Typescript source files.


![dotup-vscode-test-generator Video](https://raw.githubusercontent.com/dotupNET/dotup-vscode-test-generator-docs/master/images/video.gif)

## Installation

You can browse and install extensions from within VS Code. Press `Ctrl+P` and narrow down the list commands by typing `ext install dotup-vscode-test-generator`.

Or download from [Visual Studio Marketplace](
https://marketplace.visualstudio.com/items?itemName=dotup.dotup-vscode-test-generator).

## Usage

### 1. Command:

Open a typescript file with one or more class definitions and press `Ctrl+Shift+P` to see all commands and start typing `Generate test file` and hit `Enter`.

### 2. Context menu
Select a typescript file in the explorer, open  `context menu` and select `Generate test file`.

## General Extension Settings

This extension contributes the following settings:

* `dotupGenerateTestFile.testFileLocation`: Where should test files be created? Either in `source file path` or in `workspace root path`.
* `dotupGenerateTestFile.sourceDirectoryName`:
Name of directory with source files. E.g. `src`
* `dotupGenerateTestFile.testDirectoryName`: Name of the test directory. Only required when using `workspace root path` as test file location.
* `dotupGenerateTestFile.testFileSuffix`: Suffix for test files. E.g. `Suffix` NiceService.ts -> NiceService.Suffix.ts

## Template Extension Settings:

* `dotupGenerateTestFile.template.file`

  *Template for the whole test file.*

Default value:

```json
"default": [
  "${Imports}",
  "",
  "${FileTests}"
]
```

Placeholders:
- ${Imports} - Place to put import statements
- ${FileTests} - Place to put test statements ( Test statements for one or more classes.)

---

* `dotupGenerateTestFile.template.class`

  *Template for one class.*

Placeholder:
>- ${ClassName} - Replaced with the current class name
>- ${ClassTests} - Test statements for current class

Sample configuration:

```json
"default": [
  "describe('Test class ${ClassName}', () => {",
  "${ClassTests}",
  "});",
  ""
],
```

---

* `dotupGenerateTestFile.template.method`

  *Template for one method call.*
    
```typescript
    ClassName.MethodName();
```

* `dotupGenerateTestFile.template.asyncmethod`

  *Template for one async method call. The generated code contains the `async` keyword, something like this:*
    
```typescript
    await ClassName.MethodName();
```

Placeholder:
>- ${ClassName} - Replaced with the current class name
>- ${MethodName} - Current method name to test
>- ${Declarations} - Variable declaration for current test
>- ${MemberTests} - Method calls

Sample configuration:

```json
"default": [
  "it('${MethodName}', () => {",
  "// Arguments",
  "${Declarations}",
  "",
  "// Method call",
  "${MemberTests}",
  "});"
]
```

---

* `dotupGenerateTestFile.template.function`: 

  *Template for one method call with return value.*
  
```typescript
    const MethodCallResult = ClassName.MethodName();
```

* `dotupGenerateTestFile.template.asyncfunction`: 

  *Template for one async method call with return value. The generated code contains the `async` keyword, something like this:*
 
```typescript
    const MethodCallResult = async ClassName.MethodName();
```

Placeholders:
>- ${ClassName} - Replaced with the current class name
>- ${MethodName} - Current method name to test
>- ${Declarations} - Variable declaration for current test
>- ${MemberTests} - Method calls
>- ${MethodCallResult} - Replaced with method call result variable

Sample configuration:

```json
"default": [
  "it('${ClassName}-${MethodName}', () => {",
  "// Arguments",
  "${Declarations}",
  "",
  "// Method call",
  "${MemberTests}",
  "",
  "// Expect result",
  "expect(${MethodCallResult}).to.be.not.undefined;",
  "});"
]
```

---

* `dotupGenerateTestFile.template.property`

  *Template for one property call.*

Placeholders:
>- ${ClassName} - Replaced with the current class name
>- ${PropertyName} - Current method name to test
>- ${Declarations} - Variable declaration for current test
>- ${MemberTests} - Method calls
>- ${PropertyGetResult} - Replaced with property get result
>- ${PropertySetVariable} - Replaced with the variable name, assigned to the property

Sample configuration:

```json
"default": [
  "it('${ClassName}-${MethodName}', () => {",
  "// Arguments",
  "${Declarations}",
  "",
  "// Method call",
  "${MemberTests}",
  "",
  "// Expect result",
  "expect(${PropertyGetResult}).equals(${PropertySetVariable});",
  "});"
]
```
## Complete settings sample

```json
{
  "dotupGenerateTestFile.testFileLocation": "test directory",
  "dotupGenerateTestFile.sourceDirectoryName": "src",
  "dotupGenerateTestFile.testDirectoryName": "test",
  "dotupGenerateTestFile.testFileSuffix": "g.test",
  "dotupGenerateTestFile.template.file": [
    "import { expect } from 'chai';",
    "${Imports}",
    "",
    "${FileTests}"
  ],
  "dotupGenerateTestFile.template.class": [
    "describe('Test class ${ClassName}', () => {",
    "",
    "${ClassTests}",
    "});",
    ""
  ],
  "dotupGenerateTestFile.template.method": [
    "it('${ClassName}.${MethodName}()', () => {",
    "// Arguments",
    "${Declarations}",
    "",
    "// Method call",
    "${MemberTests}",
    "});",
    ""
  ],
  "dotupGenerateTestFile.template.asyncMethod": [
    "it('${ClassName}.${MethodName}()', async () => {",
    "// Arguments",
    "${Declarations}",
    "",
    "// Method call",
    "${MemberTests}",
    "});",
    ""
  ],
  "dotupGenerateTestFile.template.function": [
    "it('${ClassName}.${MethodName}()', () => {",
    "// Arguments",
    "${Declarations}",
    "",
    "// Method call",
    "${MemberTests}",
    "",
    "// Expect result",
    "expect(${MethodCallResult}).to.be.not.undefined;",
    "});",
    ""
  ],
  "dotupGenerateTestFile.template.asyncFunction": [
    "it('${ClassName}.${MethodName}()', async() => {",
    "// Arguments",
    "${Declarations}",
    "",
    "// Method call",
    "${MemberTests}",
    "",
    "// Expect result",
    "expect(${MethodCallResult}).to.be.not.undefined;",
    "});",
    ""
  ],
  "dotupGenerateTestFile.template.property": [
    "it('${ClassName}.${PropertyName}', () => {",
    "// Arguments",
    "${Declarations}",
    "",
    "// Property call",
    "${MemberTests}",
    "",
    "// Expect result",
    "expect(${PropertyGetResult}).equals(${PropertySetVariable});",
    "});",
    ""
  ]
}
```

## Release Notes

### 1.0.0

This is just a prototype to see if there is interest in such a tool.

**Please give me feedback!**

## Screenshots

### Project structure

![Project structure](https://raw.githubusercontent.com/dotupNET/dotup-vscode-test-generator-docs/master/images/1_TestGenerator.png)

### Source file

![Source file](https://raw.githubusercontent.com/dotupNET/dotup-vscode-test-generator-docs/master/images/2_TestGenerator.png)

### Generated test file

![Generated test file](https://raw.githubusercontent.com/dotupNET/dotup-vscode-test-generator-docs/master/images/3_TestGenerator.png)

### Generated Header:

![Header](https://raw.githubusercontent.com/dotupNET/dotup-vscode-test-generator-docs/master/images/5_TestGenerator_header.png)

### Generated Method test:

![Method test](https://raw.githubusercontent.com/dotupNET/dotup-vscode-test-generator-docs/master/images/6_TestGenerator_method.png)

### Generated Async method test:

![Async method test](https://raw.githubusercontent.com/dotupNET/dotup-vscode-test-generator-docs/master/images/7_TestGenerator_asyncMethod.png)

### Generated Method test with return value:

![Method test with return value](https://raw.githubusercontent.com/dotupNET/dotup-vscode-test-generator-docs/master/images/8_TestGenerator_function.png)

### Generated Async method test with return value:

![Async method test with return value](https://raw.githubusercontent.com/dotupNET/dotup-vscode-test-generator-docs/master/images/9_TestGenerator_asyncFunction.png)

### Generated Property test:

![Property test](https://raw.githubusercontent.com/dotupNET/dotup-vscode-test-generator-docs/master/images/10_TestGenerator_property.png)
