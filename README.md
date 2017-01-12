# GoodMeasure-Renderer-Example
Example repo to get your started using the GoodMeasure renderer!


Step 1: Fork this Repo!

Step 2: Connect GoodMeasure's Github bot to this repo (instructions in time).

Step 3: Start editing your site!

Your GoodMeasure rendered site is powered by three folders in this repo: config, partials and templates. Feel free to include anything else in your repo (build tools, etc), anything outside of those folders will be ignore by GoodMeasure.


*Config*

Change the name of your config document from `example.goodmeasure.io.yml` to `yourclientid.goodmeasure.io.yml`

Our config files are in yml, we recommend http://www.yamllint.com/ it check your config files.

Your site config file requires at least a sitemap object. The sitemap object is how you tie paths to templates

```
sitemap:
  404:
    template: 404.html
  /:
    template: home.html
  /*/home:
    template: vertical.html #Supports wildcards!
  /*/reviews:
    template: reviews.html
  /*/compare:
    template: compare.html
  /*/articles:
    template: articles.html #Use the same template for multiple paths! Configure them with forge!
  /*/articles/*:
    template: article.html
```
You can place any other config values you'd like in this file and they will be availabe in your templates under `config`!

**Partials**

GoodMeasure Renderer uses Nunjucks https://mozilla.github.io/nunjucks/ for templating.

Any html file you place in the partials folder will be loaded as a nunjucks partial and can be imported into a template.

**Templates**

A GoodMeasure template is how you integrate your GM Entities into your nunjucks templates. Each section of a template is broken up using `<<--` and `-->>` (Note: anything not between the arrows is render using standard nunjucks).

Example:
```
<<--
dynamic: true
gmRequest:
  type: forge
  blueprint: Meta
  source:
    persistsplit: true
-->>
```

*dynamic*: Whether the renderer should reach out to Goodmeasure each time or cache its original results. When forging and split testing you will always want this to be true.

*gmRequest*: Object describing the GM request to make before rendering the template. See the [blacksmith batch documentation](http://goodmeasure.readthedocs.io/en/latest/blacksmith.html#batching) for full details
