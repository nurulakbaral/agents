# Layered Structure

A guide for structuring component-based architecture in React.js with a clean, consistent flow.

## Styles and Conventions

### Naming Conventions

- File names for components should start with the feature or domain name using a dash separator. For example, given a `user` domain: write `user.tsx` for the main component, or `user-table.tsx` if the user has a table.
- The component names follow PascalCase — `User` and `UserTable` respectively — and their prop types are named `TUserProps` and `TUserTableProps` respectively.


### Component and Types

```tsx
// Native HTML component
import * as React from 'react'

type TComponentNameProps = {} & React.HTMLProps<HTMLDivElement>

export function ComponentName({ ...props }: TComponentNameProps) {
  return (
    <div {...props}>{/* ... */}</div>
  )
}

// Using a UI component library (Mantine UI)
import * as React from 'react'
import { Box, type BoxProps, type ElementProps } from '@mantine/core'

type TComponentNameProps = {} & ElementProps<'div', keyof BoxProps> & BoxProps

export function ComponentName({ ...props }: TComponentNameProps) {
  return (
    <Box component="div" {...props}>{/* ... */}</Box>
  )
}

// Using a UI component library (Ant Design)
import * as React from 'react'
import { Button, type ButtonProps } from 'antd'

type TComponentNameProps = {} & ButtonProps

export function ComponentName({ ...props }: TComponentNameProps) {
  return (
    <Button {...props}>{/* ... */}</Button>
  )
}
```

Guidelines:

- Types should not be exported by default — only export types when they are used outside the module.
- Prefer `type` over `interface` for type definitions.
- Always extend the component's type with the parent component's props. When using a UI component library, extend with the library's props accordingly.
- Type names should start with `T` and end with the `Props` suffix, e.g. `TComponentNameProps`.
- Always use named export function declarations over function expressions.
- Always add `import * as React from 'react'` at the top of the file.
- Pass props to parent components using spread destructuring.
- Always refer to the official docs of whichever UI component library you are using.
