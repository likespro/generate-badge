<p align="center">
 <img width="100px" src="https://github.com/likespro.png" align="center" alt="MasterID Server" />
 <h2 align="center">Generate Badge</h2>
 <p align="center">Creates dynamic and customizable README badges using shields.io/endpoint</p>
</p>
<p align="center">
    <a href="https://github.com/likespro/generate-badge">
      <img alt="LICENSE" src="https://img.shields.io/badge/licence-MIT-yellow" />
    </a>
    <a href="https://github.com/likespro/generate-badge/graphs/contributors">
      <img alt="GitHub Contributors" src="https://img.shields.io/github/contributors/likespro/generate-badge" />
    </a>
    <a href="https://github.com/likespro/generate-badge/issues">
      <img alt="Issues" src="https://img.shields.io/github/issues/likespro/generate-badge?color=0088ff" />
    </a>
    <a href="https://github.com/likespro/generate-badge/pulls">
      <img alt="GitHub pull requests" src="https://img.shields.io/github/issues-pr/likespro/generate-badge?color=0088ff" />
    </a>
  </p>
<p align="center">
    <a href="https://github.com/likespro/generate-badge/actions/workflows/main-branch.yml">
      <img alt="Build Passing" src="https://github.com/likespro/generate-badge/workflows/Main Branch Workflow/badge.svg" />
    </a>
    <a href="https://github.com/likespro/generate-badge">
      <img alt="Git Size" src="https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/git-size.md" />
    </a>
    <a href="https://github.com/likespro/generate-badge">
      <img alt="Git File Count" src="https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/git-file-count.md" />
    </a>
    <a href="https://github.com/likespro/generate-badge">
      <img alt="Git Lines Of Code" src="https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/git-lines-of-code.md" />
    </a>
  </p>

## Overview
*Forked from [peterrhodesdev/build-a-badge](https://github.com/peterrhodesdev/build-a-badge)*

GitHub Action to create dynamic and customizable README badges using the [Shields.io endpoint](https://shields.io/endpoint). You can specify the repository and the branch where badges will be stored, unlike in the original project.

This is achieved by storing the required JSON data of the badge in some branch of the repository (by default `badges` branch in the repository where action was called).

## Prerequisites
- All you need is just to create a branch where you want to store the badges (by default `badges` branch). For example: `git switch -c badges && git push origin badges`.

## Usage
### Single Badge
![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/my-badge.md)

Add a step to your workflow:

```yml
- name: Generate Badge
  uses: likespro/generate-badge@v1
  with:
    token: ${{ secrets.GITHUB_TOKEN }}
    filename: my-badge
    label: my
    message: badge
```

To display the badge in your README point the `url` parameter of the Shields endpoint query string to the raw content of the generated file in branch with badges (by default `badges` branch):

```markdown
![](https://img.shields.io/endpoint?url=https://github.com/<owner>/<repo>/blob/<branch-with-badges>/<filename>.md)
```

So, for the badge above it will be:

```markdown
![](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/my-badge.md)
```

### Multiple badges

![multiple-badges-1](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/multiple-badges-1.md) ![multiple-badges-2](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/multiple-badges-2.md) ![multiple-badges-3](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/multiple-badges-3.md) ![multiple-badges-4](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/multiple-badges-4.md) ![multiple-badges-5](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/multiple-badges-5.md)

The input parameters also support arrays so that multiple badges can be created in a single workflow step.

```yml
name: Create multiple badges
on: [push]
jobs:
  multiple-badges:
    name: Multiple badges
    runs-on: ubuntu-latest
    steps:
      - name: Generate Badge
        uses: likespro/generate-badge@v1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          filename: ("multiple-badges-1" "multiple-badges-2" "multiple-badges-3" "multiple-badges-4" "multiple-badges-5")
          label: ("label 1" "label 2" "label 3" "label 4" "label 5")
          message: ("message 1" "message 2" "message 3" "message 4" "message 5")
          color: ("darkslategrey" "008b8b" 'rgb(128,0,128)' 'hsl(229,100%,50%)' "")
          labelColor: ("critical" "9cf" 'rgba(72,209,204,0.5)' 'hsla(36,80%,40%,0.7)' "")
          namedLogo: ("github" "" "npm" "" "javascript")
          logoSvg: |
            (
              ''
              '<svg id="Layer_1" data-name="Layer 1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 122.88 122.88"><defs><style>.cls-1{fill:#ffd528;}.cls-1,.cls-2{fill-rule:evenodd;}.cls-2{fill:#141518;}</style></defs><title>smiley</title><path class="cls-1" d="M45.54,2.11A61.42,61.42,0,1,1,2.11,77.34,61.42,61.42,0,0,1,45.54,2.11Z"/><path class="cls-2" d="M45.78,32.27c4.3,0,7.79,5,7.79,11.27s-3.49,11.27-7.79,11.27S38,49.77,38,43.54s3.48-11.27,7.78-11.27Z"/><path class="cls-2" d="M77.1,32.27c4.3,0,7.78,5,7.78,11.27S81.4,54.81,77.1,54.81s-7.79-5-7.79-11.27S72.8,32.27,77.1,32.27Z"/><path d="M28.8,70.82a39.65,39.65,0,0,0,8.83,8.41,42.72,42.72,0,0,0,25,7.53,40.44,40.44,0,0,0,24.12-8.12,35.75,35.75,0,0,0,7.49-7.87.22.22,0,0,1,.31,0L97,73.14a.21.21,0,0,1,0,.29A45.87,45.87,0,0,1,82.89,88.58,37.67,37.67,0,0,1,62.83,95a39,39,0,0,1-20.68-5.55A50.52,50.52,0,0,1,25.9,73.57a.23.23,0,0,1,0-.28l2.52-2.5a.22.22,0,0,1,.32,0l0,0Z"/></svg>'
              ''
              '<?xml version="1.0" encoding="utf-8"?><svg version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 122.88 106.16" style="enable-background:new 0 0 122.88 106.16" xml:space="preserve"><style type="text/css">.st0{fill-rule:evenodd;clip-rule:evenodd;}</style><g><path fill="#b5eaaa" class="st0" d="M4.02,44.6h27.36c2.21,0,4.02,1.81,4.02,4.03v53.51c0,2.21-1.81,4.03-4.02,4.03H4.02 c-2.21,0-4.02-1.81-4.02-4.03V48.63C0,46.41,1.81,44.6,4.02,44.6L4.02,44.6z M63.06,4.46c2.12-10.75,19.72-0.85,20.88,16.48 c0.35,5.3-0.2,11.47-1.5,18.36l25.15,0c10.46,0.41,19.59,7.9,13.14,20.2c1.47,5.36,1.69,11.65-2.3,14.13 c0.5,8.46-1.84,13.7-6.22,17.84c-0.29,4.23-1.19,7.99-3.23,10.88c-3.38,4.77-6.12,3.63-11.44,3.63H55.07 c-6.73,0-10.4-1.85-14.8-7.37V51.31c12.66-3.42,19.39-20.74,22.79-32.11V4.46L63.06,4.46z"/></g></svg>'
              ''
            )
          style: ("" "plastic" "flat-square" "for-the-badge" "social")
```

- use [bash array](https://www.gnu.org/software/bash/manual/html_node/Arrays.html) syntax
- use single quotes `''` for strings that contain parentheses `()`
- use an empty string `""` to leave a parameter unassigned

> the smiley custom logo is from [Font Awesome](https://fontawesome.com/v5/icons/smile?s=solid) and the thumbs up custom logo is from [UXWing](https://uxwing.com/thumbs-up-black-icon/)

Add the badges to the README according to the `filename` specified for each:

```markdown
![multiple-badges-1](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/multiple-badges-1.md) 
![multiple-badges-2](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/multiple-badges-2.md) 
![multiple-badges-3](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/multiple-badges-3.md) 
![multiple-badges-4](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/multiple-badges-4.md) 
![multiple-badges-5](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/multiple-badges-5.md)
```

## Input Parameters

See [Shields.io](https://shields.io/) and the [endpoint](https://shields.io/endpoint) for a more detailed description and list of supported values for the parameters.

| Name           | Is required? | Default value | Array supported? | Description |
|----------------| --- | --- | --- | --- |
| token          | yes | | no | GitHub token secret used for authentication. The value [automatically created by GitHub](https://docs.github.com/en/actions/security-guides/automatic-token-authentication) can be used: `${{ secrets.GITHUB_TOKEN }}`. |
| filename       | yes | | yes | The filename to use for storing the JSON badge data. It cannot contain any whitespace characters. |
| label          | yes | | yes | The left text. |
| message        | yes | | yes | The right text. |
| color          | no | lightgrey | yes | The right color. |
| labelColor     | no | grey | yes | The left color. |
| namedLogo      | no | | yes | Logo supported by Shields. |
| logoSvg        | no | | yes | An SVG string containing a custom logo. |
| style          | no | flat | yes | The default template to use. |
| commitUsername | no | username from the last commit | no | Override for the commit username. |
| commitEmail    | no | email from the last commit | no | Override for the commit email. |
| commitMessage  | no | URL link to the last commit | no | Override for the commit message. |

Parameters marked as *Array supported* can be specified using either a single value or an array. Note that only one or the other is allowed, that is either all applicable parameters need to be single values or they all need to be arrays.

If `commitUsername`, `commitEmail`, and `commitMessage` are all overridden, then a checkout step will be skipped in the Generate Badge action, which will reduce the amount of time it takes to run.

## Examples
### Git
![git-size](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/git-size.md) ![git-file-count](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/git-file-count.md) ![git-lines-of-code](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/likespro/generate-badge/badges/git-lines-of-code.md)

```yml
name: Create git badges
on: [push]
jobs:
  generate-git-badges:
  name: Generate Git Badges
  runs-on: ubuntu-latest
  permissions:
    contents: write

  steps:
    - name: Checkout repository
      uses: actions/checkout@v4

    - name: Output git info
      id: git_info
      run: |
        function format_size { echo $(numfmt --to iec --suffix B $1); }
        function format_number { LC_ALL=en_US.UTF-8 printf "%'d\n" $1; }
        echo "file_count=$(format_number $(git ls-files | wc -l))" >> $GITHUB_OUTPUT
        echo "lines_of_code=$(git ls-files | xargs wc -l)" >> $GITHUB_OUTPUT
        git gc
        echo "size=$(format_size $(($(git count-objects -v | grep 'size-pack: ' | sed 's/size-pack: //g' | tr -d '\n') * 1024)))" >> $GITHUB_OUTPUT
      shell: bash

    - name: Generate-Badge
      uses: likespro/generate-badge@v1
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
        filename: |
          (
            "git-size"
            "git-file-count"
            "git-lines-of-code"
          )
        label: ("size" "files" "lines-of-code")
        message: |
          (
            "${{ steps.git_info.outputs.size }}"
            "${{ steps.git_info.outputs.file_count }}"
            "${{ steps.git_info.outputs.lines_of_code }}"
          )
        namedLogo: ("git" "git" "git")
        color: ("f1502f" "f1502f" "f1502f")
```