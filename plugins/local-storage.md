---
title: Save to LocalStorage
description: Save unsubmitted user form input to localStorage to prevent data loss.
---

# LocalStorage Plugin

:PageToc

Using the `createLocalStoragePlugin` function from `@formkit/addons`, you can easily save unsubmitted user form inputs to localStorage which will be restored on page load. This is great for preventing data loss in the event a user's browser crashes, tab is closed, or other unforeseen issue causes your application to reload before the user can submit their data.

## Installation

To install the localStorage plugin, we need to:

1. import it from `@formkit/addons`.
2. Add it to our FormKit config as a plugin.
3. Add the `use-local-storage` prop to the target form.

The `createLocalStoragePlugin` has two options you can configure:

- `prefix` - The prefix assigned to your localStorage key. Defaults to `formkit`.
- `maxAge` - The time (in milliseconds) that the saved localStorage should be considered valid. Defaults to 1 hour.

```js
// formkit.config.js
import { defaultConfig } from '@formkit/vue'
import { createLocalStoragePlugin } from '@formkit/addons'

const config = defaultConfig({
  plugins: [
    createLocalStoragePlugin({
      // plugin defaults:
      prefix: 'formkit',
      maxAge: 3600000 // 1 hour
    }),
  ],
})

export default config
```

## Usage

To enable saving to localStorage add the `use-local-storage` to your FormKit `form`. The localStorage key will be your provided `prefix` (default is `formkit`) and your form `name` eg. `formkit-contact`.

::Example
---
name: "Save to LocalStorage"
file: [
'/\_content/_examples/local-storage/index.vue',
'/\_content/_examples/local-storage/formkit.config.js'
]
---
::

That's it! Your form data will now be saved on every `commit` event that the `form` receives. It will remain valid until the `maxAge` set in your plugin config, and the localStorage data is cleared when the `submit` event fires on the target form.
