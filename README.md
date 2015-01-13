<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1. Introduction</a></li>
<li><a href="#sec-2">2. Change log</a></li>
<li><a href="#sec-3">3. My environment</a></li>
<li><a href="#sec-4">4. org-mode LaTeX settings</a></li>
</ul>
</div>
</div>


# Introduction<a id="sec-1"></a>

This file **IS NOT** the tutorial, and the **pdf file** in the repo is that.

This file is an introduction to those who want to modify the org file and export it
to pdf files on their local environment.

# Change log<a id="sec-2"></a>

2015-01-13
update settings about org-mode

# My environment<a id="sec-3"></a>

I write this document in Emacs 24.3.1 with org-mode 8.3beta.

According to my experience, there are some changes between org-mode 7.9 and 8.3beta.
So I suggest you'd better use org-mode greater than 8.0 to export the org file.

# org-mode LaTeX settings<a id="sec-4"></a>

Here is my settings about org-mode

    ; org-mode export to latex
    (require 'ox-latex)
    (setq org-export-latex-listings t)
    ; org-mode source code setup in exporting to latex
    (add-to-list 'org-latex-listings '("" "listings"))
    (add-to-list 'org-latex-listings '("" "color"))
    
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
    (add-to-list 'org-latex-packages-alist
             '("" "graphicx" t))
    
    (add-to-list 'org-latex-classes
              '("my-org-book-zh"
    "\\documentclass{book}
    \\usepackage[slantfont, boldfont]{xeCJK}
    % chapter set
    \\usepackage[Lenny]{fncychap}
    [NO-DEFAULT-PACKAGES]
    [PACKAGES]
    \\setCJKmainfont{SimSun} % 设置缺省中文字体
    \\parindent 2em
    
    \\setmainfont{DejaVu Sans} % 英文衬线字体
    \\setsansfont{DejaVu Serif} % 英文无衬线字体
    \\setmonofont{DejaVu Sans Mono} % 英文等宽字体
    %\\punctstyle{DejaVu Sans} % 开明式标点格式
    
    
    \\defaultfontfeatures{Mapping=tex-text} %如果没有它，会有一些 tex 特殊字符无法正常使用，比如连字符。
    
    % 中文断行
    \\XeTeXlinebreaklocale \"zh\"
    \\XeTeXlinebreakskip = 0pt plus 1pt minus 0.1pt
    
    % 代码设置
    \\lstset{numbers=left, 
    numberstyle= \\tiny, 
    keywordstyle= \\color{ blue!70},commentstyle=\\color{red!50!green!50!blue!50}, 
    frame=shadowbox, 
    breaklines=true,
    rulesepcolor= \\color{ red!20!green!20!blue!20} 
    } 
    
    [EXTRA]
    "
                 ("\\chapter{%s}" . "\\chapter*{%s}")
                 ("\\section{%s}" . "\\section*{%s}")
                 ("\\subsection{%s}" . "\\subsection*{%s}")
                 ("\\subsubsection{%s}" . "\\subsubsection*{%s}")
                 ("\\paragraph{%s}" . "\\paragraph*{%s}")
                 ("\\subparagraph{%s}" . "\\subparagraph*{%s}")))
    
    (setq org-latex-pdf-process
          '("xelatex -interaction nonstopmode %b"
        "xelatex -interaction nonstopmode %b"))
    
    ; org-mode babel load languages
    (org-babel-do-load-languages
     'org-babel-load-languages
     '((ditaa . t)
       (shell . t)))
