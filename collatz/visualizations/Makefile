SOURCE = collatz-27
DELAY = 80
DENSITY = 300
WIDTH = 512

make:
	pdflatex $(SOURCE).tex -output-format=pdf
	make clean

clean:
	rm -rf  *.class *.html *.log *.aux *.data

gnuplot:
	gnuplot plot.gnuplot
	pdflatex gnuplot-comb.tex -output-format=pdf
	rm plot-tmp.tex
	make clean

gif:
	pdfcrop $(SOURCE).pdf
	convert -verbose -delay $(DELAY) -loop 0 -density $(DENSITY) $(SOURCE)-crop.pdf $(SOURCE).gif
	make clean

png:
	make
	make svg
	inkscape $(SOURCE).svg -w $(WIDTH) --export-png=$(SOURCE).png

transparentGif:
	convert $(SOURCE).pdf -transparent white result.gif
	make clean

RToPNG:
	R -f analyze.R
	pdf2svg Rplots.pdf Rplots.svg
	# Necessary, as pdf2svg does not always create valid svgs:
	inkscape Rplots.svg --export-plain-svg=Rplots.svg
	rsvg-convert -a -w $(WIDTH) -f svg Rplots.svg -o Rplots2.svg
	inkscape Rplots2.svg --export-plain-svg=Rplots.svg
	rm Rplots2.svg
	inkscape Rplots.svg -w $(WIDTH) --export-png=Rplots.png

svg:
	make
	#inkscape $(SOURCE).pdf --export-plain-svg=$(SOURCE).svg
	pdf2svg $(SOURCE).pdf $(SOURCE).svg
	# Necessary, as pdf2svg does not always create valid svgs:
	inkscape $(SOURCE).svg --export-plain-svg=$(SOURCE).svg
	rsvg-convert -a -w $(WIDTH) -f svg $(SOURCE).svg -o $(SOURCE)2.svg
	inkscape $(SOURCE)2.svg --export-plain-svg=$(SOURCE).svg
	rm $(SOURCE)2.svg
