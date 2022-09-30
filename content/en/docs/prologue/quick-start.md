---
title: "Quick Start"
description: "Quick Start creating forms with react-form."
lead: "Quick Start creating forms with react form."
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
images: []
menu:
  docs:
    parent: "prologue"
weight: 110
toc: true
---

## Compatible

- [React](https://reactjs.com/) — ReactJS
- [React Native](https://react-native.org/) — React Native for mobile


## Installation

- Using Yarn
```bash
yarn add @resourge/react-form
```
- Using npm
```bash
npm install @resourge/react-form --save
```

### Schema validation with Yup

{{< alert icon="💡" text="Only needed when using Yup as schema validation" />}}


To simplify the process of converting errors from diferent validation packages like joi, yup, zod, ajv, etc to `useForm` hook lookalike errors, use `setDefaultOnError`. You only need to setup this on the initialization of the application in this case App.tsx.

`setDefaultOnError` will, by default (unless `onError` from Form Options is set), customize the errors to fit `useForm` errors

```javascript
// In App.tsx
import { setDefaultOnError } from '@resourge/react-form'

setDefaultOnError((errors: any) => {
  // Customize errors to fit the model 
  // [{ path, errors }]
  return []
});
```
- Note: We plan to add more default validations in the future. If you have one and want to share, please do and contribute.

- For yup validation, `setFormYupValidation`

```javascript
// In App.tsx
import { setDefaultOnError } from '@resourge/react-form'

setDefaultOnError((errors: any) => {
  // Customize errors to fit the model 
  // [{ path, errors }]
  return []
});
```

#### Usage

```javascript
const {
  form, // Form Data
  touches, isTouched, // Form touches
  errors, isValid, // Form validation
  context, // Context
  triggerChange, reset, merge,
  handleSubmit, field,
  onChange, getValue, changeValue,changeValue, 
  resetTouch,
  getErrors, setError, hasError, 
  watch,
  undo, redo
} = useForm(formData, formOptions)
```

`useForm` is the hook necessary to create forms. Using formData and formOptions, the hook returns an array containing the form state and the form actions.

#### Example

Demonstration of a example of a simple form.

```javascript
import React, { useState } from 'react';
import { useForm } from '@resourge/react-form';

export default function Form() {
  const { 
    isValid,
    field, 
    handleSubmit 
  } = useForm(
    { 
      name: 'Rimuru' 
    }
  )

  const onSubmit = handleSubmit((form) => {
    // Output of form data
    console.log('Form data', form)
  })

  return (
    <form onSubmit={onSubmit}>
      <input { ...field('name') }/>
      <span>
      {
        isValid ? "Valid" : "Invalid" 
      } Form
      </span>
      <button type="submit">
        Save
      </button>
    </form>
  );
}
```

{{< details "Usage of form tag" >}}
Usage of form as wrapper is optional.
{{< /details >}}


## Known Bugs

- Input cursor jumping to end.<br>
Exists a bug in react inputs where using async `onChange` will cause the input cursor to jump to the end. <a href="https://github.com/facebook/react/issues/14904">facebook/react#14904</a>.

To prevent the bug from occurring, `onChange` params needs to be an Event.


