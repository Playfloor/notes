# LaTeX Cheatsheet & Notes

## `minted`

When using `\usepackage{minted}`,
you'll most likely want `\usepackage[newfloat]{minted}` which brings the `minted` environment as a valid float,
allowing you to put it into a `listing` environment without complications.

`minted` requires `-shell-escape` which you can configure with `.latexmkrc`.

## `hyperref`

To rename the output of `\autoref` you can use:
```latex
\AtBeginDocument{ % in case the hyperref import is inaccessible to you
  \addto\extrasenglish{ % define this as the english value for babel
    \renewcommand{\XXXautorefname}{XXX} % where XXX is the command name
  }
}
```

## `tikz`

### Setting a style

Using `tikzset`:
```latex
\tikzset{
  s1/.style={->, thick},
  s2/.style={...}
}
```

Using `tikzstyle` (*preferred*):
```latex
\tikzstyle{s1}=[->, thick]
\tikzstyle{s2}=[...]
```