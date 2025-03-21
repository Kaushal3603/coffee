<div align="center">

# Coffee &nbsp;☕ <!-- omit from toc -->

— <ins>**Cof**</ins>rame <ins>**F**</ins>ront-<ins>**E**</ins>nd <ins>**E**</ins>ngineer

_Build and iterate on your UI 10x faster with AI - right from your own IDE!_

<p>
<a href="https://github.com/coframe/coffee/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-green.svg" /></a>
<a href="https://github.com/coframe/coffee"><img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/coframe/coffee?style=social" /></a>
</p>
<br />
</div>

https://github.com/Coframe/coframe-public/assets/25165841/b2eb4928-f952-4a9e-93a4-cb1e365eb53e

> Coffee caffeinates your frontend development workflow with AI. This project is intended to be more than just a nice demo, but rather be an ergonomic tool that can write and interact with production-quality code.

- [Features](#features)
- [Try It](#try-it)
- [How It Works](#how-it-works)
- [TODO](#todo)
- [Related](#related)
- [Community](#community)
- [Core Contributors](#core-contributors)
- [License](#license)

## Features

- Works with any React codebase including Next.js, Remix, etc.
- Reliable enough for most standard UI components
- Supports most simple prop types (data, callbacks, etc)
- Uses the same DX for both edit existing components as well as creating new components from scratch
- Generates clean, maintainable code
- This is where the future of AI-assisted code-gen is headed! 🚀

## Try It

No dependencies, no setup.

Just your React webapp normally, and then open another shell in the same directory and run:

```bash
docker run --pull=always -it -e OPENAI_API_KEY=${OPENAI_API_KEY} -v $(pwd):/mount coframe/coffee:latest
```

You can also build the image yourself from the /react directory:

```bash
./dev.sh build
OPENAI_API_KEY=your_api_key ./dev.sh ../path/to/any/frontend/repo/on/machine
```

You can keep an eye on the terminal running the Docker container to see what Coffee is up to. It's fun to see the code being generated!

## How It Works

Coffee uses Docker to make sure that any agentic code it runs is fully isolated. Coffee is currently implemented in Python (but you don't need to touch Python to use Coffee), and the code-generation agent is relatively simple.

When you run Coffee, it will listen for changes to `js/jsx/ts/tsx` files in your source directory, and if it detects a `<Coffee>` JSX component, it will kick off its magic!

```jsx
<Coffee parameter={parameter}>
  Here is where you put your prompt that Coffee will use to generate the first
  version of your desired component. This is the same type of prompt that you'd
  use with any LLM like ChatGPT, so feel free to get creative and apply your
  favorite prompt engineering tricks. Finally, you can also pass in any
  parameters you want from your parent component by simply adding them as
  demonstrated above.
</Coffee>
```

Every time you save your source file, Coffee will look to see if there are any `<Coffee>` components which need brewing (if they're new or if their props or prompt have been updated). For each `<Coffee>` component the agent finds, Coffee will pass your parent component code, any existing child component code, your prompt, and any custom configuration to the OpenAI chat completions API in order to generate a new version of the target component.

> ℹ️ Your application may display an error immediately after saving it the first time as the Coffee component has not been written to it by the Coffee agent yet. This is normal and will go away after the Coffee agent has had time to brew the component.

Iterating on a component after it has been brewed is just as easy:

```jsx
<Coffee parameter={parameter}>
  To edit and update the brewed component, all you need to do is replace the
  prompt with your desired changes. For instance, "make the button background
  darker".
</Coffee>
```

The brewing process is currently a little slow, but we're working on several ways to make it significantly faster.

Finally, once you're happy with your brewed component, you can add a `pour="ComponentName.tsx"` prop to your `<Coffee>` component and save the file, which will automatically replace the `<Coffee>` component with the generated component.

```tsx
export function Example() {
  return (
    <Coffee
      title="Click Me"
      onClick={() => console.log("clicked")}
      pour="MyButton.tsx"
    >
      Whatever you prompted Coffee to generate
    </Coffee>
  );
}
```

In this example, we added a special `pour` prop. When you save this file, Coffee will replace this code with the following:

```tsx
import MyButton from "./MyButton";

export function Example() {
  return <MyButton title="Click Me" onClick={() => console.log("clicked")} />;
}
```

Now you have a fully functional, reusable React component that's ready to use in production.

**The coolest part of Coffee, however, is that you can edit existing React components just as easily as creating new components from scratch.**

https://github.com/Coframe/coframe-public/assets/25165841/3fb67edb-a6a2-4a1c-a48a-00bd74168c1e

Let's say that you want to edit the MyButton (or any other) component. All you need to do is add the `coffee="description of change to make"` prop:

```tsx
export function Example() {
  return (
    <MyButton
      title="Click Me"
      onClick={() => console.log("clicked")}
      coffee="make the button color blue"
    />
  );
}
```

Once you save this file, Coffee will detect this "caffeinated" component and update it for you after it's had time to think and generate it.

You can keep iterating like this forever – you can never run out of Coffee! 😂 Once you're satisfied, just remove the `coffee` prop and you're good to go.

## TODO

- [x] Add basic tests and GitHub CI
- [ ] Run `prettier` on generated code
- [ ] Variety of agents: faster/smarter/cheaper
- [ ] Add visuals and data feedback loop from component to agent (GPT-4V)
- [ ] Support custom prompt
- [ ] Support custom agents
- [ ] Expand support for `coffee.config.json` config
- [ ] Integrate natively with tools like Next.js, webpack, Remix, Prettier, ESlint, etc.
- [ ] Add support for other popular frontend frameworks (Vue, Svelte, etc)

## Related

- [v0](https://v0.dev) - Amazing generative React playground by [Vercel](https://vercel.com)
  - We're hoping they OSS it soon in order to open it up to a wider audience 🥹
  - We were excited to experiment with a DX that was more natively integrated into a frontend developer's existing workflow, so we could better understand the tradeoffs between two approaches.
- [Screenshot to Code](https://github.com/abi/screenshot-to-code) - OSS project showcasing the power of GPT-V for UI generation 🤯
  - One of the first projects to showcase GPT-V's capabilities for UI generation from an image (besides [GDB's timeless GPT-4 announcement](https://www.youtube.com/live/outcGtbnMuQ?feature=shared&t=978), of course!)
- [Draw a UI](https://github.com/SawyerHood/draw-a-ui) - ditto!
- [Cursor](https://cursor.sh/) - AI-native IDE that the Coframe team uses and loves 🥰
  - Coffee can be used in any IDE, but we're huge fans of Cursor and are excited to see what they launch next!
- [Fynix](https://www.fynix.ai/) - Fynix combines real-time AI coding assistance with agent-powered code reviews. Write smarter, faster, and cleaner code.

## Community

Join us on [Discord](https://discord.gg/coframe) for support, to show off what you've brewed, and good vibes in general.

Follow us on [Twitter](https://twitter.com/coframe_ai) for new feature releases, product updates, and other exciting news!

## Core Contributors

https://github.com/Coframe/coframe-public/assets/25165841/2f355984-2c6a-4773-8601-9ff156bbfb0d

If you'd like to be a contributor, just submit a pull request!

⚡ We are also hiring for generalist engineers and AI engineers who are passionate about the future of UX/AI. Coffee is just one of the many exciting things we have brewing. If you want to build this future with us, please shoot us a DM on [Twitter](https://twitter.com/coframe_ai)!

## Local Development

```sh
cd react
pip3 install -r dev_requirements.txt
pytest
```

## License

Apache 2.0 © [Coframe](https://coframe.com)
