## $${\color{red}shadcn \ cheat \ sheet}$$

**shadcn/ui** is a collection of **accessible, reusable UI components** built with **React**, **Tailwind CSS**, and **Radix UI**.
Unlike typical libraries, components are **copied into your project**, giving full control over customization.

---

#### 1. Installation

### Create project (example with Next.js)

```bash
npx create-next-app@latest my-app
cd my-app
```

#### Install shadcn

```bash
npx shadcn@latest init
```

Options typically asked:

```
✔ Framework: Next.js
✔ Style: Default
✔ Base color: Slate
✔ CSS variables: Yes
```

---

### 2. Add Components

Install individual components when needed.

```bash
npx shadcn@latest add button
npx shadcn@latest add dialog
npx shadcn@latest add card
```

Generated structure:

```
/components
  /ui
    button.tsx
    dialog.tsx
    card.tsx
```

---

### 3. Basic Usage

#### Button

```tsx
import { Button } from "@/components/ui/button"

export function Example() {
  return <Button>Click me</Button>
}
```

Variants:

```tsx
<Button>Default</Button>
<Button variant="secondary">Secondary</Button>
<Button variant="destructive">Delete</Button>
<Button variant="outline">Outline</Button>
<Button variant="ghost">Ghost</Button>
<Button variant="link">Link</Button>
```

Sizes:

```tsx
<Button size="sm" />
<Button size="lg" />
<Button size="icon" />
```

---

### 4. Card Component

```tsx
import {
  Card,
  CardHeader,
  CardTitle,
  CardContent,
  CardFooter
} from "@/components/ui/card"

<Card>
  <CardHeader>
    <CardTitle>Profile</CardTitle>
  </CardHeader>

  <CardContent>
    Content here
  </CardContent>

  <CardFooter>
    Footer actions
  </CardFooter>
</Card>
```

---

### 5. Dialog (Modal)

```tsx
import {
  Dialog,
  DialogTrigger,
  DialogContent,
  DialogHeader,
  DialogTitle
} from "@/components/ui/dialog"

<Dialog>
  <DialogTrigger>Open</DialogTrigger>

  <DialogContent>
    <DialogHeader>
      <DialogTitle>Edit Profile</DialogTitle>
    </DialogHeader>
  </DialogContent>
</Dialog>
```

---

### 6. Form Example

Often used with **React Hook Form** and **Zod**.

Install:

```bash
npm install react-hook-form zod @hookform/resolvers
```

Example:

```tsx
import { useForm } from "react-hook-form"

const form = useForm()

<form onSubmit={form.handleSubmit(console.log)}>
  <Input {...form.register("email")} />
  <Button type="submit">Submit</Button>
</form>
```

---

### 7. Input Components

### Input

```tsx
import { Input } from "@/components/ui/input"

<Input placeholder="Email" />
```

#### Checkbox

```tsx
import { Checkbox } from "@/components/ui/checkbox"

<Checkbox />
```

#### Select

```tsx
import {
  Select,
  SelectTrigger,
  SelectContent,
  SelectItem,
  SelectValue
} from "@/components/ui/select"

<Select>
  <SelectTrigger>
    <SelectValue placeholder="Select" />
  </SelectTrigger>

  <SelectContent>
    <SelectItem value="a">Option A</SelectItem>
  </SelectContent>
</Select>
```

---

### 8. Layout Helpers

### Separator

```tsx
import { Separator } from "@/components/ui/separator"

<Separator />
```

#### Scroll Area

```tsx
import { ScrollArea } from "@/components/ui/scroll-area"

<ScrollArea className="h-72 w-48">
  Content
</ScrollArea>
```

---

### 9. Toast Notifications

Install:

```bash
npx shadcn@latest add toast
```

Usage:

```tsx
import { useToast } from "@/components/ui/use-toast"

const { toast } = useToast()

toast({
  title: "Saved",
  description: "Your changes were saved."
})
```

---

### 10. Theming

shadcn uses **CSS variables** and **Tailwind**.

Theme variables are defined in:

```
globals.css
```

Example:

```css
:root {
  --primary: 222 47% 11%;
  --background: 0 0% 100%;
}
```

Dark mode example:

```tsx
<html className="dark">
```

---

### 11. Common Components

Popular components available:

```
accordion
alert
alert-dialog
avatar
badge
breadcrumb
button
calendar
card
checkbox
command
dialog
dropdown-menu
hover-card
input
label
menubar
navigation-menu
popover
progress
radio-group
select
sheet
slider
switch
table
tabs
textarea
toast
tooltip
```

Install any with:

```bash
npx shadcn@latest add component-name
```

---

### 12. Utility Helpers

### `cn()` class merge helper

```ts
import { cn } from "@/lib/utils"

<div className={cn("p-4", isActive && "bg-red-500")} />
```

Uses:

* **clsx**
* **tailwind-merge**

---

### 13. Best Practices

- Install **only needed components**
- Modify components directly in project
- Keep `ui` components isolated
- Use **Tailwind for styling**
- Combine with **Radix accessibility**

Typical stack:

```
React
Next.js
Tailwind
shadcn/ui
Radix UI
React Hook Form
Zod
```
