This is the technical documentation of the Concept API.
It contains information about how to get the engine up and running, how to ingest content into it, log user actions, tune the recommendation algorithm, scale, and deploy.

## How this documentation is organized

As the documentation uses Jekyll as a site generator, its structure follows Jekyll's conventions for organizing content. Basically, it consists of static and dynamic content. The static pages are the ones that are not updated regularly such as Home, Roadmap, and Help. The dynamic content are pages written in Markdown format, which you can find in the *_vx_x_x-docs* (x_x_x is the version number of the given release) and *_posts* folders, and which can be changed/updated at any moment. Such pages are the ones from the HowTo's and Release sections.

Jekyll also happens to be the engine behind GitHub Pages, which means we use Jekyll to host our documentation website from the GitHub’s server.

## Adding content

### Add a new page to the documentation

* For each release create a folder named *_vx_x_x-docs*, where <code>x_x_x is</code> the version number of the release
* Add a page(s) in Markdown format to the *_vx_x_x-docs* folder;
* Add a config entry in *_config.yml* and below the *collections* property add folder name indented with 2 spaces like this: 
<pre><code>
collections:
  _vx_x_x-docs:
    output: true
...
</code></pre>
* Add a config entry in *_data/releases.yml*. Keep in mind that in order to preserve the hierarchical structure, each subelement has to be indented with two spaces and no TABs. It's a YAML thing. Example:
<pre><code>
releases:
  "v1_2_0":
    "Getting Started":
      - "quick-start"
      - "installation"
    "HowTo's":
      - "content-based-recommendation"
      - "get-behavioural-recommendations"
      - "advanced-recommendation-parameters"
      - "stop-recommending-content"
      - "uploading-articles"
      - "user-actions"
      - "upgrade-to-a-newer-version"
    "Miscellaneous":
      - "troubleshooting"
      - "faq"
      - "known-issues"
  "v1_1_1":
    "Getting Started":
      - "quick-start"
      - "installation"
</code></pre>

The files described in *releases.yml* must have the same names in the *_vx_x_x-docs* folder.
* The permalink in the Front Matter part of each document (Markdown file) should be like this: *_vx_x_x-docs/file-name*. The category name should match to the one in *releases.yml* file as well;
* If there is an *info*, *note* or *warning* section, you should wrap it inside a div block like this:
<pre><code>
Info badge: &lt;div class="info-badge"&gt;...&lt;/div&gt;
Note badge: &lt;div class="note-badge"&gt;...&lt;/div&gt;
Warning badge: &lt;div class="warning-badge"&gt;...&lt;/div&gt;
</code></pre>

### Add a release note or news

* Copy the release note written in Markdown format from GitHub;
* Add it to *_posts* folder, while respecting the naming convention.

## Test changes

* You need Jekyll installed;
* Go to your local clone of the documentation repo and execute
`jekyll serve`;

* The documentation is available on http://localhost:4000;
* When changing the *.yml* file(s), you need to restart Jekyll;
* All other changes are applied immediately.

## Deploy changes

* Push them to the gh-pages branch;
* Depending from the current context, you should edit the *baseurl* property in *_config.yml*. Example: <code>baseurl: /recommend-pub-docs</code>

## Caveats

### Code blocks

When writing in Markdown, you need to wrap a multi-line code block in `<pre><code>...</code></pre>`, in order to preserve white spaces. Single lines/embedded code snippets can be wrapped in single backticks (`). Everything within the backticks appear as-is, with no other special formatting. For more information, see [Markdown Basics](https://help.github.com/articles/markdown-basics/). 

### Front matter

* Category comes from the *_data/releases.yaml*;
* Permalink is *_vx_x_x-docs/file-name/*.
