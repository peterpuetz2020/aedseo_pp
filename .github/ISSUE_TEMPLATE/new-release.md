---
name: New release
about: Steps to perform before new release.
title: Prepare for release vX.X.X
labels: documentation
assignees: ''

---

## Replace X.X.X with version of release (<major>.<minor>.<patch>)
## Replace YYY with version type for this release: 'major', 'minor' or 'patch'

Prepare for release:

First create a new branch in terminal:
* [ ] git switch master
* [ ] `git pull`
* [ ] git checkout -b "release-vX.X.X"

Then in R:
* [ ] `usethis::use_version('YYY')`
* [ ] Check [current CRAN check results](https://cran.rstudio.org/web/checks/check_results_aedseo.html)
* [ ] Check if any deprecation processes should be advanced, as described in [Gradual deprecation](https://lifecycle.r-lib.org/articles/communicate.html#gradual-deprecation)
* [ ] [Polish NEWS](https://style.tidyverse.org/news.html#news-release)
* [ ] `usethis::use_github_links()`
* [ ] `urlchecker::url_check()`
* [ ] `devtools::build_readme()`
* [ ] `devtools::check()`
* [ ] Test if works on windows:
     - devtools::build()
     - Upload tar.gz folder to: https://win-builder.r-project.org/upload.aspx
     - Fix things if errors in e-mail
* [ ] tarball <- devtools::build()
* [ ] rcmdcheck::rcmdcheck(tarball, args = c("--as-cran")) <- tests as CRAN
* [ ] Update `cran-comments.md`
* [ ] git commit -am "Prepare release vX.X.X"
* [ ] git push -u origin release-vX.X.X

Submit to CRAN:
* [ ] `devtools::submit_cran()`
* [ ] Approve email

Wait for CRAN to accept.
* [ ] Accepted 🎉 

Update main to new version:
* [ ] git checkout master
* [ ] git pull
* [ ] git merge --no-ff release-vX.X.X -m "Merge release vX.X.X"
* [ ] git tag vX.X.X
* [ ] git push
* [ ] git push --tags

Deploy blogpost:
* [ ] pkgdown::build_site()

Github release:
* [ ] `usethis::use_github_release()`

Change to development version again:
* [ ] `usethis::use_dev_version(push = TRUE)`
* [ ] pkgdown::build_site()
