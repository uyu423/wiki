---
title: Visual Studio Code 초기 세팅 및 추천 플러그인
description: 
published: true
date: 2023-02-17T17:59:24.794Z
tags: vscode
editor: markdown
dateCreated: 2022-11-24T04:41:28.192Z
---

# Visual Studio Code

- Atom 은 아무래도 TypeScript 에서는 영 구린것 같다.
- 그리고 GitLens 가 너무 좋아보여서 vscode 로 가즈아
- vscode 가 더 가벼운 것 같다.

## Mac 에서 PATH 에 `code` 추가

- vscode 열고, Shift + Cmd + P
- Shell Command: Install 'code' command in PATH

## package install (v.20200421)

```
$ code --list-extensions

aaron-bond.better-comments
amatiasq.sort-imports
CoenraadS.bracket-pair-colorizer
dbaeumer.vscode-eslint
eamodio.gitlens
eg2.vscode-npm-script
Equinusocio.vsc-community-material-theme
Equinusocio.vsc-material-theme
equinusocio.vsc-material-theme-icons
esbenp.prettier-vscode
ms-vscode.vscode-typescript-tslint-plugin
PKief.material-icon-theme
vscodevim.vim
```

```bash
# MacBook Pro on Workplace

code --install-extension aaron-bond.better-comments
code --install-extension amatiasq.sort-imports
code --install-extension CoenraadS.bracket-pair-colorizer
code --install-extension dbaeumer.vscode-eslint
code --install-extension eamodio.gitlens
code --install-extension eg2.vscode-npm-script
code --install-extension Equinusocio.vsc-community-material-theme
code --install-extension Equinusocio.vsc-material-theme
code --install-extension equinusocio.vsc-material-theme-icons
code --install-extension esbenp.prettier-vscode
code --install-extension ms-vscode.vscode-typescript-tslint-plugin
code --install-extension PKief.material-icon-theme
code --install-extension vscodevim.vim
```

## package install (legacy)

- TypeScript, PHP, vim extenstion 설정은 걍 vscode 켜고 첫화면에서 클릭 세번하니 완료됨.

```bash
code --install-extension eamodio.gitlens
code --install-extension shd101wyy.markdown-preview-enhanced
code --install-extension Equinusocio.vsc-material-theme
code --install-extension PKief.material-icon-theme
code --install-extension abusaidm.html-snippets
code --install-extension tht13.html-preview-vscode
code --install-extension esbenp.prettier-vscode
code --install-extension CoenraadS.bracket-pair-colorizer
code --install-extension wayou.vscode-todo-highlight
# Vscode Korean Patch
code --install-extension ms-ceintl.vscode-language-pack-ko
# Vscode Vim Mode
code --install-extension vscodevim.vim
# Json Util
code --install-extension eriklynd.json-tools
# Json to TS Interface
code --install-extension mariusalchimavicius.json-to-ts
# Vscode famous Icon Theme(Ctrl + Shift + P -> Icons: Activate VSCode Icons)
code --install-extension robertohuertasm.vscode-icons

```

### Typescript 관련

```bash
# Typescript lint plugin by MS
code --install-extension ms-vscode.vscode-typescript-tslint-plugin
# Typescript Commmon Lint
# code --install-extension eg2.tslint
```

### golang 관련

```bash
code --install-extension ms-vscode.go
```

### GitLens

- Extenstion Id : `eamodio.gitlens`
- Git 과 관련된 편한 기능을 제공해준다.
- 가장 마음에 든 기능은 에디터에서 각 row 마다 blame 을 보여주는 기능
  - 사실상 이 기능 때문에 atom 에서 vscode 로 갈아탐
- 더 많은 기능이 있을 것 같지만 깊게 써보지는 않음.
  ![image](https://user-images.githubusercontent.com/8033320/36265737-3566d1ce-12b3-11e8-8334-1a15e16cc9ed.png)

### Markdown Preview Enhanced`

- Extenstion Id: `shd101wyy.markdown-preview-enhanced`
- 마크다운 미리보기 기능을 제공 `ctrl` + `shift` + `m`

### Material Theme

- Extenstion Id: `Equinusocio.vsc-material-theme`
- 마테리얼 테마

### Material Icon Teheme

- Extenstion Id: `PKief.material-icon-theme`
- 마테리얼 아이콘 테마

### HTML Snippets

- Extenstion Id: `abusaidm.html-snippets`
- HTML 스니펫 제공

### HTML Preview

- Extenstion Id: `tht13.html-preview-vscode`
- HTML 미리보기 기능을 제공 `ctrl` + `shift` + `h`

### Prettier Code Formater

- Extension Id: `esbenp.prettier-vscode`
- [Prettier](https://github.com/prettier/prettier) 의 VsCode Plugin
- javascript, TypeScript, CSS 코드 포맷을 이쁘게 맞춰준다.
- TSLint 의 AutoFix 가 제대로 못 잡아주는 형식을 잡는데 사용한다.

## Bracket Pair Colorizer

- Extension Id: `CoenraadS.bracket-pair-colorizer`
- 브라켓 (`()` 등)을 구분하기 쉽도록 컬러라리이징 해준다.

## VsCode Todo Highlight

- Extension Id: `wayou.vscode-todo-highlight`
- 주석으로 TODO, FIXME, REVIEW 등의 코멘트를 하이라이팅 처리해준다.
- Shifp + cmd + p 에서 Todo List 를 따로 색인하여 확인 할 수도 있다.
