This file is meant to demonstrate an issue in
SublimeLinter-eslint.

## what happened

If the `package.json` file is this:
```json
{"bin":{"cli":"whatever.js"}}
```

then the syntax error in `bin.js` is found.

but if I change the `package.json` file to this:
```json
{"bin":"whatever.js"}
```

then I receive this error:

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

NPM supports the bin property being set as a string, as well as an object:
https://docs.npmjs.com/files/package.json#bin

## what I expect to happen

I expect that the bin property being set as a string does not cause sublime linter to fail.
