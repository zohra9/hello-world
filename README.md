# hello-world
JUST ANOTHER REPOSITORY
HSOUBI CHAKHSI
% This model is only usable with LaTeX 2 epsilon
% (highly) modified by
% Vivian Brégier <Vivian.Bregier@are-ata.org>
\NeedsTeXFormat{LaTeX2e}

\ProvidesClass{these}[2007/07/16 classe pour mise en forme de These]
\LoadClass[a4paper,12pt]{book}

\RequirePackage{fancyhdr}
\RequirePackage{tabularx}
\RequirePackage{ifthen}
\RequirePackage[includefoot,nomarginpar,twoside,
    top=27mm,bottom=20mm,
    head=5mm,headsep=7mm,
    footskip=7mm,
    hmargin=25mm,bindingoffset=10mm]{geometry}

\newif\if@blankemptypage
\DeclareOption{noblankemptypage}{\@blankemptypagefalse}
\DeclareOption{blankemptypage}{\@blankemptypagetrue}

\@blankemptypagefalse
%\ExecuteOptions{}
\ProcessOptions

% names
\newcommand{\@titleapp}{Titre}
\newcommand{\@engtitleapp}{Title}
\newcommand{\@resumeapp}{R\'esum\'e}
\newcommand{\@abstractapp}{Abstract}
\newcommand{\@keywordsapp}{Mot-clefs}
\newcommand{\@engkeywordsapp}{Keywords}
\newcommand{\@juryapp}{Jury}
\newcommand{\@advisorapp}{Directeur de th\`ese}
\newcommand{\@coadvisorapp}{Co-directeur de th\`ese}
\newcommand{\@labapp}{Laboratoire}

% Sets the name of the laboratory
\newcommand{\@labo}{\textbf{!\texttt{labo} \`a d\'efinir!}}
\newcommand{\labo}[1]{\renewcommand{\@labo}{#1}}

% Sets the name of the school
\newcommand{\@school}{\textbf{!\texttt{school} \`a d\'efinir!}}
\newcommand{\school}[1]{\renewcommand{\@school}{#1}}

% Sets the name of the phd speciality
\newcommand{\@speciality}{\textbf{!\texttt{speciality} \`a d\'efinir!}}
\newcommand{\speciality}[1]{\renewcommand{\@speciality}{#1}}

% Sets the name of the university
\newcommand{\@universityabbrv}{\textbf{!\texttt{universit\'e} \`a d\'efinir!}}
\newcommand{\@university}{\textbf{!\texttt{universit'e} \`a d\'efinir!}}
\newcommand{\university}[2]{
    \renewcommand{\@universityabbrv}{#1}
    \renewcommand{\@university}{#2}
}

% Sets the ISBN number (if not set, prints lines for space to the 10 digits to
% be written
\newlength{\@ISBNcolwidth}
\setlength{\@ISBNcolwidth}{.25em}
\newcommand{\@ISBN}{
    \begin{tabular}{*{13}{|p{\@ISBNcolwidth}}|}
        &&&&&&&&&\\
        \hline
    \end{tabular}
}
\newcommand{\ISBN}[1]{\renewcommand{\@ISBN}{\texttt{#1}}}

% Sets the advisor name (and title, optional, defaults to M)
\newcommand{\@advisor}{\textbf{!\texttt{advisor} \`a d\'efinir!}}
\newcommand{\@advisortitle}{M}
\newcommand{\advisor}[2][M]{
    \renewcommand{\@advisortitle}{#1}
    \renewcommand{\@advisor}{#2}
}
	
% Sets the coadvisor name (and title, optional, defaults to M)
\newcommand{\@coadvisor}{\textbf{!\texttt{coadvisor} \`a d\'efinir!}}
\newcommand{\@coadvisortitle}{M}
\newcommand{\coadvisor}[2][M]{
    \renewcommand{\@coadvisortitle}{#1}
    \renewcommand{\@coadvisor}{#2}
}

% Defines a member of the jury
\newcommand{\@jury}{}
\newcommand{\jury}[1]{\renewcommand{\@jury}{
\begin{tabular}{r@{ }ll}
#1
\end{tabular}
}}
\newcommand{\jurymember}[3][M]{#1. &#2, &#3}
\newcommand{\juryadvisor}[1][Directeur de th\`ese]{
    \jurymember[\@advisortitle]{\@advisor}{#1}
}
\newcommand{\jurycoadvisor}[1][Co-directeur de th\`ese]{
    \jurymember[\@coadvisortitle]{\@coadvisor}{#1}
}

\newcommand{\@labaddr}{}
\newcommand{\labaddr}[1]{
    \renewcommand{\@labaddr}{#1}
}
\newcommand{\@engtitle}{}
\newcommand{\engtitle}[1]{
    \renewcommand{\@engtitle}{#1}
}

\newcommand{\@resume}{}
\newcommand{\@abstract}{}
\newcommand{\resume}[2]{
    \renewcommand{\@resume}{#1}
    \renewcommand{\@abstract}{#2}
    \chapter{\@resumeapp}
    \@resume

    \ifthenelse{\equal{\@abstract}{}}{}{
        \@openrightfalse
        \chapter{\@abstractapp}
        \@openrighttrue
        \@abstract
    }
}

\newcommand{\@keywords}{}
\newcommand{\@engkeywords}{}
\newcommand{\keywords}[2]{
    \renewcommand{\@keywords}{#1}
    \renewcommand{\@engkeywords}{#2}
}

\newcommand{\@resumesize}{\small}
\newcommand{\resumesize}[1]{\renewcommand{\@resumesize}{#1}}
	
% redefine the \maketitle command
\renewcommand{\maketitle}{
    \begin{titlepage}
        \thispagestyle{empty}
%\geometry{nomarginpar,noheadfoot,twoside,showframe,
%    top=15mm,bottom=20mm,
%    hmargin=25mm,bindingoffset=10mm}
%        \vsize = 277mm
%        \voffset = -15mm
%        \topmargin = 0mm
%        \headheight = 0mm
%        \headsep = 0mm
%        \hsize = 160mm
%        \hoffset = -10mm
%        \vbox to \vsize {
            \begin{center}
                \textsc{\@university}
            \end{center}
            \vspace*{\stretch{1}}
            \begin{flushright}
                \parbox{6cm}{
                    \begin{center}
                        N{$^\circ$} attribu\'e par la biblioth\`eque\\
                        \texttt{\@ISBN}
                    \end{center}
                }
            \end{flushright}
            \vspace*{\stretch{1}}
            \begin{center}
                {\Large\textbf{TH\`ESE}}\\
                \vspace*{\stretch{2}}
                pour obtenir le grade de\\
                \vspace*{\stretch{1}}
                \textbf{\textsc{Docteur} de \@universityabbrv}\\
                \vspace*{\stretch{1}}
                Sp\'ecialit\'e : \textbf{\@speciality}\\
                \vspace*{\stretch{1}}
                pr\'epar\'ee au laboratoire \textbf{\@labo}\\
                \vspace*{\stretch{1}}
                dans le cadre de l'\'Ecole Doctorale \textbf{\@school}\\
                \vspace*{\stretch{2}}
                pr\'esent\'ee et soutenue publiquement\\
                par\\
                \vspace*{\stretch{3}}
                {\Large\textbf{\@author}}\\
                \vspace*{\stretch{3}}
                le \@date\\
                \vspace*{\stretch{5}}
                \@titleapp :\\
                {\large\textbf{\@title}}\\
                \vspace*{\stretch{5}}
                \@advisorapp : \textbf{\@advisor}\\
                \ifthenelse{\equal{\@coadvisor}{}}{}{
                    \@coadvisorapp : \textbf{\@coadvisor}\\
                }
                \vspace*{\stretch{8}}
                {\large \@juryapp}\\
                \@jury
            \end{center}
%        }
    \end{titlepage}
}

% Back page
\newcommand{\@backsection}[4][r]{%
    \ifthenelse{\equal{#3}{}}{%
    }{%
        \ifthenelse{\equal{#2}{}}{}{\noindent\textbf{\textsc{#2}}%
            \ifthenelse{\equal{#1}{r}}{\\}{}}%
        \ifthenelse{\equal{#1}{r}}{\indent}{\noindent}{#4{#3}}\\%
        \ifthenelse{\equal{#1}{r}}{%
            \vspace*{\stretch{1}}%
            \noindent\rule{\hsize}{1pt}%
            \vspace*{\stretch{1}}%
        }{}%
     }%
}
\newcommand{\makeback}{
    \begin{titlepage}
        \thispagestyle{empty}
        \null\clearpage
        \thispagestyle{empty}
%        \vsize = 277mm
%        \voffset = -15mm
%        \topmargin = 0mm
%        \headheight = 0mm
%        \headsep = 0mm
%        \hsize = 160mm
%        \hoffset = -10mm
%        \vbox to \vsize {
            \noindent\rule{\hsize}{1pt}
            \vspace*{\stretch{1}}
            \@backsection{\@resumeapp}{\@resume}{\@resumesize}
            \@backsection{\@keywordsapp}{\@keywords}{\@resumesize}
            \@backsection{\@engtitleapp}{\@title}{\bf}
            \@backsection{\@abstractapp}{\@abstract}{\@resumesize}
            \@backsection{\@engkeywordsapp}{\@engkeywords}{\@resumesize}
            \@backsection[]{Adrr : }{\@labaddr}{\@resumesize}%
            \@backsection[]{ISBN : }{\@ISBN}{}
%            \vspace*{\stretch{1}}
%            \noindent\textbf{\textsc{ISBN}} : {\@resumesize{\@ISBN}}
%            \noindent\textbf{\textsc{ISBN}} : {\@resumesize{\@ISBN}}
    \end{titlepage}
}

% fancy pagestyle redefinition
    \fancyhead[LE,RO]{\small\leftmark}
    \fancyhead[LO,C,RE]{}
    \fancyfoot[LE,RO]{\rm\thepage}
    \fancyfoot[LO,RE]{\small\rightmark}
    \fancyfoot[C]{}
% plain pagestyle redefinition
\fancypagestyle{plain}{
    \fancyhead[L,C,R]{}
    \fancyfoot[LE,RO]{\rm\thepage}
    \fancyfoot[LO,C,RE]{}
    \renewcommand{\headrulewidth}{0pt}
}
\pagestyle{fancy}

\renewcommand\thepart           {\@Roman\c@part}
\renewcommand\thechapter        {\@arabic\c@chapter}
\renewcommand\thesection        {\@arabic\c@section}
\renewcommand\thesubsection     {\thesection.\@arabic\c@subsection}
\renewcommand\thesubsubsection  {\thesubsection.\@arabic\c@subsubsection}
\renewcommand\theparagraph      {\thesubsubsection.\@arabic\c@paragraph}
\renewcommand\thesubparagraph   {\theparagraph.\@arabic\c@subparagraph}

\newcommand{\openany}{\@openrightfalse}
\newcommand{\openright}{\@openrighttrue}

\newif{\if@frontmatter}
\renewcommand{\frontmatter}{
    \cleardoublepage
    \@mainmatterfalse
    \@frontmattertrue
    \pagenumbering{roman}}
\renewcommand{\mainmatter}{
    \cleardoublepage
    \@mainmattertrue
    \@frontmatterfalse
    \pagenumbering{arabic}
}
\renewcommand{\backmatter}{
    \if@openright
        \cleardoublepage
    \else
        \clearpage
    \fi
    \@mainmatterfalse
    \@frontmatterfalse
}

\def\@chapter[#1]#2{
    \ifnum \c@secnumdepth >\m@ne
        \if@mainmatter
            \refstepcounter{chapter}
            \typeout{\@chapapp\space\thechapter.}
            \addcontentsline{toc}{chapter}
            {\protect\numberline{\thechapter}#1}
        \else
            \if@frontmatter
                \addcontentsline{toc}{section}{#1}
            \else
                \addcontentsline{toc}{chapter}{toto#1}
            \fi
        \fi
    \else
        \addcontentsline{toc}{chapter}{#1}
    \fi
    \chaptermark{#1}
    \addtocontents{lof}{\protect\addvspace{10\p@}}
    \addtocontents{lot}{\protect\addvspace{10\p@}}
    \if@twocolumn
        \@topnewpage[\@makechapterhead{#2}]
    \else
        \@makechapterhead{#2}
        \@afterheading
    \fi
}

\let\@oldschapter\@schapter
\def\@schapter#1{%
    \@oldschapter{#1}%
    \if@mainmatter
        \addcontentsline{toc}{chapter}{{#1}}
    \else
        \if@frontmatter
            \addcontentsline{toc}{section}{#1}
        \else
            \addcontentsline{toc}{chapter}{#1}
        \fi
    \fi
    \@mkboth{\MakeUppercase{#1}}{\MakeUppercase{#1}}
}

\if@blankemptypage
    %Redefine cleardoublepage so that the pages inserted are really empty
    \renewcommand{\cleardoublepage}{
        \clearpage
        \if@twoside
            \ifodd
                \c@page
            \else
                \null
                \thispagestyle{empty} %set style empty
                \newpage
                \if@twocolumn\null\newpage\fi
            \fi
        \fi
    }
\fi
