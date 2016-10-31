extends: default.liquid

title: |
  Automatic testing and coverage in NodeJS with Mocha, Istanbul, TravisCI,
  Coveralls, and Yarn.
date: 29 October 2016 17:15:00 -0700
path: /:year/:month/:day/automatic-tests-coverage-nodejs-mocha-istanbul-travisci-coveralls-yarn
---

## Tests, tests, gotta have tests
Here&rsquo;s a confession and possible hot take: I&rsquo;m skeptical of TDD,
or test driven development.

Maybe I&rsquo;ve never done it correctly, maybe I&rsquo;ve never been bitten
by a bug that a test would have caught, or shit, maybe I&rsquo;m just lazy,
I&rsquo;m not exactly sure. But at the end of the day, I write the tests and who
tests the tests? That is a different blog post altogether, though.

However! In the spirit of learning new things and adding to the toolbox, I have
been trying to embrace better testing. Especially on anything I may consider
open sourcing and releasing to the public.

## Let&rsquo;s start with Mocha and basic testing

Getting started with Mocha is pretty quick. Normally in a post like this, I
might leave the installing and setup as an exercise to the reader, but since I
am using [Yarn](https://yarnpkg.com), I wanted to write a bit more.

If you haven&rsquo;t used it yet, [Yarn](https://yarnpkg.com) is a new package
and dependency manager for NodeJS. Why you would or wouldn&rsquo;t use Yarn
is another post as well. But I&rsquo;ve been trying it out and really enjoy it.

So, to install Mocha:

    yarn add --dev mocha

One of the beautiful parts of Yarn, is it traverses the `node_modules` directory
by default. So, you can simply run:

    yarn run mocha

You can do this with npm by adding mocha to your scripts but this is one less
step needed. Pretty cool!

I do like adding a more semantic `test` alias that calls `mocha` to my scripts
list though.

    scripts: {
      "test": "mocha"
    }

Now this is where I&rsquo;ll leave learning Mocha up to the reader. 😀 

## Adding test coverage with Istanbul

We now have Mocha set up and are testing, great. But how do we know if
we&rsquo;re testing the right stuff. That&rsquo;s where Istanbul comes into
play.

[Istanbul](https://istanbul.js.org) is JavaScript test coverage made simple.
It counts the lines of code hit when running your tests to generate an
overall percentage along with a full detailed report.

To use Istanbul to generate test coverage, you actually only need the `nyc`
cli client.

To install:

    yarn add --dev nyc

Now all you will need to do is update your test command.

    scripts: {
      "test": "nyc mocha"
    }

Now rerun your tests and bask in the test coverage light.

## Automate with TravisCI and Coveralls

We&rsquo;ve now added testing and test coverage with little effort, but
let&rsquo;s go a bit further. Let&rsquo;s make this all happen when pushing
to [GitHub](https://github.com) with [TravisCI](https://travis-ci.org).
We will also generate a report on
[Coveralls.io](https://coveralls.zendesk.com/hc/en-us).

Before we set up the build, we need to install coveralls. Do that by running:

    yarn add --dev coveralls

This command will take our test coverage output and send it to Coveralls.io.
Then add a command to your `scripts` section in your `package.json`:

    scripts: {
      "test": "nyc mocha",
      "overalls": "nyc report --reporter=text-lcov | coveralls"
    }

This command will tell `nyc` to report our coverage but output it in the `lcov`
form and pipe that to `coveralls`.

Then, to tell TravisCI how to build your project, your `.travis.yml` file will
look something like this:

```
language: node_js
node_js:
  - "6"

before_install:
  - npm install -g yarn
install:
  - yarn install
script:
  - yarn run test
after_success:
  - yarn run overalls
```

This is saying to install yarn before we install any dependencies, then use
yarn to install those dependencies, after that we run our tests, and only
after the build is successful do we send our test coverage report to
Coveralls.io.

## Conclusion

That&rsquo;s about it! We added testing and testing coverage and were able
to automate the build and generate a nice report all with minimal work.

If you would like to see a live Coveralls.io report, you can checkout
[https://coveralls.io/github/rjgoldsborough/node-cannabis-reports?branch=master](https://coveralls.io/github/rjgoldsborough/node-cannabis-reports?branch=master).

Tweet me at [@rjgoldsborough](https://twitter.com/rjgoldsborough) with any
feedback or questions!
