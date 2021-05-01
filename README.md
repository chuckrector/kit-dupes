# SvelteKit duplication of nested anchors

In both development and preview modes, the content of nested anchors will be duplicated on load. `index.svelte` contains:

```html
SvelteKit <a href="/"><a href="/">test</a></a>
```

After `npm run dev`, you will initially see "SvelteKit test" and a moment later "SvelteKit testtest". Inspecting the document in Chrome reveals:

```html
<div id="svelte">
    "SvelteKit "
    <a href="/">
        <a href="/">test</a>
    </a>
    <a href="/">test</a>
    <-- ... --->
</div>
```

If you fiddle with the contents and add a newline like so

```html
SvelteKit
<a href="/"><a href="/">test</a></a>
```

you may then see "testSvelteKit test". Inspecting the document reveals:

```html
<div id="svelte">
    <a href="/">test</a>
    "SvelteKit "
    <a href="/">
        <a href="/">test</a>
    </a>
    <-- ... --->
</div>
```

In development mode, it does not always happen immediately and sometimes only occurs after repeated edits such as undoing/redoing the newline.