This repository is meant to demonstrate an issue in
SublimeLinter-eslint.

## steps to replicate

#### prerequisites

1. SublimeLinter
2. SublimeLinter-eslint (https://github.com/SublimeLinter/SublimeLinter-eslint#installation)
3. Node.js (and npm)
4. eslint `npm install -g eslint`

#### steps

1. Clone this repo
2. Open bin.js in Sublime Text
3. Save it. You will see `eslint(erred)` in the status bar.
4. Open the sublime console. You'll see the error I got below, which is `TypeError: string indices must be integers`

## workaround

Change the `package.json` file to this:
```json
{"bin":{"cli":"whatever.js"}}
```

Then save bin.js, and the syntax error will be found.


## full error message

I have SublimeLinter debug:true in my user settings. Even without that, you should recieve the entire stack trace below

```
SublimeLinter: #104 linter.py:1003    eslint: linting 'bin.js'
SublimeLinter: #104 __init__.py:1273  ERROR: Unhandled exception:
Traceback (most recent call last):
  File "C:\Users\Joseph\AppData\Roaming\Sublime Text 3\Installed Packages\SublimeLinter.sublime-package\lint/backend.py", line 157, in execute_lint_task
    errors = linter.lint(code, view_has_changed)
  File "C:\Users\Joseph\AppData\Roaming\Sublime Text 3\Installed Packages\SublimeLinter.sublime-package\lint/linter.py", line 1010, in lint
    cmd = self.get_cmd()
  File "C:\Users\Joseph\AppData\Roaming\Sublime Text 3\Installed Packages\SublimeLinter.sublime-package\lint/linter.py", line 729, in get_cmd
    return self.build_cmd(cmd)
  File "C:\Users\Joseph\AppData\Roaming\Sublime Text 3\Installed Packages\SublimeLinter.sublime-package\lint/linter.py", line 742, in build_cmd
    have_path, path = self.context_sensitive_executable_path(cmd)
  File "C:\Users\Joseph\AppData\Roaming\Sublime Text 3\Installed Packages\SublimeLinter.sublime-package\lint/base_linter/node_linter.py", line 81, in context_sensitive_executable_path
    local_cmd = self.find_local_executable(start_dir, npm_name)
  File "C:\Users\Joseph\AppData\Roaming\Sublime Text 3\Installed Packages\SublimeLinter.sublime-package\lint/base_linter/node_linter.py", line 126, in find_local_executable
    script = os.path.normpath(os.path.join(path, manifest['bin'][npm_name]))
TypeError: string indices must be integers
```

## what I expect to happen

Since NPM supports the [bin property](https://docs.npmjs.com/files/package.json#bin) being set as a string, as well as an object...


I expect that the bin property can be set as a string and sublime linter should not fail.
