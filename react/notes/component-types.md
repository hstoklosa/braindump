# [<span style="font-size:0.65em;vertical-align: 13%;">🔗</span> React.ReactNode vs JSX.Element vs React.ReactElement](https://www.totaltypescript.com/jsx-element-vs-react-reactnode)

## TLDR

`JSX.Element` and `React.ReactElement` are practically the same type and both represent whatever the JSX expression creates.

```tsx
const node: JSX.Element <-> React.ReactElement = <div />
```

`React.ReactNode` is a broader type that can represent outputs of JSX expressions, strings, numbers, undefined, and so on.

```tsx
const node: React.ReactNode = <div />;

const node2: React.ReactNode = "hello world";

const node3: React.ReactNode = 123;

const node4: React.ReactNode = undefined;

const node5: React.ReactNode = null;
```

In everyday use, consider the `React.ReactNode` type.

## Full Explanation

**_The stumbling block when adding React support:_** JSX's syntax doesnt exist in JS, so the TS team had to build it into the compiler.

### JSX.Element

JSX is a _global namespace_ that can contain types with `Element` being one of them.

If React's type definitions define `JSX.Element`, then it will be picked up by TS.

```tsx
// Puts it in the global scope
declare global {
  // Puts it in the JSX namespace
  namespace JSX {
    // Defines the Element interface
    interface Element extends React.ReactElement<any, any> {}
  }
}
```

Think of `JSX.Element` as representing the type of the thing that calling a JSX expression creates.

### What is JSX.Element used for?

For example, typing the `children` property of a component.

```tsx
const Component = ({ children }: { children: JSX.Element }) => {
  return <div>{children}</div>;
};
```

However, issues start to arise when you e.g., want to pass a string instead of the JSX.Element.

```tsx
// 'Component' components don't accept text as child elements.
// Text in JSX has the type 'string', but
// the expected type of 'children' is 'Element'.
<Component>hello world</Component>
```

This is valid in React, but TS complains about the `Component` only accepting `JSX.Element` as children.

Hence the need for `React.ReactNode`.

### React.ReactNode

It's a type that represents everything React can render.

```tsx
declare namespace React {
  type ReactNode =
    | ReactElement
    | string
    | number
    | ReactFragment
    | ReactPortal
    | boolean
    | null
    | undefined;
}
```

It can be used to type the `children` prop of a component.

```tsx
const Component = ({ children }: { children: React.ReactNode }) => {
  return <div>{children}</div>;
};

...

<Component>hello world</Component>
<Component>{123}</Component>
<Component>{undefined}</Component>
<Component>
  <div>Hello world</div>
</Component>
```

### When shouldn't you use React.ReactNode?

Before TS 5.1 -> you can't use `React.ReactNode` in 1 specific case i.e., typing the return type of a functional component.

```tsx
const Component = (): React.ReactNode => {
  return <div>Hello world</div>;
};
```

TypeScript will complain with an error once we try using the component.

> _**"Component' cannot be used as a JSX component. Its return type 'ReactNode' is not a valid JSX element".**_

This is occurring because TS uses the definition of `JSX.Element` to check if something can be rendered as JSX.

`React.ReactNode` contains other things that aren't JSX, so it can't be used as a return type for a component.

However, since TypeScript 5.1 this is no longer an issue due to the changes that improved the way TS infers types from React components.

## React.ReactElement

A type defined in such way to represent the object representation of the element you're rendering.

```tsx
interface ReactElement<P, T extends string | JSXElementConstructor<any>> {
  type: T;
  props: P;
  key: Key | null;
}
```

Printng an element will output an object with the properties shown above.

```tsx
/*
 *    {
 *      type: 'div',
 *      props: {
 *        children: []
 *      },
 *      key: null
 *   }
 */
console.log(<div />);
```

It can be used anywhere you'd type `JSX.Element`.

```tsx
const Component = (): React.ReactElement => {
  return <div>Hello world</div>;
};
```

But, it also breaks when you attempt to pass in a string, number, or undefined to the return value.

> Type 'string' is not assignable to type 'ReactElement<any, string | JSXElementConstructor<any>>'.

```tsx
const Component = (): React.ReactElement => {
  return "123";
};
```

Therefore, we can conclude that `React.ReactElement` and `JSX.Element` are pretty much the same thing.

## Summary

The `JSX.Element` and `React.ReactElement` types are used internally by TypeScript to represent the return type of JSX expressions, hence they should be avoided.

Instead, use `React.ReactNode` to type the children of your components.
