<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1. Introduction</a></li>
<li><a href="#sec-2">2. My environment</a></li>
<li><a href="#sec-3">3. org-mode LaTeX settings</a></li>
</ul>
</div>
</div>


# Introduction<a id="sec-1"></a>

This file is not the tutorial, and the pdf file in the repo is that.

This file is an introduction to those who want to modify the org file and export it
to pdf files on their local environment.

# My environment<a id="sec-2"></a>

I write this document in Emacs 24.3.1 with org-mode 8.3beta.
According to my experience, there are some changes between org-mode 7.9 and 8.3beta.
So I suggest you'd better use org-mode greater than 8.0 to export the org file.

# org-mode LaTeX settings<a id="sec-3"></a>

At first, I manually require org-latex's el file and enable export listings.

    (require 'ox-latex)
    (setq org-export-latex-listings t)

Because there is a confilt between inputenc and xeCJK package of LaTeX, 
and inputenc is in the default package list of org-mode,
I disabled the default package list.
So, I add some useful package to the user's package list.

    (add-to-list 'org-latex-packages-alist
                 '("" "hyperref" t))
    (add-to-list 'org-latex-packages-alist
                 '("" "xcolor" t))
    (add-to-list 'org-latex-packages-alist
                 '("" "listings" t))
    (add-to-list 'org-latex-packages-alist
                 '("" "fontspec" t))
    (add-to-list 'org-latex-packages-alist
                 '("" "indentfirst" t))
    (add-to-list 'org-latex-packages-alist
                 '("" "xunicode" t))
    (add-to-list 'org-latex-packages-alist
                 '("" "amsmath"))

Next, I add an org-latex-class, *my-org-article-zh*.
In the class setting, I set something about xeCJK and listings.
You need to install the following fonts:

-   SimSun
-   DejaVu Sans
-   DejaVu Serif
-   DejaVu Sans Mono

    (add-to-list 'org-latex-classes
              '("my-org-article-zh"
    
    "\\documentclass{article}
    
    \\usepackage[slantfont, boldfont]{xeCJK}
    
    [NO-DEFAULT-PACKAGES]
    
    [PACKAGES]
    
    \\setCJKmainfont{SimSun}
    
    \\parindent 2em
    
    \\setmainfont{DejaVu Sans}
    
    \\setsansfont{DejaVu Serif}
    
    \\setmonofont{DejaVu Sans Mono}
    
    \\defaultfontfeatures{Mapping=tex-text}
    
    \\XeTeXlinebreaklocale \"zh\"
    
    \\XeTeXlinebreakskip = 0pt plus 1pt minus 0.1pt
    
    \\lstset{numbers=left, 
    
    numberstyle= \\tiny, 
    
    keywordstyle= \\color{ blue!70},commentstyle=\\color{red!50!green!50!blue!50}, 
    
    frame=shadowbox, 
    
    rulesepcolor= \\color{ red!20!green!20!blue!20} 
    
    } 
    
    [EXTRA]
    "
    
                 ("\\section{%s}" . "\\section*{%s}")
                 ("\\subsection{%s}" . "\\subsection*{%s}")
                 ("\\subsubsection{%s}" . "\\subsubsection*{%s}")
                 ("\\paragraph{%s}" . "\\paragraph*{%s}")
                 ("\\subparagraph{%s}" . "\\subparagraph*{%s}")))

Finally, I change the export process from *pdflatex* to *xelatex*,
so you need to install xetex first.

    (setq org-latex-pdf-process
          '("xelatex -interaction nonstopmode %b"
            "xelatex -interaction nonstopmode %b"))
