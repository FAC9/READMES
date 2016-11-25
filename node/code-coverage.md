Does Codecov replace my CI provider?

No, Codecov does not run your test suite. That's the job of a CI provider.
Codecov does static analysis on your repository once your tests are complete and coverage reports are uploaded.

Once complete Istanbul will generate you an lcov file that you can send to services like coveralls and a html web page that details the percentage of your code that is covered and even the specific code lines that have been and hit and the ones that haven’t. (http://www.vapidspace.com/coding/2014/10/29/code-coverage-metrics-with-mocha-and-istanbul/)
