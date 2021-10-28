---
id: bqE8D
name: How Does The /desktop Site Work?
file_version: 1.0.2
app_version: 0.6.3-1
file_blobs:
  docusaurus.config.js: c13ae5a0e2b808d763ea63d90562cce49866fbbe
  sidebarsDesktop.js: e452eb1909762d55f5af6db2a911a3c7aec04887
---

A Short Bit Of Context
----------------------

Swimm didn't have any kind of documentation site until mid-2021, and the first documentation site came into existence after plans to build in-app documentation on the desktop version were abandoned due to complexities.

When the in-app docs were being created, they were organized like how patches used to be staged so that they could be applied in the correct order, e.g.:

```
00-first-patch.txt
01_second-patch.txt
03_third-patch.txt
...
```

This let scripts scrape the output of `ls` or `dir` in any given directory and understand the order that the patches needed to be applied.

When the project was abandoned, we took the content that had been created and launched it using [our Docusaurus demo template](https://github.com/swimmio/docusaurus-template). Since the way that the content was organized lent well to the default (automatic) way that Docusaurus orders content, it was a perfect fit. It was available for a while at docs.swimm.live.

However, development shifted to the Web app being the primary feature driver, so upon launching, a whole new documentation site was needed. While the desktop and web app share many common features, the way that people interact with them are increasingly different as the web app evolves. So, we relaunched with all new content on docs. swimm.io, and imported the existing desktop app documentation to a separate instance of the docs plugin found in `📄 desktop`. We're in the process of setting up redirects to catch anyone that saved the old docs.swimm.live links.

**Nothing links to docs.swimm.io/desktop from our end except for a link that ships in the desktop app.** While we're going to continue to support the desktop app for those that simply can't use the web version, feature development is happening on the web right now, so we don't want to offer the desktop unless the user just can't use the web app.

How Is It Separated?
--------------------

We run [multiple instances of the docs plugin](https://docusaurus.io/docs/docs-multi-instance) so they have separate directories and navigation. The site map still picks up all of the content.

<br/>

You can run as many parallel documentation areas as you want with the content plugin, just define an instance of it with unique name, path, base path and sidebar configuration files as needed.

**Note that images for the** `/desktop` **route come from** `/img/desktop/` **and not** `/img`.
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 docusaurus.config.js
```javascript
⬜ 62             // When applying `zh` in language, please install `nodejieba` in your project.
⬜ 63           },
⬜ 64         ],
🟩 65         [
🟩 66           '@docusaurus/plugin-content-docs',
🟩 67           {
🟩 68             id: 'desktop',
🟩 69             path: 'desktop',
🟩 70             routeBasePath: 'desktop',
🟩 71             sidebarPath: require.resolve('./sidebarsDesktop.js'),
🟩 72           },
🟩 73         ],
⬜ 74       ],
⬜ 75       themeConfig:
⬜ 76         /** @type {import('@docusaurus/preset-classic').ThemeConfig} */
```

<br/>

For the sidebar, we just use the default, however we can change this as-needed just like the main sidebar.
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 sidebarsDesktop.js
```javascript
🟩 1      module.exports = {
🟩 2        tutorialSidebar: [{type: 'autogenerated', dirName: '.'}],
🟩 3      };
🟩 4      
```

<br/>

What Else Needs Done There?
---------------------------

A laundry list of things. The document paths / names need to be normalized like the main site, the files need to be saved with `.mdx` extensions, and ordering is going to happen in the metadata at the top of the doc along with `_category_.json` files like the main site works. There's also video tutorials that could probably be shared between the two.

Other things like sharing a common definition for the CI integrations and such are planned for the next cool down cycle.

<br/>

This file was generated by Swimm. [Click here to view it in the app](https://app.swimm.io/#/repos/Z2l0aHViJTNBJTNBZG9jcy5zd2ltbS5pbyUzQSUzQXN3aW1taW8=/docs/bqE8D).