# Course notes template

Copy `template/main.tex`, `template/entries`, `template/.vscode`, and
`template/.latexmkrc` into a course-code folder. Preserve any existing notes
when copying.
`STA347` is already set up with a main document and its first entry.

Edit `coursecode`, `coursename`, `term`, and `studentname` near the top, then
write your notes directly in `entries/lec01.tex`. Each entry starts with an
editable title such as `\section{Week 1}` or `\section{Week 1: Probability basics}`.
STA347's first entry is `entries/week01.tex`. Week titles appear in the table
of contents.

Keep `template/preamble.tex` in place: course documents share its formatting
and math commands through `\input{../template/preamble.tex}`. Course folders
must sit beside `template`, as they do now.

## Build a PDF

In VS Code with LaTeX Workshop, saving an entry automatically builds the
entire course's `main.pdf`. You can also run **LaTeX Workshop: Build LaTeX
project** while editing an entry. The included `.vscode/settings.json` works
when you open the course folder directly; Notes also has these settings.

Keep this line at the very top of every entry (duplicating an entry preserves it):

```tex
% !TeX root = ../main.tex
```

It directs the editor to the course's main document. New entries still need
an `\input` line in `main.tex` to appear in the PDF. These editor settings
use LaTeX Workshop's [build-on-save support](https://github.com/James-Yu/LaTeX-Workshop/wiki/Compile#latex-workshoplatexautobuildrun).

Run these commands from the Notes folder after copying the starter:

```sh
cd STA347
latexmk -pdf -interaction=nonstopmode -halt-on-error main.tex
```

This creates `main.pdf` in the course folder. Substitute another course code
as needed. To preview the starter itself, use `cd template` instead.
If using an editor, configure it to compile from the document's folder.

Each course folder's `.latexmkrc` sends build clutter (`.aux`, `.log`,
`.fls`, `.fdb_latexmk`, `.out`, `.toc`, `.synctex.gz`) into a `build/`
subfolder; only `main.pdf` lands next to `main.tex`. Copy `.latexmkrc` along
with the other starter files when setting up a new course.

## Write notes

- Use `\section{Week 1}` for the entry title and `\subsection{Heading}` for topics within it.
- Write inline math as `$x^2$` and displayed math as `\[ x^2 \]`.
- Use `equation` for numbered equations and `align` for aligned derivations.
- Available environments: `definition`, `theorem`, `lemma`, `proposition`,
  `example`, `exercise`, `remark`, and `proof`.
- Shortcuts: `\R`, `\N`, `\Z`, `\E`, `\Prob`, `\Var`, and `\Cov`.
- Escape special text characters, for example `\%`, `\&`, `\_`, and `\#`.

## Add a lecture

### Definition and theorem shortcuts

In VS Code, type `definition` (or `def`) or `theorem` (or `thm`), then
select the corresponding **Course notes** completion. If suggestions are
hidden, press Control+Space. The snippet inserts both environment lines;
edit the selected optional `[Name]` (or delete it), then press Tab to write
the body. Snippets are included in `.vscode/notes.code-snippets`.

You can also type the environments directly in any entry:

```tex
\begin{definition}[Independence]
  Events $A$ and $B$ are independent if
  $\Prob(A \cap B) = \Prob(A)\Prob(B)$.
\end{definition}

\begin{theorem}[Complement rule]
  For any event $A$, $\Prob(A^c) = 1 - \Prob(A)$.
\end{theorem}
```

These environments are already defined in `template/preamble.tex` and
numbered continuously through the document. The bracketed name is optional;
titles print bold with no parentheses (e.g. `\begin{theorem}[Complement
rule]` prints "**Theorem 1 Complement rule.**"). `definition` prints as
"Def." instead of "Definition".

All six (`theorem`, `lemma`, `proposition`, `definition`, `example`,
`exercise`) also accept a second bracketed argument for a custom number, to
match a textbook's own numbering: `\begin{proposition}[][2.7]` prints
"Proposition 2.7." (no title), and `\begin{example}[Coin Flips][2.8]` prints
"Example 2.8 Coin Flips." (title and number). Leave the first bracket
empty (`[]`) to give a number with no title. The shared counter still
advances normally afterward, so later auto-numbered environments are
unaffected.

### Entry files

Duplicate `entries/lec01.tex` as `entries/lec02.tex`, clear any
previous notes, update the week title, and start writing. Keep the root-file comment at the top.

Each entry contains its week title, notes, and root-file comment, without a document
class, preamble, or `document` environment. In `main.tex`, add an input for
each entry before `\end{document}`, in reading order:

```tex
\input{entries/lec01.tex}
\input{entries/lec02.tex}
```

Compile `main.tex` to build the entire course, including the table of contents.
Paths inside entries are relative to the course folder, so images stored in
a course-local `figures` folder can use `\includegraphics{figures/diagram.png}`.
