textabletidy
============

is a (very) simple script to align the columns of a TeX table. I tried to make it as simple as possible while still being useful.

I wrote this while working on a book which contained several tables of statistics. These tables were generated automatically, but were difficult to read along with the rest of the LaTeX source because the columns weren't lined up. I took a quick look around, but didn't find anything that looked like a simple and easy solution.

Usage
-----

If `example.table.tex` contains a TeX table,

	cat example.table.tex | textabletidy

or

	textabletidy example.table.tex

will both write the aligned table to `STDOUT`.

Example
-------
`example.table.tex` contains

	\begin{tabular}{
		r
		S[table-format=1.3]
		S[table-format=3.5e-1]
		S[table-format=1.4]
		S[table-format=-1.5]
	}\toprule
	Frankness & {$\aleph_0$} & {Widgets \& Bobbins} & {$\Delta_{\text{funk}}$} & {$r$}\\\midrule
	Crows & 5.897 & 0.3692 & 0.4679 & -0.1367\\
	Malaise & 5.128 & 1.692e-05 & 0.6395 & -0.06257\\
	Lantern & 6.334 & 0.7099 & 0.57 & -0.1425\\
	Rushing & 15.11 & 0.01569 & 0.3576 & 0.01739\\\midrule
	Splinters & 3.753 & 1.084 & 0.2924 & -0.1632\\
	Brilliant & 3.174 & 1.061e+04 & 0.2827 & -0.2533\\
	Still & 3.192 & 1.795e+04 & 0.3066 & -0.1173\\
	\midrule
	Quickening & 2.93 & 250.6 & 0.999 & -0.02164\\
	Barter & 3.437 & 6.625e-06 & 0.8351 & -0.6018\\
	Promise & 9.753 & 16.03 & 0.5062 & 0.1852\\
	\bottomrule
	\end{tabular}

This is hard to read. Piping it through `textabletidy` makes it easier to read:

	\begin{tabular}{
		r
		S[table-format=1.3]
		S[table-format=3.5e-1]
		S[table-format=1.4]
		S[table-format=-1.5]
	}\toprule
	Frankness  & {$\aleph_0$} & {Widgets \& Bobbins} & {$\Delta_{\text{funk}}$} & {$r$}    \\ \midrule
	Crows      & 5.897        & 0.3692               & 0.4679                   & -0.1367  \\ 
	Malaise    & 5.128        & 1.692e-05            & 0.6395                   & -0.06257 \\ 
	Lantern    & 6.334        & 0.7099               & 0.57                     & -0.1425  \\ 
	Rushing    & 15.11        & 0.01569              & 0.3576                   & 0.01739  \\ \midrule
	Splinters  & 3.753        & 1.084                & 0.2924                   & -0.1632  \\ 
	Brilliant  & 3.174        & 1.061e+04            & 0.2827                   & -0.2533  \\ 
	Still      & 3.192        & 1.795e+04            & 0.3066                   & -0.1173  \\ 
	\midrule
	Quickening & 2.93         & 250.6                & 0.999                    & -0.02164 \\ 
	Barter     & 3.437        & 6.625e-06            & 0.8351                   & -0.6018  \\ 
	Promise    & 9.753        & 16.03                & 0.5062                   & 0.1852   \\ 
	\bottomrule
	\end{tabular}

Notice that `textabletidy` doesn't do anything to lines that don't look like rows of the table, that it doesn't force things like horizontal rule commands to appear on their own line, and that it doesn't get confused by escaped ampersands.

Failure points
--------------

`textabletidy` chokes if a table row doesn't contain the same number of columns as the other rows. This occurs when using `\multirow`, for example.
