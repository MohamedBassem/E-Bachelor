pdf:
		latex mtheme.ins
		latex mtheme.ins
		latex mtheme.ins
		latex mtheme.ins
		latex mtheme.ins
		latex mtheme.ins
		latexmk -xelatex -output-directory=.temptex presentation.tex
		cp .temptex/presentation.pdf .

clean:
		find . -maxdepth 2 -name '*.sty' -exec rm {} \;
		find . -maxdepth 2 -name '*.log' -exec rm {} \;
		find . -maxdepth 2 -name '*.out' -exec rm {} \;
		find . -maxdepth 2 -name '*.nav' -exec rm {} \;
		find . -maxdepth 2 -name '*.snm' -exec rm {} \;
		find . -maxdepth 2 -name '*.vrb' -exec rm {} \;
		find . -maxdepth 2 -name '*.toc' -exec rm {} \;
		find . -maxdepth 2 -name '*.aux' -exec rm {} \;
		rm -rf .temptex

