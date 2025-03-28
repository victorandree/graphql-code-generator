> [!IMPORTANT]
> This is an unsupported fork to make the plugin work with new versions of Next.js and "use client" directives. Use at your own peril.
>
> This version is 0.7.0. It's built with `swc_core` 16.2.2. To understand if this version is compatible with your project/runtime, check <https://plugins.swc.rs/versions/range>.
>
> @victorandree maintains this fork and releases new versions when I find it useful for myself. I typically bump `swc_core` in Cargo.toml, build the plugin and try it out with a sample Next.js project before releasing. I don't provide any support for other users.

# `@victorandree/graphql-codegen-client-preset-swc-plugin`

When using the [`@graphql-codegen/client-preset`](https://the-guild.dev/graphql/codegen/plugins/presets/preset-client) on large scale projects might want to enable code splitting or tree shaking on the `client-preset` generated files. This is because instead of using the map which contains all GraphQL operations in the project, we can use the specific generated document types.

This plugin works for [SWC](https://swc.rs) only.

### Installation

```bash
yarn add -D @victorandree/graphql-codegen-client-preset-swc-plugin
```

### Usage

You will need to provide the `artifactDirectory` path that should be the same as the one configured in your `codegen.ts`

#### Vite

```ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react-swc'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [
    react({
      plugins: [
        ['@victorandree/graphql-codegen-client-preset-swc-plugin', { artifactDirectory: './src/gql', gqlTagName: 'graphql' }]
      ]
    })
  ]
})
```

#### Next.js

```ts
const nextConfig = {
  // ...
  experimental: {
    swcPlugins: [
      ['@victorandree/graphql-codegen-client-preset-swc-plugin', { artifactDirectory: './src/gql', gqlTagName: 'graphql' }]
    ]
  }
}
```

#### `.swcrc`

```json5
{
  // ...
  jsc: {
    // ...
    experimental: {
      plugins: [
        ['@victorandree/graphql-codegen-client-preset-swc-plugin', { artifactDirectory: './src/gql', gqlTagName: 'graphql' }]
      ]
    }
  }
}
```

### Release

To publish a new version ensure you have done the following:

- Update the version in `package.json`
- Update the `CHANGELOG.md` with the new version and changes
- Commit the changes
- From GitHub Actions, run the `Rust plugin` workflow
