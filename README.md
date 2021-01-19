# Stylex

NOTE: Sylex will be released on February 1, 2021. Give this repo a star!

See Facebook React conf video for about Stylex: [Click here](https://youtu.be/9JZHodNR184?t=229)

## Join Stylex Community (Facebook group)
Visit [this link](https://www.facebook.com/groups/713597106002279) to join Stylex community.

## Installation (Not ready yet)

Yarn users:
```bash
yarn add @ladifire-opensource/stylex
```

Npm users:
```bash
npm install @ladifire-opensource/stylex
```

The second step is depending on what bundler you use, for webpack you 
need to install a webpack plugin

```bash
yarn add @ladifire-opensource/stylex-webpack-plugin
```

## How to use stylex?

There're some methods you can you with stylex:

### Create new stylex object ```(stylex.create)```

This method will create a new stylex object:

```js
import stylex from "@ladifire-opensource/stylex";

const styles = stylex.create({
  root: {
    fontWeight: 700,
    color: "blue"
  },
  button: {
    borderRadius: 8,
  },
});
```

Then we can use as:

```js
<div className={stylex(styles.root)}>
  Component
</div>
```

The arguments of ```stylex(...args)``` can be separated by comma:

```js
<div className={stylex(styles.root, styles.button)}>
  Component
</div>
```

or as an array:

```js
<div className={stylex([styles.root, styles.button])}>
  Component
</div>
```

### Dedupe stylex objects ```(stylex.dedupe)```

This method will dedupe (override) duplicate style properties:

```js
<div
    className={stylex.dedupe(
      {
        color: "var(--primary-text)",
      },
      isError ? {
        color: "var(--negative)"
      } : null,
    )}
  >
    Dedupe
</div>
```

### Create a keyframes animation name ```(stylex.keyframes)```

```js
let j = stylex.create({
  dark: {
    backgroundColor: "var(--placeholder-icon)"
  },
  paused: {
    animationPlayState: "paused"
  },
  root: {
    animationDirection: "alternate",
    animationDuration: "1s",
    animationIterationCount: "infinite",
    animationName: stylex.keyframes({
      '0%': {
        opacity: 0.25,
      },
      '100%': {
        opacity: 1,
      },
    }),
    animationTimingFunction: "steps(10,end)",
    backgroundColor: "var(--wash)",
    opacity: 0.25
  }
});
```

### Compose (merge) stylex objects ```(stylex.compose)```

```js
const s = stylex.compose(
  {
    color: "red",
    backgroundColor: "blue"
  },
  {
    backgroundColor: "white"
  },
);
```

The above code will transformed to:
```js
const s = {
    color: "a512sdfe5", // red
    backgroundColor: "wer115asse" // white
}
```

#### Quick uses
*Describe some common static methods for quick uses, eg: stylex.absolute, ...*

### Plugin options

#### Inject css to compiled js
*Describe how to setup stylex to inject css to compiled js*

#### Separate css into .css files
*Describe how to setup stylex to separate css into reference links*

### Babel

### SSR support

### Others 

#### Typescript support
*Describe how to use stylex with typescript support*

#### Pass stylex through props (Reactjs)

If you using Reactjs, consider to use **xstyle** props to pass some stylex class from
parent to child. Let's see bellow example:

```js
import * as React from "react";
import stylex from "@ladifire-opensource/stylex";
import ChildComponent from "./path/to/child";

type Style = 
    | "root";

const styles = stylex.create({
    root: {
        color: "red"
    },
});

const Parent = () => {
    return (
        <ChildComponent
            xstyle={styles.root}
            //...otherProps
        />
    );
}
```

The ```xstyle``` prop is a good method because it helps to combine style props under one namespace
and doesn't populate the global orios environment and it looks similar to the goal of
sx prop.

Then in your child component you can use ```xstyle``` props as:

```js
import * as React from "react";

import stylex from "@ladifire-opensource/stylex";

const styles = stylex.create({
  root: {
    backgroundColor: "red"
  },
});

const ChildComponent = (props) => {
  const {
    xstyle,
  } = props;
  
  return (
    <div className={stylex(styles.root, xstyle)}>
      Child
    </div>
  );
};
```

#### Theming with stylex

We're working to bring theming to stylex, through the package ```stylex-theme```. It's
coming soon!

## Thanks to

* I'd like to send a big thanks to: johanholmerin for style9 (an other stylex cover)
* I'd like to thanks Facebook very much (most of javascript code in stylex is re-write from built code of Facebook)

## Contributing

Contributions are always welcome, no matter how large or small!

#### Setup

Fork the `stylex` repository to your GitHub Account.

Then, run: ```yarn install```

To see reactjs demo, cd to ```stylex-reactjs-examples``` and following steps in
README.md to run Reactjs demo

### License

Stylex is [MIT licensed](./LICENSE).
