# Reproduction of [#4988](https://github.com/pnpm/pnpm/issues/4988)

```
# no lockfile in repo
pnpm i
ls workspace-app1/node_modules/lodash && echo "peer dep was auto installed successfully"
ls workspace-app2/node_modules/lodash && echo "peer dep was auto installed successfully"

# (should be successful)

# remove all installed module dirs
find . -maxdepth 3 -type d -name node_modules -exec rm -rf '{}' \;

# lockfile but nothing installed (like fresh repo)
pnpm i
ls workspace-app1/node_modules/lodash && echo "peer dep was auto installed successfully"
ls workspace-app2/node_modules/lodash && echo "peer dep was auto installed successfully"

# expected to work but not seeing these modules installed:

# ls: workspace-app1/node_modules/lodash: No such file or directory
# ls: workspace-app2/node_modules/lodash: No such file or directory
```