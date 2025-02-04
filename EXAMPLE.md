% Proof of Existing Pandoc Feature
% Kurt Pfeifle
% May 25th, 2015

# Basics

This is not just a *proof of concept*, but a basic utilization of [Pandoc][2]'s behavior
when it comes to [Markdown][1] processing.

* Pandoc, by default, passes any \LaTeX\ code snippets it identifies within the Markdown
  source file to the target document, if that target document is a \LaTeX\ one (this
  includes f.e. Beamer or PDF output.
  (It does not pass these snippets to any other output formats, but instead drops them.)
* Pandoc, by default, also passes any HTML code snippets it identifies within the
  Markdown sources to the target document, should that be HTML based (this includes f.e.
  EPUB or RevealJS output).
  (It does not pass these snippets to any other output formats, but instead drops them.)
* This allows for any specific formatting to be achieved in the target document format:
  ***(1)*** Insert two versions of the snippet, one as HTML, one as \LaTeX\. ***(2)***
  The HTML one will make it to the HTML-based targets, while \LaTeX\ is being dropped;
  the \LaTeX\ will make it into \LaTeX-based targets, while the HTML is being dropped.

It also supports linked references. **[Click here](#tab:fsttable)** to jump to a page with a
table.

## How it works

It works out of the box:

1. Just write a Markdown document, and sprinkle your \LaTeX\ code snippets in between.
1. Save the document with an `.md` suffix.
1. Run the Pandoc conversion:

    ```` {.bash}
     pandoc --from=markdown --output=my.tex my.md --to=latex --standalone
    ````

    or

    ```` {.bash}
     pandoc --from=markdown --output=my.pdf my.md \
            --variable=geometry:"margin=0.5cm, paperheight=421pt, paperwidth=595pt" \
            --highlight-style=espresso
    ````

I want a few words appear as \textcolor{red}{red} or in a \textcolor{green}{different}
\textcolor{blue}{color}. Here is the Markdown source code of previous sentence; it uses
no syntax highlighting (unlike the previous two code blocks):

     [...] as \textcolor{red}{red} or in a \textcolor{green}{different}
     \textcolor{blue}{color}.

After this paragraph, I want to insert a page break. I'll add `\newpage{}` beneath, on
a line of its own.

\newpage{}

This was the Markdown source code (with context) for the page break preceeding this:

```` {.markdown}
After this paragraph, I want to insert a page break. I'll add `\newpage{}` beneath, on
a line of its own.

\newpage{}
````

## Inserting a \LaTeX\ table

Here comes a table. Its code is inserted as \LaTeX\ code into the Markdown source document:

\begin{table}[h]
\centering
\begin{tabular}{|r|l|}
  \hline
  7C0 & hexadecimal \\
  3700 & octal \\ \cline{2-2}
  11111000000 & binary \\
  \hline \hline
  1984 & decimal \\
  \hline
\end{tabular}
\caption\small\textit{\textcolor{magenta}{This table shows some data}}
\label{tab:fsttable}
\end{table}

This is the Markdown code for the previous table, including its textual context:

```` {.latex}
Here comes a table. Its code is inserted as \LaTeX\ code into the Markdown source document:

\begin{table}[h]
\centering
\begin{tabular}{|r|l|}
  \hline
  7C0 & hexadecimal \\
  3700 & octal \\ \cline{2-2}
  11111000000 & binary \\
  \hline \hline
  1984 & decimal \\
  \hline
\end{tabular}
\caption\small\textit{\textcolor{magenta}{This table shows some data}}
\label{tab:fsttable}
\end{table}

This is the Markdown code for the previous table, including its textual context:
````

## Inserting a \LaTeX\ Formula

To include a mathematical formula in Markdown, enclose it with **`$`** characters like this:

```` {.latex}
 $\frac{n!}{k!(n-k)!} = \binom{n}{k}$
````

The result:

$\frac{n!}{k!(n-k)!} = \binom{n}{k}$

# Status

There are no known (to me) bugs for this feature.

[1]: http://daringfireball.net/projects/markdown/
[2]: http://pandoc.org/