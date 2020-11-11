Глеб М. @ 00:44 29.10.2020

Искал проблему, почему при использовании сносок в поле `author` класса `article` сноска странно нумеруется и не создаётся ссылка (за неё вроде бы отвечает пакет `hyperref`).

## Повторное использование сносок

Нашёл на [tex.stackexchange.com](https://tex.stackexchange.com/) интересный вариант, как повторно использовать ссылку на сноску несколько раз. [Ссыль.](https://tex.stackexchange.com/a/1807) Там даётся очень интересный код:
```tex
\documentclass{article}
\usepackage{hyperref}

\newcommand{\footremember}[2]{%
   \footnote{#2}
    \newcounter{#1}
    \setcounter{#1}{\value{footnote}}%
}

\newcommand{\footrecall}[1]{%
    \footnotemark[\value{#1}]%
} 

\title{How to bowl properly}

\author{%
    The Dude\footremember{alley}{Holly Star Lanes Bowling Alley}%
    \and Walter Sobchak\footremember{trailer}{probably in a trailer park}%
    \and Jesus Quintana\footrecall{alley} \footnote{Mexico?}%
    \and Uli Kunkel\footrecall{trailer} \footnote{Germany?}%
}

\begin{document}
    \maketitle
    The whole example is taken from \href{http://anthony.liekens.net/index.php/LaTeX/MultipleFootnoteReferences}{anthony liekens}\ldots
\end{document}
```
Функция `\footremember{#1}{#2}` принимает в качестве аргумента `#1` метку-идентификатор для сноски, а в качестве `#2` &mdash; тело сноски. Уже функция `\footrecall{#1}` принимает только метку и вставляет присвоенное данной сноске значение.

Прикольно, но почему-то всё равно старые проблемы не исчезают.

Не разобрался, забил. Не так всё ужасно.