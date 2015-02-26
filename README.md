# example-travis_ci-pull_request_review-jscs 

run jscs and pull request review comment

[Actual script for TravisCI](./bin/run-jscs.sh)

```
# .travis.yml
before_script: ./bin/run-jscs.sh

# bin/run-jscs.sh
#!/bin/bash
set -v
if [ -n "${TRAVIS_PULL_REQUEST}" ] && [ "${TRAVIS_PULL_REQUEST}" != "false" ]; then
  gem install --no-document checkstyle_filter-git saddler saddler-reporter-github

  git diff --name-only origin/master \
   | grep -e '\.js$' \
   | xargs ./node_modules/gulp-jscs/node_modules/.bin/jscs \
       --reporter checkstyle \
   | checkstyle_filter-git diff origin/master \
   | saddler report \
      --require saddler/reporter/github \
      --reporter Saddler::Reporter::Github::PullRequestReviewComment
fi

exit 0
```

If you prefer to exec `after_script`, you can set this. see: [Travis CI: Configuring your build](http://docs.travis-ci.com/user/build-configuration/)

## Setting

[Travis CI: Encryption keys](http://docs.travis-ci.com/user/encryption-keys/)

```
$ gem install travis
$ travis encrypt -r <owner_name>/<repos_name> "GITHUB_ACCESS_TOKEN=<github_token>"
```


## Contributing

In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [gulp](http://gulpjs.com/).


## License

Copyright (c) 2015 sanemat. Licensed under the MIT license.



[npm-url]: https://npmjs.org/package/example-travis-ci-pull-request-review-jscs
[npm-image]: https://badge.fury.io/js/example-travis-ci-pull-request-review-jscs.svg
[travis-url]: https://travis-ci.org/sanemat/example-travis-ci-pull-request-review-jscs
[travis-image]: https://travis-ci.org/sanemat/example-travis-ci-pull-request-review-jscs.svg?branch=master
[daviddm-url]: https://david-dm.org/sanemat/example-travis-ci-pull-request-review-jscs.svg?theme=shields.io
[daviddm-image]: https://david-dm.org/sanemat/example-travis-ci-pull-request-review-jscs
[coveralls-url]: https://coveralls.io/r/sanemat/example-travis-ci-pull-request-review-jscs
[coveralls-image]: https://coveralls.io/repos/sanemat/example-travis-ci-pull-request-review-jscs/badge.png
