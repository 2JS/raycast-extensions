# Actions

Our API includes a few built-in actions that can be used for common interactions, such as opening a link or copying some content to the clipboard. By using them, you make sure to follow our human interface guidelines. If you need something custom, use the [`Action`](#action) component. All built-in actions are just abstractions on top of it.

## API Reference

### Action

A context-specific action that can be performed by the user.

Assign keyboard shortcuts to items to make it easier for users to perform frequently used actions.

#### Example

```typescript
import { ActionPanel, Action, List } from "@raycast/api";

export default function Command() {
  return (
    <List navigationTitle="Open Pull Requests">
      <List.Item
        title="Docs: Update API Reference"
        subtitle="#1"
        actions={
          <ActionPanel title="#1 in raycast/extensions">
            <Action.OpenInBrowser url="https://github.com/raycast/extensions/pull/1" />
            <Action.CopyToClipboard
              title="Copy Pull Request Number"
              content="#1"
            />
            <Action
              title="Close Pull Request"
              onAction={() => console.log("Close PR #1")}
            />
          </ActionPanel>
        }
      />
    </List>
  );
}
```

#### Props

| Prop | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| title<mark style="color:red;">*</mark> | The title displayed for the item. | <code>string</code> | - |
| icon | The icon displayed for the action. | <code>Image.ImageLike</code> | - |
| shortcut | The keyboard shortcut for the item. | <code>Keyboard.Shortcut</code> | - |
| onAction | Callback that is triggered when the item is selected. | <code>() => void</code> | - |

### Action.CopyToClipboard

Action that copies the content to the clipboard.

The main window is closed, and a HUD is shown after the content was copied to the clipboard.

#### Example

```typescript
import { ActionPanel, Action, Detail } from "@raycast/api";

export default function Command() {
  return (
    <Detail
      markdown="Press `⌘ + .` and share some love."
      actions={
        <ActionPanel>
          <Action.CopyToClipboard
            content="I ❤️ Raycast"
            shortcut={{ modifiers: ["cmd"], key: "." }}
          />
        </ActionPanel>
      }
    />
  );
}
```

#### Props

| Prop | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| content<mark style="color:red;">*</mark> | The contents that will be written to the clipboard as string. | <code>string</code> or <code>number</code> | - |
| icon | A optional icon displayed for the item. | <code>Image.ImageLike</code> | [Icon.Clipboard](icons-and-images.md#icon) |
| shortcut | The keyboard shortcut for the action. | <code>Keyboard.Shortcut</code> | - |
| title | An optional title for the action. | <code>string</code> | `"Copy to Clipboard"` |
| onCopy | Callback when the content was copied to clipboard. | <code>(content: string \| number) => void</code> | - |

### Action.Open

An action to open a file or folder with a specific application, just as if you had double-clicked the
file's icon.

The main window is closed after the file is opened.

#### Example

```typescript
import { ActionPanel, Detail, Action } from "@raycast/api";

export default function Command() {
  return (
    <Detail
      markdown="Check out your extension code."
      actions={
        <ActionPanel>
          <Action.Open title="Open Folder" target={__dirname} />
        </ActionPanel>
      }
    />
  );
}
```

#### Props

| Prop | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| target<mark style="color:red;">*</mark> | The file, folder or URL to open. | <code>string</code> | - |
| title<mark style="color:red;">*</mark> | The title for the action. | <code>string</code> | - |
| application | The application name to use for opening the file. | <code>string</code> or <code>Application</code> | - |
| icon | The icon displayed for the action. | <code>Image.ImageLike</code> | [Icon.Finder](icons-and-images.md#icon) |
| shortcut | The keyboard shortcut for the action. | <code>Keyboard.Shortcut</code> | - |
| onOpen | Callback when the file or folder was opened. | <code>(target: string) => void</code> | - |

### Action.OpenInBrowser

Action that opens a URL in the default browser.

The main window is closed after the URL is opened in the browser.

#### Example

```typescript
import { ActionPanel, Detail, Action } from "@raycast/api";

export default function Command() {
  return (
    <Detail
      markdown="Join the gang!"
      actions={
        <ActionPanel>
          <Action.OpenInBrowser url="https://raycast.com/jobs" />
        </ActionPanel>
      }
    />
  );
}
```

#### Props

| Prop | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| url<mark style="color:red;">*</mark> | The URL to open. | <code>string</code> | - |
| icon | The icon displayed for the action. | <code>Image.ImageLike</code> | [Icon.Globe](icons-and-images.md#icon) |
| shortcut | The optional keyboard shortcut for the menu item | <code>Keyboard.Shortcut</code> | - |
| title | An optional title for the action. | <code>string</code> | `"Open in Browser"` |
| onOpen | Callback when the URL was opened in the browser. | <code>(url: string) => void</code> | - |

### Action.OpenWith

Action that opens a file or folder with a specific application.

The action opens a sub-menu with all applications that can open the file or folder.
The main window is closed after the file is opened in the specified application.

#### Example

```typescript
import { ActionPanel, Detail, Action } from "@raycast/api";
import { homedir } from "os";

const DESKTOP_DIR = `${homedir()}/Desktop`;

export default function Command() {
  return (
    <Detail
      markdown="What do you want to use to open your desktop with?"
      actions={
        <ActionPanel>
          <Action.OpenWith path={DESKTOP_DIR} />
        </ActionPanel>
      }
    />
  );
}
```

#### Props

| Prop | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| path<mark style="color:red;">*</mark> | The path to open. | <code>string</code> | - |
| icon | The icon displayed for the action. | <code>Image.ImageLike</code> | [Icon.Upload](icons-and-images.md#icon) |
| shortcut | The keyboard shortcut for the action. | <code>Keyboard.Shortcut</code> | - |
| title | The title for the action. | <code>string</code> | `"Open With"` |
| onOpen | Callback when the file or folder was opened. | <code>(path: string) => void</code> | - |

### Action.Paste

Action that pastes the content to the front-most applications.

The main window is closed after the content is pasted to the front-most application.

#### Example

```typescript
import { ActionPanel, Detail, Action } from "@raycast/api";

export default function Command() {
  return (
    <Detail
      markdown="Let us know what you think about the Raycast API?"
      actions={
        <ActionPanel>
          <Action.Paste content="api@raycast.com" />
        </ActionPanel>
      }
    />
  );
}
```

#### Props

| Prop | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| content<mark style="color:red;">*</mark> | The contents that will be written to the clipboard as string. | <code>string</code> or <code>number</code> | - |
| icon | The icon displayed for the action. | <code>Image.ImageLike</code> | [Icon.Clipboard](icons-and-images.md#icon) |
| shortcut | The keyboard shortcut for the action. | <code>Keyboard.Shortcut</code> | - |
| title | An optional title for the action. | <code>string</code> | `"Paste in Active app"` |
| onPaste | Callback when the content was pasted into the front-most application. | <code>(content: string \| number) => void</code> | - |

### Action.Push

Action that pushes a new view to the navigation stack.

#### Example

```typescript
import { ActionPanel, Detail, Action } from "@raycast/api";

function Ping() {
  return (
    <Detail
      markdown="Ping"
      actions={
        <ActionPanel>
          <Action.Push title="Push Pong" target={<Pong />} />
        </ActionPanel>
      }
    />
  );
}

function Pong() {
  return <Detail markdown="Pong" />;
}

export default function Command() {
  return <Ping />;
}
```

#### Props

| Prop | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| target<mark style="color:red;">*</mark> | The target view that will be pushed to the navigation stack. | <code>React.ReactNode</code> | - |
| title<mark style="color:red;">*</mark> | The title displayed for the item. | <code>string</code> | - |
| icon | The icon displayed for the action. | <code>Image.ImageLike</code> | - |
| shortcut | The keyboard shortcut for the action. | <code>Keyboard.Shortcut</code> | - |
| onPush | Callback when the target view was pushed. | <code>() => void</code> | - |

### Action.ShowInFinder

Action that shows a file or folder in the Finder.

The main window is closed after the file or folder is revealed in the Finder.

#### Example

```typescript
import { ActionPanel, Detail, Action } from "@raycast/api";
import { homedir } from "os";

const DOWNLOADS_DIR = `${homedir()}/Downloads`;

export default function Command() {
  return (
    <Detail
      markdown="Are your downloads pilling up again?"
      actions={
        <ActionPanel>
          <Action.ShowInFinder path={DOWNLOADS_DIR} />
        </ActionPanel>
      }
    />
  );
}
```

#### Props

| Prop | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| path<mark style="color:red;">*</mark> | The path to open. | <code>[PathLike](../utilities.md#pathlike)</code> | - |
| icon | A optional icon displayed for the item. | <code>Image.ImageLike</code> | [Icon.Finder](icons-and-images.md#icon) |
| shortcut | The keyboard shortcut for the action. | <code>Keyboard.Shortcut</code> | - |
| title | An optional title for the action. | <code>string</code> | `"Show in Finder"` |
| onShow | Callback when the file or folder was shown in the Finder. | <code>(path: [PathLike](../utilities.md#pathlike)) => void</code> | - |

### Action.SubmitForm

Action that adds a submit handler for capturing form values.

#### Example

```typescript
import { ActionPanel, Form, Action } from "@raycast/api";

export default function Command() {
  return (
    <Form
      actions={
        <ActionPanel>
          <Action.SubmitForm
            title="Submit Answer"
            onSubmit={(values) => console.log(values)}
          />
        </ActionPanel>
      }
    >
      <Form.Checkbox id="answer" label="Are you happy?" defaultValue={true} />
    </Form>
  );
}
```

#### Props

| Prop | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| icon | The icon displayed for the action. | <code>Image.ImageLike</code> | - |
| shortcut | The keyboard shortcut for the action. | <code>Keyboard.Shortcut</code> | - |
| title | The title displayed for the item. | <code>string</code> | `"Submit Form"` |
| onSubmit | Callback that is triggered when the submit was submitted. Use the handler to perform custom validation logic and call other Raycast API methods. The handler receives a the values object containing the user input. | <code>(input: Form.Values) => void</code> | - |

### Action.Trash

Action that moves a file or folder to the Trash.

#### Example

```typescript
import { ActionPanel, Detail, Action } from "@raycast/api";
import { homedir } from "os";

const FILE = `${homedir()}/Downloads/get-rid-of-me.txt`;

export default function Command() {
  return (
    <Detail
      markdown="Some spring cleaning?"
      actions={
        <ActionPanel>
          <Action.Trash paths={FILE} />
        </ActionPanel>
      }
    />
  );
}
```

#### Props

| Prop | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| paths<mark style="color:red;">*</mark> | The item or items to move to the trash. | <code>[PathLike](../utilities.md#pathlike)</code> or <code>[PathLike](../utilities.md#pathlike)[]</code> | - |
| icon | A optional icon displayed for the action. | <code>Image.ImageLike</code> | [Icon.Trash](icons-and-images.md#icon) |
| shortcut | The optional keyboard shortcut for the action. | <code>Keyboard.Shortcut</code> | - |
| title | An optional title for the action. | <code>string</code> | `"Move to Trash"` |
| onTrash | Callback when all items were moved to the trash. | <code>(paths: [PathLike](../utilities.md#pathlike) \| [PathLike](../utilities.md#pathlike)[]) => void</code> | - |

### Action.CreateSnippet

Action that navigates to the the Create Snippet command with some or all of the fields prefilled.

#### Example

```typescript
import { ActionPanel, Detail, Action } from "@raycast/api";

export default function Command() {
  return (
    <Detail
      markdown="Test out snippet creation"
      actions={
        <ActionPanel>
          <Action.CreateSnippet snippet={{ text: "DE75512108001245126199" }} />
        </ActionPanel>
      }
    />
  );
}
```

#### Props

| Prop | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| snippet<mark style="color:red;">*</mark> |  | <code>Snippet</code> | - |
| icon | A optional icon displayed for the item. See [Image.ImageLike](icons-and-images.md#image.imagelike) for the supported formats and types. | <code>Image.ImageLike</code> | - |
| shortcut | The keyboard shortcut for the action. | <code>Keyboard.Shortcut</code> | - |
| title | An optional title for the action. | <code>string</code> | - |

### Action.CreateQuicklink

Action that navigates to the the Create Quicklink command with some or all of the fields prefilled.

#### Example

```typescript
import { ActionPanel, Detail, Action } from "@raycast/api";

export default function Command() {
  return (
    <Detail
      markdown="Test out quicklink creation"
      actions={
        <ActionPanel>
          <Action.CreateQuicklink
            quicklink={{ link: "https://duckduckgo.com/?q={Query}" }}
          />
        </ActionPanel>
      }
    />
  );
}
```

#### Props

| Prop | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| quicklink<mark style="color:red;">*</mark> | The [Quicklink](actions.md#quicklink) to create. | <code>Quicklink</code> | - |
| icon | A optional icon displayed for the item. See [Image.ImageLike](icons-and-images.md#image.imagelike) for the supported formats and types. | <code>Image.ImageLike</code> | - |
| shortcut | The keyboard shortcut for the action. | <code>Keyboard.Shortcut</code> | - |
| title | An optional title for the action. | <code>string</code> | - |

## Types

### Snippet

#### Properties

| Property | Description | Type |
| :--- | :--- | :--- |
| text<mark style="color:red;">*</mark> | The snippet contents. | <code>string</code> |
| keyword | The keyword to trigger the snippet. | <code>string</code> |
| name | The snippet name. | <code>string</code> |

### Quicklink

#### Properties

| Property | Description | Type |
| :--- | :--- | :--- |
| link<mark style="color:red;">*</mark> | The URL or file path, optionally including placeholders such as in "https://google.com/search?q=\{Query\}" | <code>string</code> |
| application | The application that the quicklink should be opened in. | <code>string</code> or <code>Application</code> |
| name | The quicklink name | <code>string</code> |
