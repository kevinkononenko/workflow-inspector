# Workflow Inspector

A pattern library of the customer workflows behind essential B2B products.

## Local development

```bash
npm install
npm run dev
```

The production build is configured to serve Workflow Inspector from the site root (`/`).

## Adding workflow content

Product timeline content lives in `src/data/productWorkflows.js`. Add each supplied stage under
its product slug and stage id:

```js
jira: {
  define: {
    featureName: "Review the issue",
    description: "One sentence explaining how the user applies it.",
    screenshot: {
      src: "/screenshots/jira-define.png",
      alt: "What the screenshot shows",
      objectPosition: "70% 35%",
      scale: 1.5,
      panX: 0,
      panY: 0,
    },
    article: {
      title: "Knowledge base article title",
      url: "https://example.com/article",
    },
  },
},
```

Store imported screenshots in `src/assets/<product>/` (or URL-served screenshots in
`public/screenshots/`). `objectPosition` selects the focal point and `scale` controls the zoom. A
stage appears in the homepage explorer once every required field is filled in.

### Stage-title standard

Every workflow card title (`featureName`) must be a short, action-oriented phrase that starts with
a clear verb and describes what the user is doing at that stage. Aim for roughly two to six words.
Use `Open a pull request`, `Track the approval`, or `Mark the work item done`—not noun-only labels
such as `Pull request`, `Designated reviewer`, or `Status and Resolution`. The product feature or
object belongs in the phrase, but the user's action is the title's organizing idea.

## Workflow research standard

Every product flow should meet the level of detail established by the Procore purchase-order change
flow: describe one specific, end-to-end job rather than provide a tour of the product. Each of the
eight stages should identify the user's real-world trigger or input, the action they take, the
feature that supports it, the decision or handoff involved, the resulting outcome, and the most
important friction or risk. Include meaningful work that happens away from the screen, such as a
field conversation or approval, when that work is necessary to complete the job.

## Screenshot sourcing standard

Screenshots should make the flow feel like one continuous session in the current product:

- Every time an in-product workflow card is added or substantially revised, search for its
  supporting screenshot in the same work session. A card is not complete until a screenshot has
  been found, checked, stored locally, and connected to the stage—or the search has established
  that no current, trustworthy image is available. Cards marked `outsideProduct` are the explicit
  exception because their visual treatment does not render a product screenshot.
- Start with image search across official product documentation, release notes, product blogs, and
  recent official walkthroughs. Expand to a reputable current secondary source only when the
  official sources do not show the required interface state.
- Before adding the image, verify that it actually shows the feature or evidence named by the
  card, that its interface generation is compatible with the rest of the workflow, and that the
  source page and publication or recording date are known.
- Store the verified image in `src/assets/<product>/`, then add descriptive alt text, a stable
  annotation key, a concise focus label, the source and date credit, and the source-page URL.
- Every screenshot must come from the last four years.
- Within a workflow, prefer one official source set or screenshots captured during the same general
  time period. They should represent the same interface generation and visual design.
- Do not mix screenshots from before and after a major product redesign, even when every image is
  less than four years old. Check release notes and visible interface details before treating a
  help-center image as compatible with the rest of the flow.
- Prefer official documentation, release notes, and recent official product walkthrough videos.
- Use populated examples with realistic names, descriptions, statuses, quantities, and amounts.
  Avoid empty, heavily redacted, or generic setup screens when a detailed example exists.
- Match every image to the stage text and crop it consistently around the evidence that supports
  that stage.
- Record the source and its publication or recording date in the screenshot credit. If a current,
  relevant image cannot be verified, leave the gap visible rather than silently substituting a
  legacy screenshot.

## Feature relationship diagrams

The complete authoring standard—including the object-versus-state decision rules, ERD field
patterns, stage labels, relationship semantics, visual tokens, Eraser JSON examples, and review
checklist—lives in [`diagrams/README.md`](diagrams/README.md).

Every completed workflow includes a wide object-and-state diagram below the workflow map. Keep
product concepts visually dominant, use the eight stage names as small contextual labels, and label
connections with the result one object supplies to the next. Include meaningful feedback loops
instead of forcing every relationship into a straight line.

Give icons only to durable system concepts or objects. States, fields, roles, and user actions belong
inside or alongside the object they affect and do not receive concept icons of their own. Make object
lineage visually explicit: distinguish records created from earlier records, references to existing
product objects, mutations to those objects, and state transitions such as review, rejection,
revision, and approval. The diagram's layout should follow these object relationships rather than
simply repeating the eight stages in chronological order.

Diagram source files live in `diagrams/` and are rendered with Eraser's open-source
`@eraserlabs/diagrams-cli` package. For example, regenerate the Procore diagram with:

```bash
npm run diagram:procore
```

## HyperFrames video

The 29-second whiteboard-style Procore workflow overview and Define example lives in
`videos/eraser-to-problem/`. Its `index.html` composition is the source of truth for the video's
content, timing, layout, and animation. Generated previews and rendered video files should be
treated as outputs, not edited as source.

```bash
npm run video:preview
npm run video:check
npm run video:render
```

HyperFrames requires Node.js 22 or newer and FFmpeg for local MP4 rendering.
