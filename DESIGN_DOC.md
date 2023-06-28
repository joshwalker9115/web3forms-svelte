# Software Design Doc

## Web3Forms-Svelte
June 24, 2023
Joshua Walker - https://github.com/joshwalker9115

---
## Introduction

Web3Forms-Svelte is a svelte component/wrapper for the standard use cases of Web3Forms.

---
## Principles

- Simplicity
The basic use of the form should be as easy as inserting the component. Styling should fall right in line.

- Control
When needed, the component should allow full without jumping through hoops.

- Type Safety
Full TypeScript support.

---
## Design

- Standard Fields - These fields are applied if no default slot is provided:
    - `Name`
    - `Email`
    - `Message`
    - `Submit`
>
- Custom Fields - Just wrap your from in a `svelte:fragment`
- Required Props - The only required prop is the API key `apikey`, available at [Web3Forms](https://web3forms.com/)

- Optional Props
    - Web3Forms-Svelte Specific Customizations
        - `onSuccess`
            - Custom function call on form submission success.
        - `onError`
            - Custom function call on form submission failure.
        - `inputClass`
            - If only using standard fields and you already have a global style class for your inputs, pass it to this prop to apply it to the standard fields.
        - `status`
            - Control over a status message is available via this prop. Without passing anything to this prop it will display "Submitting..." and then standard API response, depending upon success or failure.
        - `disableStatus`
            - If you don't want the status displayed at all, or want to create your own, pass `true` to this prop.
    -  Web3Forms Customizations - [See Docs](https://docs.web3forms.com/getting-started/customizations). Prop names line up with input names from the Web3Forms docs.
        - `subject`
            - The string passed into this prop will be used as the subject line for the delivered email. If you use a custom form that contains an input with `name="subject"`, this property will be ignored.
        - `redirect`
            - Passing a valid absolute URL with `https://` will redirect after a successful form submission.
        - `honeypot`
            - Uses the built in SPAM Protection from Web3Forms by default. Pass `false` to disable it and/or implement your own. See [Web3Forms Docs](https://docs.web3forms.com/getting-started/customizations/spam-protection) for additional info.
        - `replyto`
            - A custom replyto email address can be passed here.
        - `from_name`
            - The default From Name is "Notifications" but you can customize it with this prop.
- Styling
    - `input` will pass a class to all inputs. This is useful if you have a global stylesheet with styling for inputs.
    - Styling is available over all standard fields via `W3F__Inputs`. This can be targeted as a global css class:
        ```
        :global(.W3F__Inputs) {
          display: block;
          margin: 1rem;
        }
        ```
        - If you have other styling local to the parent component you can extend the class with SCSS:
        ```
        <style lang="scss">
          .input {
            display: block;
            margin: 1rem;
          }
          :global(.W3F__Inputs) {
            @extend .input
          }
        </style>
        ```
    - Individual standard fields are targetable via `W3F__[name]`:
        - `W3F__Honeypot` - this will likely never be needed however if you have any clash in your styling with hidden inputs this could be helpful
        - `W3F__Name`
        - `W3F__Email`
        - `W3F__Message`
        - `W3F__Submit`
        - `W3F__Status`
    - Custom Fields can be styled 