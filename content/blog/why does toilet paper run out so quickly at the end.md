+++
title = "Why does toilet paper run out quickly at the end"
author = "Sabiqul Hoque"
date = "2020-12-12"
tags = ["Derivation", "Graphs"]
categories = ["Mathematics"]
draft = "true"
+++

# The Problem

So one day, sitting on the toilet I found myself in the all too familiar conundrum: "Should I shout out for someone to bring me a new roll and at the same time bring dishonour and embarrassment to thyself".

![Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled.png](Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled.png)

More pertinent to this blog post, however was that I thought we had a somewhat thick toilet paper roll yesterday. Was someone hoarding toilet paper? But, doesn't it feel like toilet paper gets used up much more quickly towards the end of the roll than compared to the beginning? This is the question we shall answer in this blog post:

> Why does toilet paper feel like it runs out really fast near the end?

# The Solution

Some of you would already propose the answer as one of basic geometry. At the beginning, the radius of the toilet paper is large so one arc length carries a larger amount of toilet paper roll than compared to near the end. But have you bothered to do the maths behind it? No, didn't think so.

Let's set up some constants:

$$\ce{H2O <=> 2H+ + O2-}$$

![Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled%201.png](Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled%201.png)

- Code to generate image:

```latex
% !TeX program = lualatex
\documentclass[border=1cm]{standalone}

\usepackage{fontspec}
\setmainfont{Architects Daughter}
\RequirePackage{tikz}
\usepackage{ifthen}

\usetikzlibrary{calc,patterns,decorations,plotmarks,shapes.geometric}
\usepackage{pgfplots}
\pgfplotsset{compat=1.8}

\begin{document}


\pgfdeclaredecoration{penciline}{initial}{
\state{initial}[width=+\pgfdecoratedinputsegmentremainingdistance,
auto corner on length=1pt,
]{
\ifthenelse
{\pgfkeysvalueof{/tikz/penciline/jag ratio}=0} {
\pgfpathcurveto%
{% 1st control point
\pgfpoint
{\pgfdecoratedinputsegmentremainingdistance/2}
{2*rnd*\pgfdecorationsegmentamplitude}
}
{%% 2nd control point
\pgfpoint
%% Make sure random number is always between origin and target points
{\pgfdecoratedinputsegmentremainingdistance/2}
{2*rnd*\pgfdecorationsegmentamplitude}
}
{% 2nd point (1st one is implicit)
\pgfpointadd
{\pgfpointdecoratedinputsegmentlast}
{\pgfpoint{0*rand*1pt}{0*rand*1pt}}
}          
} {
\pgfpathcurveto%
{% 1st control point
\pgfpoint
{\pgfdecoratedinputsegmentremainingdistance*rnd*1pt}
{\pgfkeysvalueof{/tikz/penciline/jag ratio}*
rand*\pgfdecorationsegmentamplitude}
}
{%% 2nd control point
\pgfpoint
%% Make sure random number is always between origin and target points
{(.5+0.25*rand)*\pgfdecoratedinputsegmentremainingdistance}
{\pgfkeysvalueof{/tikz/penciline/jag ratio}*
rand*\pgfdecorationsegmentamplitude}
}
{% 2nd point (1st one is implicit)
\pgfpointadd
{\pgfpointdecoratedinputsegmentlast}
{\pgfpoint{rand*1pt}{rand*1pt}}
}
}
}
\state{final}{}
}




\tikzset{
penciline/.code={\pgfqkeys{/tikz/penciline}{#1}},
penciline={
jag ratio/.initial=5,
decoration/.initial = penciline,
},
penciline/.style = {
decorate,
%%decoration={\pgfkeysvalueof{/tikz/penciline/decoration}},
penciline/.cd,
#1,
/tikz/.cd,
},
decorate,
decoration={\pgfkeysvalueof{/tikz/penciline/decoration}},
}


\def\Grid{
\draw[penciline={jag ratio=6},style=help lines] (-2,-2) grid[step=1cm] (4,4);
}

\makeatletter
\pgfset{
/pgf/decoration/randomness/.initial=2,
/pgf/decoration/wavelength/.initial=100
}
\pgfdeclaredecoration{sketch}{init}{
\state{init}[width=0pt,next state=draw,persistent precomputation={
\pgfmathsetmacro\pgf@lib@dec@sketch@t0
}]{}
\state{draw}[width=\pgfdecorationsegmentlength,
auto corner on length=\pgfdecorationsegmentlength,
persistent precomputation={
\pgfmathsetmacro\pgf@lib@dec@sketch@t{mod(\pgf@lib@dec@sketch@t+pow(\pgfkeysvalueof{/pgf/decoration/randomness},rand),\pgfkeysvalueof{/pgf/decoration/wavelength})}
}]{
\pgfmathparse{sin(2*\pgf@lib@dec@sketch@t*pi/\pgfkeysvalueof{/pgf/decoration/wavelength} r)}
\pgfpathlineto{\pgfqpoint{\pgfdecorationsegmentlength}{\pgfmathresult\pgfdecorationsegmentamplitude}}
}
\state{final}{}
}
\tikzset{xkcd/.style={decorate,decoration={sketch,segment length=0.5pt,amplitude=0.5pt}}}
\makeatother

\pgfmathsetseed{1}

\begin{tikzpicture}
\node (a) [cylinder,draw,xkcd,shape aspect=3,minimum height=4cm,minimum width=3cm,thick] {};
\pgfmathsetseed{2}
\node (a) [cylinder,draw,xkcd,shape aspect=3,minimum height=4cm,minimum width=3cm] {};
\draw[penciline={jag ratio=0},thick] (1.54,0) -- (-1.76,0);
\draw[xkcd] (1.54,0) -- (-1.76,0);
\draw[xkcd,densely dashed] (2,0) -- (3.5,0);
\draw[xkcd,densely dashed] (2,1.5) -- (3.5,1.5);
\draw[penciline={jag ratio=1},|<->|] (3.7,1.5) -- (3.7,0) node[midway,right] {R};
\draw[xkcd,|<->|,thick] (3.7,1.5) -- (3.7,0);
\draw[latex-,penciline={jag ratio=0},thick] (1,-1.5) .. controls +(-90:0.7) and +(180:0.6) .. +(1.5,-1) node[right] {Amount still in roll: L};
\draw[latex-,penciline={jag ratio=0}] (1,-1.5) .. controls +(-90:0.7) and +(180:0.6) .. +(1.5,-1);
\end{tikzpicture}


\end{document}
```

For now, let's just pretend there is no hole through the middle. I also lied, $L$ is not a constant but is a variable. Let's set up the remaining of the variables:

![Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled%202.png](Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled%202.png)

- Code to generate image

```latex
% !TeX program = lualatex
\documentclass[border=1cm]{standalone}

\usepackage{fontspec}
\setmainfont{Architects Daughter}
\RequirePackage{tikz}
\usepackage{ifthen}

\usetikzlibrary{calc,patterns,decorations,plotmarks,shapes.geometric}
\usepackage{pgfplots}
\pgfplotsset{compat=1.8}

\begin{document}


\pgfdeclaredecoration{penciline}{initial}{
\state{initial}[width=+\pgfdecoratedinputsegmentremainingdistance,
auto corner on length=1pt,
]{
\ifthenelse
{\pgfkeysvalueof{/tikz/penciline/jag ratio}=0} {
\pgfpathcurveto%
{% 1st control point
\pgfpoint
{\pgfdecoratedinputsegmentremainingdistance/2}
{2*rnd*\pgfdecorationsegmentamplitude}
}
{%% 2nd control point
\pgfpoint
%% Make sure random number is always between origin and target points
{\pgfdecoratedinputsegmentremainingdistance/2}
{2*rnd*\pgfdecorationsegmentamplitude}
}
{% 2nd point (1st one is implicit)
\pgfpointadd
{\pgfpointdecoratedinputsegmentlast}
{\pgfpoint{0*rand*1pt}{0*rand*1pt}}
}          
} {
\pgfpathcurveto%
{% 1st control point
\pgfpoint
{\pgfdecoratedinputsegmentremainingdistance*rnd*1pt}
{\pgfkeysvalueof{/tikz/penciline/jag ratio}*
rand*\pgfdecorationsegmentamplitude}
}
{%% 2nd control point
\pgfpoint
%% Make sure random number is always between origin and target points
{(.5+0.25*rand)*\pgfdecoratedinputsegmentremainingdistance}
{\pgfkeysvalueof{/tikz/penciline/jag ratio}*
rand*\pgfdecorationsegmentamplitude}
}
{% 2nd point (1st one is implicit)
\pgfpointadd
{\pgfpointdecoratedinputsegmentlast}
{\pgfpoint{rand*1pt}{rand*1pt}}
}
}
}
\state{final}{}
}




\tikzset{
penciline/.code={\pgfqkeys{/tikz/penciline}{#1}},
penciline={
jag ratio/.initial=5,
decoration/.initial = penciline,
},
penciline/.style = {
decorate,
%%decoration={\pgfkeysvalueof{/tikz/penciline/decoration}},
penciline/.cd,
#1,
/tikz/.cd,
},
decorate,
decoration={\pgfkeysvalueof{/tikz/penciline/decoration}},
}


\def\Grid{
\draw[penciline={jag ratio=6},style=help lines] (-2,-2) grid[step=1cm] (4,4);
}

\makeatletter
\pgfset{
/pgf/decoration/randomness/.initial=2,
/pgf/decoration/wavelength/.initial=100
}
\pgfdeclaredecoration{sketch}{init}{
\state{init}[width=0pt,next state=draw,persistent precomputation={
\pgfmathsetmacro\pgf@lib@dec@sketch@t0
}]{}
\state{draw}[width=\pgfdecorationsegmentlength,
auto corner on length=\pgfdecorationsegmentlength,
persistent precomputation={
\pgfmathsetmacro\pgf@lib@dec@sketch@t{mod(\pgf@lib@dec@sketch@t+pow(\pgfkeysvalueof{/pgf/decoration/randomness},rand),\pgfkeysvalueof{/pgf/decoration/wavelength})}
}]{
\pgfmathparse{sin(2*\pgf@lib@dec@sketch@t*pi/\pgfkeysvalueof{/pgf/decoration/wavelength} r)}
\pgfpathlineto{\pgfqpoint{\pgfdecorationsegmentlength}{\pgfmathresult\pgfdecorationsegmentamplitude}}
}
\state{final}{}
}
\tikzset{xkcd/.style={decorate,decoration={sketch,segment length=0.5pt,amplitude=0.5pt}}}
\makeatother

\pgfmathsetseed{1}

\begin{tikzpicture}
\node (a) [cylinder,draw,xkcd,shape aspect=3,minimum height=4cm,minimum width=2.5cm] {};
\pgfmathsetseed{2}
\node (a) [cylinder,draw,xkcd,thick,shape aspect=3,minimum height=4cm,minimum width=2.5cm] {};
\draw[xkcd,white,fill=white] (1.54,0) rectangle (-1.76,-2);
\draw[penciline={jag ratio=0},thick] (1.54,0) |- (-1.76,-2) -- (-1.76,0);
\draw[penciline={jag ratio=0}] (1.54,0) |- (-1.76,-2) -- (-1.76,0);
\draw[penciline={jag ratio=0},densely dotted] (-1.76,0) -- (1.54,0);
\draw[xkcd,densely dashed] (2,0) -- (3.5,0);
\draw[xkcd,densely dashed] (2,1.25) -- (3.5,1.25);
\draw[xkcd,|<->|,thick] (3.7,1.25) -- (3.7,0) node[midway,right] {h};
\draw[penciline={jag ratio=1},|<->|] (3.7,1.25) -- (3.7,0);
\draw[xkcd,|<->|,thick] (-1.96,0) -- (-1.96,-2) node[midway,left] {l};
\draw[penciline={jag ratio=1},|<->|] (-1.96,0) -- (-1.96,-2);
\draw[xkcd,-latex] (-0.11,-2.1) -- (-0.11,-2.7) node[below] {v};
\pgfmathsetseed{3}
\draw[xkcd,-latex] (-0.11,-2.1) -- (-0.11,-2.7);
\draw[latex-,penciline={jag ratio=0},thick] (1.65,-1.25) .. controls +(-90:0.7) and +(180:0.6) .. +(1.5,-1) node[right] {Amount still in roll: L};
\draw[latex-,penciline={jag ratio=0}] (1.65,-1.25) .. controls +(-90:0.7) and +(180:0.6) .. +(1.5,-1);
\end{tikzpicture}


\end{document}
```

Where $v=\frac{dl}{dt}$, is a constant and is the speed at which you use the toilet paper

The only real way to explain this mathematically is find a function of $h$ against $l$ and a function for $h$ against $t$ and plot these as well. 

It should be apparent that the following equations holds:

$$\begin{aligned}l+L&=\text{Total length in roll}\;(P)\\v&=\frac{dl}{dt}=-\frac{dL}{dt}\end{aligned}$$

Let's switch to a side view

![Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled%203.png](Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled%203.png)

- Code to generate image

```latex
% !TeX program = lualatex
\documentclass[border=1cm]{standalone}

\usepackage{fontspec}
\setmainfont{Architects Daughter}
\RequirePackage{tikz}
\usepackage{ifthen}

\usetikzlibrary{calc,patterns,decorations,plotmarks}
\usepackage{pgfplots}
\pgfplotsset{compat=1.8}

\begin{document}


\pgfdeclaredecoration{penciline}{initial}{
\state{initial}[width=+\pgfdecoratedinputsegmentremainingdistance,
auto corner on length=1pt,
]{
\ifthenelse
{\pgfkeysvalueof{/tikz/penciline/jag ratio}=0} {
\pgfpathcurveto%
{% 1st control point
\pgfpoint
{\pgfdecoratedinputsegmentremainingdistance/2}
{2*rnd*\pgfdecorationsegmentamplitude}
}
{%% 2nd control point
\pgfpoint
%% Make sure random number is always between origin and target points
{\pgfdecoratedinputsegmentremainingdistance/2}
{2*rnd*\pgfdecorationsegmentamplitude}
}
{% 2nd point (1st one is implicit)
\pgfpointadd
{\pgfpointdecoratedinputsegmentlast}
{\pgfpoint{0*rand*1pt}{0*rand*1pt}}
}          
} {
\pgfpathcurveto%
{% 1st control point
\pgfpoint
{\pgfdecoratedinputsegmentremainingdistance*rnd*1pt}
{\pgfkeysvalueof{/tikz/penciline/jag ratio}*
rand*\pgfdecorationsegmentamplitude}
}
{%% 2nd control point
\pgfpoint
%% Make sure random number is always between origin and target points
{(.5+0.25*rand)*\pgfdecoratedinputsegmentremainingdistance}
{\pgfkeysvalueof{/tikz/penciline/jag ratio}*
rand*\pgfdecorationsegmentamplitude}
}
{% 2nd point (1st one is implicit)
\pgfpointadd
{\pgfpointdecoratedinputsegmentlast}
{\pgfpoint{rand*1pt}{rand*1pt}}
}
}
}
\state{final}{}
}




\tikzset{
penciline/.code={\pgfqkeys{/tikz/penciline}{#1}},
penciline={
jag ratio/.initial=5,
decoration/.initial = penciline,
},
penciline/.style = {
decorate,
%%decoration={\pgfkeysvalueof{/tikz/penciline/decoration}},
penciline/.cd,
#1,
/tikz/.cd,
},
decorate,
decoration={\pgfkeysvalueof{/tikz/penciline/decoration}},
}


\def\Grid{
\draw[penciline={jag ratio=6},style=help lines] (-2,-2) grid[step=1cm] (4,4);
}

\makeatletter
\pgfset{
/pgf/decoration/randomness/.initial=2,
/pgf/decoration/wavelength/.initial=100
}
\pgfdeclaredecoration{sketch}{init}{
\state{init}[width=0pt,next state=draw,persistent precomputation={
\pgfmathsetmacro\pgf@lib@dec@sketch@t0
}]{}
\state{draw}[width=\pgfdecorationsegmentlength,
auto corner on length=\pgfdecorationsegmentlength,
persistent precomputation={
\pgfmathsetmacro\pgf@lib@dec@sketch@t{mod(\pgf@lib@dec@sketch@t+pow(\pgfkeysvalueof{/pgf/decoration/randomness},rand),\pgfkeysvalueof{/pgf/decoration/wavelength})}
}]{
\pgfmathparse{sin(2*\pgf@lib@dec@sketch@t*pi/\pgfkeysvalueof{/pgf/decoration/wavelength} r)}
\pgfpathlineto{\pgfqpoint{\pgfdecorationsegmentlength}{\pgfmathresult\pgfdecorationsegmentamplitude}}
}
\state{final}{}
}
\tikzset{xkcd/.style={decorate,decoration={sketch,segment length=0.5pt,amplitude=0.5pt}}}
\makeatother

\pgfmathsetseed{1}

\begin{tikzpicture}[penciline={jag ratio=2},scale=0.7]
\draw [domain=0:25.1327,variable=\t,samples=190,rotate=180,xkcd,thick] plot ({\t r}:{0.1591549431*\t});
\draw [domain=0:25.1327,variable=\t,samples=35,smooth,rotate=180,penciline={jag ratio=1}] plot ({\t r}:{0.1591549431*\t});
\draw[thick,penciline={jag ratio=1},thick] (-4,0) -- (-4,-3) -- (-3,-3) -- (-3,0);
\draw[penciline={jag ratio=0}] (-4,0) -- (-4,-3) -- (-3,-3) -- (-3,0);
\draw[penciline={jag ratio=1},|<->|,thick] (-4,-3.4) -- (-3,-3.4) node[midway,below] {T};
\draw[penciline={jag ratio=1},|<->|] (-4,-3.4) -- (-3,-3.4);
\draw[penciline={jag ratio=1},|<->|,thick] (-4.3,-3) -- (-4.3,0) node[midway,left] {l};
\draw[penciline={jag ratio=1},|<->|] (-4.3,-3) -- (-4.3,0);
\end{tikzpicture}


\end{document}
```

The spiral of the toilet paper can be represented by the formula $h=\frac{\theta}{2\pi}\times T$ where $T$ is the thickness of the toilet paper as shown below:

![Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled%204.png](Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled%204.png)

Unfortunately, I couldn't change the font of the maths. I decided to keep the spiral perfect because it's a graph

- Code to generate image

```latex
% !TeX program = lualatex
\documentclass[border={5pt 5pt 5pt 5pt}]{standalone} %left bottom right top

\usepackage{fontspec}
\setmainfont{Architects Daughter}
\usepackage{tikz}
\usetikzlibrary{calc,decorations,patterns,arrows,decorations.pathmorphing,3d,shapes.geometric}
\definecolor{pltblue}{HTML}{1F77B4}

\makeatletter
\pgfset{
/pgf/decoration/randomness/.initial=2,
/pgf/decoration/wavelength/.initial=100
}
\pgfdeclaredecoration{sketch}{init}{
\state{init}[width=0pt,next state=draw,persistent precomputation={
\pgfmathsetmacro\pgf@lib@dec@sketch@t0
}]{}
\state{draw}[width=\pgfdecorationsegmentlength,
auto corner on length=\pgfdecorationsegmentlength,
persistent precomputation={
\pgfmathsetmacro\pgf@lib@dec@sketch@t{mod(\pgf@lib@dec@sketch@t+pow(\pgfkeysvalueof{/pgf/decoration/randomness},rand),\pgfkeysvalueof{/pgf/decoration/wavelength})}
}]{
\pgfmathparse{sin(2*\pgf@lib@dec@sketch@t*pi/\pgfkeysvalueof{/pgf/decoration/wavelength} r)}
\pgfpathlineto{\pgfqpoint{\pgfdecorationsegmentlength}{\pgfmathresult\pgfdecorationsegmentamplitude}}
}
\state{final}{}
}
\tikzset{xkcd/.style={decorate,decoration={sketch,segment length=0.5pt,amplitude=0.5pt}}}
\makeatother

\pgfmathsetseed{1}

\pagestyle{empty}

\usepackage{chemfig}
%\usepackage{mol2chemfig}
\usepackage{amsmath}
\usepackage{amsfonts}
\usepackage{amssymb}
\usepackage{mhchem}
\usepackage{pgfplots}
\usepgfplotslibrary{polar}
\begin{document}

\begin{tikzpicture}
\draw [domain=0:25.1327,variable=\t,smooth,samples=85,rotate=0,thick] plot ({\t r}:{0.1591549431*\t});
\draw[-latex,xkcd] (-5,0) -- (5,0);
\draw[-latex,xkcd] (0,-5) -- (0,5);
\node[below right] at (1,0) {T};
\node[below right] at (2,0) {2T};
\node[below right] at (3,0) {3T};
\node[below right] at (4,0) {4T};
\draw[xkcd] (0,0) -- (45:2.125);
\node[above left] at (45:1.625) {r};
\draw (0:0.4) arc (0:45:0.4);
\node at (22.5:0.6) {$\theta$};
\node at (2,4) {$r=\frac{T}{2\pi}\theta$};
\end{tikzpicture}

\end{document}
```

Hence we are able to get that:

$$\begin{aligned} h=\frac{\theta}{2\pi}\times T &&&& \theta=\frac{2\pi}{T}\times h\end{aligned}$$

If we take a small slice like so:

![Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled%205.png](Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled%205.png)

As $\delta\theta\to0$, the slice approximates a sector in a circle, and so the two straight sides become approximately equal. Hence we can label both sides as $h$.

- Code to generate image

```latex
% !TeX program = lualatex
\documentclass[border=1cm]{standalone}

\usepackage{fontspec}
\setmainfont{Architects Daughter}
\RequirePackage{tikz}
\usepackage{ifthen}
\definecolor{pltblue}{HTML}{1F77B4}

\usetikzlibrary{calc,patterns,decorations,plotmarks}
\usepackage{pgfplots}
\pgfplotsset{compat=1.8}

\begin{document}


\pgfdeclaredecoration{penciline}{initial}{
\state{initial}[width=+\pgfdecoratedinputsegmentremainingdistance,
auto corner on length=1pt,
]{
\ifthenelse
{\pgfkeysvalueof{/tikz/penciline/jag ratio}=0} {
\pgfpathcurveto%
{% 1st control point
\pgfpoint
{\pgfdecoratedinputsegmentremainingdistance/2}
{2*rnd*\pgfdecorationsegmentamplitude}
}
{%% 2nd control point
\pgfpoint
%% Make sure random number is always between origin and target points
{\pgfdecoratedinputsegmentremainingdistance/2}
{2*rnd*\pgfdecorationsegmentamplitude}
}
{% 2nd point (1st one is implicit)
\pgfpointadd
{\pgfpointdecoratedinputsegmentlast}
{\pgfpoint{0*rand*1pt}{0*rand*1pt}}
}          
} {
\pgfpathcurveto%
{% 1st control point
\pgfpoint
{\pgfdecoratedinputsegmentremainingdistance*rnd*1pt}
{\pgfkeysvalueof{/tikz/penciline/jag ratio}*
rand*\pgfdecorationsegmentamplitude}
}
{%% 2nd control point
\pgfpoint
%% Make sure random number is always between origin and target points
{(.5+0.25*rand)*\pgfdecoratedinputsegmentremainingdistance}
{\pgfkeysvalueof{/tikz/penciline/jag ratio}*
rand*\pgfdecorationsegmentamplitude}
}
{% 2nd point (1st one is implicit)
\pgfpointadd
{\pgfpointdecoratedinputsegmentlast}
{\pgfpoint{rand*1pt}{rand*1pt}}
}
}
}
\state{final}{}
}




\tikzset{
penciline/.code={\pgfqkeys{/tikz/penciline}{#1}},
penciline={
jag ratio/.initial=5,
decoration/.initial = penciline,
},
penciline/.style = {
decorate,
%%decoration={\pgfkeysvalueof{/tikz/penciline/decoration}},
penciline/.cd,
#1,
/tikz/.cd,
},
decorate,
decoration={\pgfkeysvalueof{/tikz/penciline/decoration}},
}


\def\Grid{
\draw[penciline={jag ratio=6},style=help lines] (-2,-2) grid[step=1cm] (4,4);
}

\makeatletter
\pgfset{
/pgf/decoration/randomness/.initial=2,
/pgf/decoration/wavelength/.initial=100
}
\pgfdeclaredecoration{sketch}{init}{
\state{init}[width=0pt,next state=draw,persistent precomputation={
\pgfmathsetmacro\pgf@lib@dec@sketch@t0
}]{}
\state{draw}[width=\pgfdecorationsegmentlength,
auto corner on length=\pgfdecorationsegmentlength,
persistent precomputation={
\pgfmathsetmacro\pgf@lib@dec@sketch@t{mod(\pgf@lib@dec@sketch@t+pow(\pgfkeysvalueof{/pgf/decoration/randomness},rand),\pgfkeysvalueof{/pgf/decoration/wavelength})}
}]{
\pgfmathparse{sin(2*\pgf@lib@dec@sketch@t*pi/\pgfkeysvalueof{/pgf/decoration/wavelength} r)}
\pgfpathlineto{\pgfqpoint{\pgfdecorationsegmentlength}{\pgfmathresult\pgfdecorationsegmentamplitude}}
}
\state{final}{}
}
\tikzset{xkcd/.style={decorate,decoration={sketch,segment length=0.5pt,amplitude=0.5pt}}}
\makeatother

\pgfmathsetseed{1}

\begin{tikzpicture}[penciline={jag ratio=2},scale=0.45]
\draw [domain=0:25.1327,variable=\t,samples=190,rotate=180,xkcd,thick] plot ({\t r}:{0.1591549431*\t});
\draw [domain=0:25.1327,variable=\t,samples=35,smooth,rotate=180,penciline={jag ratio=1}] plot ({\t r}:{0.1591549431*\t});
\draw[thick,penciline={jag ratio=1},thick] (-4,0) -- (-4,-3) -- (-3,-3) -- (-3,0);
\draw[penciline={jag ratio=0}] (-4,0) -- (-4,-3) -- (-3,-3) -- (-3,0);
\draw[xkcd,|<->|,thick] (-4,-3.4) -- (-3,-3.4) node[midway,below] {T};
\draw[penciline={jag ratio=1},|<->|] (-4,-3.4) -- (-3,-3.4);
\draw[penciline={jag ratio=1},|<->|,thick] (-4.3,-3) -- (-4.3,0) node[midway,left] {l};
\draw[penciline={jag ratio=1},|<->|] (-4.3,-3) -- (-4.3,0);

\draw[thick,fill=pltblue,fill opacity=.7,yshift=-0.2cm,penciline={jag ratio=1}] (0,0) -- (95:4.2638888889) arc (95:85:4.2638888889) -- (0,0);
\draw[yshift=-0.2cm,penciline={jag ratio=1}] (0,0) -- (95:4.2638888889) arc (95:85:4.2638888889) -- (0,0);

\begin{scope}[xshift=5cm]
\draw[penciline={jag ratio=0},thick] (0,-5) rectangle (5,5);
\draw[penciline={jag ratio=1}] (0,-5) rectangle (5,5);
\node[inner sep=0pt] (A) at (0,3) {};
\draw[penciline={jag ratio=1},thick,fill=pltblue,fill opacity=.7] (2.5,-4.5) -- +(85:8) node[midway,right,fill opacity=1] {h} arc (85:95:9) node[midway,above,fill opacity=1] {$\delta$L} -- cycle node[midway,left,fill opacity=1] {h};
\draw[penciline={jag ratio=1}] (2.5,-4.5) -- +(85:8) arc (85:95:9)  -- cycle;
\draw[thick] (2.5,-4.5) +(85:2) arc (85:95:2);
\draw[xkcd] (2.5,-2.5) .. controls +(90:1) and +(180:0.5) .. +(1,-0.5) node[right] {$\delta\theta$};
\end{scope}

\draw[-latex,xkcd,thick] (90:4.0638888889) .. controls +(90:1.5) and +(-170:1.5) .. (A);
\pgfmathsetseed{2}
\draw[-latex,xkcd] (90:4.0638888889) .. controls +(90:1.5) and +(-170:1.5) .. (A);
\end{tikzpicture}


\end{document}
```

Using the arc length formula:

$$\delta L=h\cdot\delta\theta$$

Substituting in and continuing on we find that:

$$\begin{aligned}\int dL&=\int h\;d\theta\\L&=\int\frac{\theta}{2\pi}\times T\;d\theta\\&=\frac{\theta^2 T}{4\pi}+C\end{aligned}$$

Remember how I said to pretend that there is no hole in the middle. Well that means that when the length of toilet paper in the roll is 0 (i.e. it is empty, $L=0$), that $\theta=0$. Therefore, $C=0$.

If we substitute in $\theta=\frac{2\pi h}{T}$ into the equation we get:

$$\begin{aligned}L&=\frac{\theta^2T}{4\pi}\\&=\left(\frac{2\pi h}{T}\right)^2\times\frac{T}{4\pi}\\&=\frac{4\pi^2h^2}{T^2}\times\frac{T}{4\pi}\\&=\frac{\pi h^2}{T}\end{aligned}$$

Rearranging to make $h$ the subject:

$$h=\sqrt{\frac{TL}{\pi}}$$

Remember how the total length of the roll, $P$ can be given by: $P=L+l$, so $L=P-l$. So, 

$$h=\sqrt{\frac{T\left(P-l\right)}{\pi}}$$

To accommodate for the hole in the middle, we can set it so that $h\in \text{I\!R},\;h\ge r$

, where $r$ is the radius of the inner hole.

![Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled%206.png](Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled%206.png)

Decided against the cartoon look since its a graph

- Code to generate diagram

```latex
% !TeX program = lualatex
\documentclass[border={5pt 5pt 5pt 5pt}]{standalone} %left bottom right top

\usepackage{tikz}
\usepackage{pgfplots}

\begin{document}
\begin{tikzpicture}
\begin{axis}[
title={$h=\sqrt{\frac{T(P-l)}{\pi}}$},
width=10cm,height=5cm,
ymin=0,ymax=2.5,
xmin=0,xmax=2.25,
axis lines=left,
ytick={0,0.5,2},
yticklabels={0,$r$,$\sqrt{\frac{TP}{\pi}}$},
ylabel=$h$,
xlabel=$l$,
every axis x label/.style={
at={(ticklabel* cs:1.05)},
anchor=west,
},
every axis y label/.style={
at={(ticklabel* cs:1.05)},
anchor=south,
},
xtick={0,1.875},
xticklabels={0,$P-\frac{h^2\pi}{T}$}
]
\addplot[
black,
no markers,
samples=50,
domain=0:1.875
] 
{sqrt(4-2*x)};

\draw[densely dotted] (axis cs:0,0.5) -- (axis cs:2.25,0.5);

\draw[latex-] (axis cs:1,1.414) .. controls +(50:4) and +(-4,0) .. +(25,30) node [right,align=left] {$h$ decreases more\\rapidly as $l$ increases};
\end{axis}
\end{tikzpicture}
\end{document}
```

If we are pulling out the length of toilet paper at a constant rate, $v$ and we want to find the function for $h$ as it changes with time, $t$, we can integrate the equation for $\frac{dh}{dt}$.

$$\begin{aligned}\frac{dh}{dt}&=\frac{dh}{dL}\times\frac{dL}{dt}\end{aligned}$$

We can find $\frac{dh}{dL}$:

$$\begin{aligned}L&=\frac{\pi h^2}{T}\\\frac{dL}{dh}&=\frac{2\pi h}{T}\\\frac{dh}{dL}&=\frac{T}{2\pi h}\end{aligned}$$

And as stated before:

$$\frac{dL}{dt}=-v$$

So,

$$\begin{aligned}
\frac{dh}{dt}&=\frac{T}{2\pi h}\times -v\\
h\;dh&=\frac{-vT}{2\pi}\;dt\\
\int h\;dh&=\int\frac{-vT}{2\pi}\;dt\\
\frac{h^2}{2}&=\frac{-vT}{2\pi}t+c_1\\
h^2&=\frac{-vT}{\pi}t+c_2
\end{aligned}$$

Initially at $t=0$, $h=R$ as none of the roll has been used, so

$$\begin{aligned}R^2&=0+c_2\\\therefore\quad c_2&=R^2\end{aligned}$$

So we get,

$$\begin{aligned}h^2&=\frac{-vT}{\pi}t+ R^2\\h&=\sqrt{\frac{-vT}{\pi}t+ R^2}\end{aligned}$$

This looks as follows:

![Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled%207.png](Why%20does%20toilet%20paper%20feel%20like%20it%20runs%20out%20really%2033066541cba94699b90921b20fe24dc0/Untitled%207.png)

- Code used to generate image

```latex
% !TeX program = lualatex
\documentclass[border={5pt 5pt 5pt 5pt}]{standalone} %left bottom right top

\usepackage{tikz}
\usepackage{pgfplots}

\begin{document}
\begin{tikzpicture}
\begin{axis}[
title={$h=\sqrt{\frac{-vT}{\pi}t+R^2}$},
width=10cm,height=5cm,
ymin=0,ymax=2.5,
xmin=0,xmax=2.25,
axis lines=left,
ytick={0,0.5,2},
yticklabels={0,$r$,R},
ylabel=$h$,
xlabel=$t$,
every axis x label/.style={
at={(ticklabel* cs:1.05)},
anchor=west,
},
every axis y label/.style={
at={(ticklabel* cs:1.05)},
anchor=south,
},
xtick={0,1.875},
xticklabels={0,$\frac{(R^2-r^2)\cdot\pi}{vT}$}
]
\addplot[
black,
no markers,
samples=50,
domain=0:1.875
] 
{sqrt(4-2*x)};

\draw[densely dotted] (axis cs:0,0.5) -- (axis cs:2.25,0.5);

\draw[latex-] (axis cs:1,1.414) .. controls +(50:4) and +(-4,0) .. +(25,30) node [right,align=left] {$h$ decreases more\\rapidly as $t$ increases};
\end{axis}
\end{tikzpicture}
\end{document}
```

An important thing to note is that at $t=0$, no amount of toilet paper has been used so $l=0$ and $h=R$. This all means that $h=R=\sqrt{\frac{T(P-0)}{\pi}}=\sqrt{\frac{TP}{\pi}}$. Also, both graphs become identical if $v=1$ which is to be expected.

# Your Own Playable Graph

Here is your own graph for you to play through (if you prefer links, you can use this link below)

[Toilet Paper Roll Graphs](https://www.desmos.com/calculator/6deixmhsjt)

[https://www.desmos.com/calculator/6deixmhsjt](https://www.desmos.com/calculator/6deixmhsjt)

<div>
<iframe src="https://www.desmos.com/calculator/htg8xs7om3?embed" width="500" height="500" style="border: 1px solid #ccc" frameborder=0></iframe>
</div>
