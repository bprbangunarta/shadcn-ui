Install shadcn/typeset in this project.

Typeset is a single stylesheet that styles rendered markdown: wrap the output in a `typeset` container and everything inside (headings, lists, tables, code, blockquotes, math) is styled. Everything outside is untouched.

1. Download https://ui.shadcn.com/typeset.css and save it as typeset.css next to the project's main CSS file (where Tailwind is imported). If the file already exists, replace it with the downloaded copy.

2. Import it in the main CSS file, after the Tailwind import:

@import "./typeset.css";

3. Install the fonts:

npm install @fontsource-variable/geist @fontsource-variable/geist-mono

Then import them in the main CSS file:

/* globals.css */
@import "@fontsource-variable/geist";
@import "@fontsource-variable/geist-mono";

:root {
  --font-geist: 'Geist Variable', sans-serif;
  --font-geist-mono: 'Geist Mono Variable', monospace;
}

4. Add this preset to the main CSS file, after the typeset import. If a class named .typeset-docs already exists, update its values in place. Leave any other typeset-* presets untouched: they are separate surfaces:

.typeset-docs {
  --typeset-font-body: var(--font-geist);
  --typeset-font-heading: var(--font-geist);
  --typeset-font-mono: var(--font-geist-mono);
  --typeset-size: 15px;
  --typeset-leading: 1.75;
  --typeset-flow: 1.25em;
}

5. Do not apply the class anywhere yet. Search the project for surfaces that render markdown or rich content: react-markdown, Streamdown, or MDX components, dangerouslySetInnerHTML with parsed markdown, prose classes, CMS content renderers. Present the candidates you find as a short list and ask the user which surface should use typeset. Then wrap only the surface they pick:

<div className="typeset typeset-docs max-w-[37em]">
  {content}
</div>

If the picked surface already has its own typography (a prose class, styled markdown components), list those styles and let the user decide what to remove before wrapping.

Notes:

- To exclude an embedded component from typeset styles, add the not-typeset class or the data-not-typeset attribute to it.
- Verify on the surface the user picked: headings, lists, tables, and code inside the container should be styled with no classes on the content itself.
- Docs: https://ui.shadcn.com/docs/typeset