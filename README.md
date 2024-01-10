# wiki

My personal wiki. Built using [Jekyll](https://jekyllrb.com/). Search implemented using [Pagefind](https://pagefind.app/). Hosted using [GitHub Pages](https://pages.github.com/). Favicon by [@batgirlodessa](https://twitter.com/batgirlodessa).

## Developing

### Build

```sh
bundle exec jekyll build
npx -y pagefind --site ./_site
```

### Test

```sh
bundle exec jekyll serve
```

The search bar will not be available when testing this way.

