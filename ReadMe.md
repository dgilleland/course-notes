# About this Repository

This repository is a custom setup of notes published using VuePress. The actual documentation is in the `/docs/` folder on the `master` branch, while the `gh-pages` branch is set as the *GitHub Pages* site for the repository. Normally, I would use some **CI** (*Continuous Integration*) server like TravisCI to do the actual publications. This would free me up to just write content and commit to GitHub, and the content will be "automagically" published on the web for me.

However, this is a private repository, and combined with my being so ~~cheap~~ frugal, I have to actually run a set of commands in the terminal to publish this site. Here are those commands:

```cmd
git worktree prune
del docs\.vuepress\dist -recurse -force
del docs\.vuepress\pub -recurse -force
git worktree prune
vuepress build docs
git worktree add docs\.vuepress\pub gh-pages
xcopy docs\.vuepress\dist\* docs\.vuepress\pub\* /E /Y
xcopy docs\.vuepress\public\* docs\.vuepress\pub\* /E /Y
cd docs\.vuepress\pub
git add .
git commit -m "Publish content updates"
git push --force
cd ..\..\..
```
