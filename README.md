<h1 align="center" width="100%">
  <img src="https://raw.githubusercontent.com/surishortlink/suri/HEAD/logo.png" width="200" alt="Suri" />
</h1>

<h3 align="center" width="100%">
  <i>Your own short links as an easily deployed static site on Vercel</i>
</h3>

You're viewing a template repository tailored for deploying Suri to
[Vercel](https://vercel.com/). Head over to
[the main repository](https://github.com/surishortlink/suri) to learn more about
Suri, including additional deployment options.

## Setup: One Click

[![Deploy to Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fsurishortlink%2Fsuri-deploy-vercel&project-name=suri&repository-name=suri&output-directory=build)

After you hit the above button, Vercel will walk you through the entire process,
from creating a new repository based on this one, to the initial build and
deploy. Everything should be correctly configured and ready to go.

### Auto-Deploy

Any commits to the `main` branch of your new repository will trigger a new build
and deploy. You can change this by going to the "Settings" of your new site and
editing the relevant "Git" options.

### Custom Domain

To use a custom domain, follow Vercel's guide:
[Adding & Configuring a Custom Domain](https://vercel.com/docs/projects/domains/add-a-domain).

## How It Works

### Manage Links

At the heart of Suri is the [`links.json`](src/links.json) file, located in the
`src` directory, where you manage your links. All of the template repositories
include this file seeded with a few examples:

```json
{
  "/": "https://www.youtube.com/watch?v=CsHiG-43Fzg",
  "1": "https://fee.org/articles/the-use-of-knowledge-in-society/",
  "gh": "https://github.com/surishortlink/suri"
}
```

It couldn't be simpler: the key is the "short link" path that gets redirected,
and the value is the target URL. Keys can be as short or as long as you want,
using whatever mixture of characters you want. `/` is a special entry for
redirecting the root path.

### Build Static Site

Suri ships with a `suri` executable file that generates the static site from the
`links.json` file. The static site is output to a directory named `build`.

All of the template repositories are configured with a `build` script that
invokes this executable, making the command you run simple:

```bash
npm run build
```

When you make a change to the `links.json` file, simply re-run this command to
re-generate the static site, which can then be re-deployed. This template
repository is configured to do this automatically.

### Config

Configuration is handled through the [`suri.config.json`](suri.config.json) file
in the root directory. There is only one option at this point:

| Option | Description                                                        | Type    | Default |
| ------ | ------------------------------------------------------------------ | ------- | ------- |
| `js`   | Whether to redirect with JavaScript instead of a `<meta>` refresh. | Boolean | `false` |

### Public Directory

Finally, any files in the `public` directory will be copied over to the `build`
directory without modification when the static site is built. This can be useful
for files like `favicon.ico` or `robots.txt` (that said, Suri provides sensible
defaults for both).
