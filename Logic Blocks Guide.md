---
title-meta: Logic Blocks Guide
author-meta: ALVAROPING1#6682
lang: en

mainfont: Calibri.ttf
mainfontoptions:
- Extension=.ttf
- UprightFont=*
- BoldFont=*b
- ItalicFont=*i
- BoldItalicFont=*z

fontsize: 12pt

# For some reason, boxlinks is necessary for colorlinks to work even though it shouldn't have any effect when colorlinks is set
boxlinks: true
linkcolor: hyperlinkBlue
urlcolor: hyperlinkBlue

geometry: "left=3cm,right=3cm,top=2.5cm,bottom=2.5cm"

header-includes: |
    ```{=latex}
    % Fonts
    \setmathfont{Cambria Math}
    \parskip=3.5pt

    % Hyperlink color
    \definecolor{hyperlinkBlue}{RGB}{5,99,193}

    % Custom horizontal line width on tables (tabular/aligned)
    \usepackage{booktabs}
    \aboverulesep=0ex
    \belowrulesep=0ex
    \newcommand\HLine[1]{\specialrule{#1}{0pt}{0pt}}

    % Multi page tables
    \usepackage{longtable}

    % Multi line table cells
    \usepackage{makecell}
    \renewcommand\theadfont{\bfseries}

    % Increase table cell height
    \renewcommand{\arraystretch}{1.4}

    % Increase table header height
    \renewcommand\theadgape{\Gape[5pt]}

    % Merge rows/columns in tables
    \usepackage{multirow}

    % Vertically center table cells
    \usepackage{array}

    % Custom list labels
    \newcommand{\LabelItemI}{\labelitemfont \textbullet}
    \newcommand{\LabelItemII}{\labelitemfont \bfseries \textendash}
    \newcommand{\LabelItemIII}{\labelitemfont \rule[0.5ex]{0.6ex}{0.6ex}}
    \newcommand{\LabelItemIV}{\labelitemfont \textasteriskcentered}

    % Increase max nesting depth for lists
    \usepackage{enumitem}
    
    \setlistdepth{5}

    \setlist[itemize]{leftmargin=2em}
    \setlist[itemize,1]{label=\LabelItemI, leftmargin=2.5em}
    \setlist[itemize,2]{label=\LabelItemII}
    \setlist[itemize,3]{label=\LabelItemIII}
    \setlist[itemize,4]{label=\LabelItemIV}
    \setlist[itemize,5]{label=\LabelItemI}
    
    \renewlist{itemize}{itemize}{5}

    % Diagrams
    \usepackage{tikz}
    \usetikzlibrary{positioning, fit, calc, arrows.meta, backgrounds, decorations.markings}
    % Basic node style
    \tikzset{rectangleNode/.style={rectangle, draw=black, fill=white, thick, minimum height=6.6mm}}
    % Node style for image annotations
    \tikzset{annotation/.style={rectangleNode, align=left}}
    % Node style for diagram nodes
    \tikzset{node/.style={rectangleNode, align=center, minimum width=30.4mm}}
    % Node style for hidden diagram nodes
    \tikzset{hiddenNode/.style={rectangleNode, draw=none, fill=none, minimum width=5mm}}
    % Style for lines
    \tikzset{line/.style={-, thick}}
    % Style for arrows
    \tikzset{arrow/.style={-Triangle, thick}}
    % Style for arrows with the tip on the middle
    \tikzset{->-/.style={line, decoration={markings, mark=at position 0.5 with {\arrow{Triangle}}}, postaction={decorate}}}

    % Plot graphs
    \usepackage{pgfplots}
    \pgfplotsset{every axis plot/.append style={very thick}}

    % Images location
    \graphicspath{ {img/} }

    % Ceiling function
    \usepackage{mathtools}
    \DeclarePairedDelimiter{\ceil}{\lceil}{\rceil}

    \newcommand{\TOCLabelI}{\large \color{black}}
    \newcommand{\TOCLabelII}{\hspace{-0.225em} \color{black} \LabelItemI \hspace{0.5em}}
    \newcommand{\TOCLabelIII}{\hspace{-0.305em} \color{black} \LabelItemIII \hspace{0.5em}}

    \newcommand{\TitleFormat}[1]{\centering \LARGE \underline{#1}}
    \newcommand{\TitleFormatI}[1]{\Large \underline{#1}}
    \newcommand{\TitleFormatII}[1]{\large #1}
    ```
---

# \TitleFormat{Logic Blocks Guide} {.unlisted .unnumbered}

\vspace{1mm}
\begin{center}
\includegraphics[width=\linewidth]{thumbnail}
\end{center}

\tableofcontents
\clearpage

\newcommand{\titleA}{Settings}
\phantomsection
\addcontentsline{toc}{section}{\TOCLabelI \titleA}

## \TitleFormatI{\titleA} {.unlisted .unnumbered}

\newcommand{\titleAA}{Distance Sensor}
\phantomsection
\addcontentsline{toc}{subsection}{\TOCLabelII \titleAA}

- **\TitleFormatII{\titleAA}**
  - Range: in meters, $1 \text{ block} = 0.25 \text{ m}$
  - Output value: from $-1$ to $1$
  - Trigger
    - Normal: sends an output when it detects something
    - Inverted: sends an output when it detects nothing
  - Outputs

\vspace{2mm}
\begin{center}
\begin{tikzpicture}
    % Image in a node
    \node[anchor=south west, inner sep=0] (image) at (0,0) {\includegraphics[width=16em]{distance_sensor}};
    % Use the image as the bounding box of the tikzpicture for centering
    \useasboundingbox (image.south east) rectangle (image.north west);

    % Create scope with normalized axes
    \begin{scope}[
        x={($0.05*(image.south east)$)},
        y={($0.05*(image.north west)$)}
    ]
        % Draw grid
        %\draw[lightgray,step=1] (image.south west) grid (image.north east);

        % Draw axes labels
        %\foreach \x in {0,1,...,20} {\node [below] at (\x,0) {\tiny \x};}
        %\foreach \y in {0,1,...,20} {\node [left]  at (0,\y) {\tiny \y};}

        % Nodes
        \node[annotation, left]  (output_on)    at (-1.5, 16.4) {Output (on)\\(will send an\\input to it)};
        \node[annotation, right] (output_off)   at (21.5, 16.4) {Output (off)\\(won't send an\\input to it)};
        \node[annotation, left]  (range)        at (-1.5, 3)    {Range};
        \node[annotation, below] (output_value) at (8.5, -1.5)  {Output value};
        \node[annotation, right] (trigger)      at (21.5, 0)    {Invert trigger (on/off),\\currently off\\(normal trigger)};

        % Arrows
        \draw[arrow] (output_on.east)     -- (4.4, 16.4);
        \draw[arrow] (output_off.west)    -- (9.8, 16.4);
        \draw[arrow] (range.east)         -- (0.3, 3);
        \draw[arrow] (output_value.north) -- (8.5, 0.7);
        \draw[arrow] (trigger.west)       -- (14, 4.5);
    \end{scope}
\end{tikzpicture}
\end{center}
\vspace{10mm}

\newcommand{\titleAB}{Altitude Sensor}
\phantomsection
\addcontentsline{toc}{subsection}{\TOCLabelII \titleAB}

- **\TitleFormatII{\titleAB}**
  - Altitude: in meters above the frame of reference, $1 \text{ block} = 0.25 \text{ m}$
  - Output value: from $-1$ to $1$
  - Frame of reference
    - Ignore waves: fixed altitude at the average sea level
    - Relative to waves: altitude of the water below the sensor
    - Outside of high seas, both options are equivalent
  - Trigger
    - Normal: sends an output when it's above the altitude you set
    - Below: sends an output when it's below the altitude you set
  - Outputs

\vspace{2mm}
\begin{center}
\begin{tikzpicture}
    % Image in a node
    \node[anchor=south west, inner sep=0] (image) at (0,0) {\includegraphics[width=21em]{altitude_sensor}};
    % Use the image as the bounding box of the tikzpicture for centering
    \useasboundingbox (image.south east) rectangle (image.north west);

    % Create scope with normalized axes
    \begin{scope}[
        x={($0.05*(image.south east)$)},
        y={($0.05*(image.north west)$)}
    ]
        % Draw grid
        %\draw[lightgray,step=1] (image.south west) grid (image.north east);

        % Draw axes labels
        %\foreach \x in {0,1,...,20} {\node [below] at (\x,0) {\tiny \x};}
        %\foreach \y in {0,1,...,20} {\node [left]  at (0,\y) {\tiny \y};}

        % Nodes
        \node[annotation, left]  (output_on)       at (-1.5, 16.2) {Output (on)\\(will send an\\input to it)};
        \node[annotation, right] (output_off)      at (21.5, 16.2) {Output (off)\\(won't send an\\input to it)};
        \node[annotation, left]  (altitude)        at (-1.5, 2.5)  {Altitude};
        \node[annotation, below] (output_value)    at (4.9, -1.5)  {Output value};
        \node[annotation, below] (reference_frame) at (12.2, -1.5) {Frame of reference};
        \node[annotation, right] (trigger)         at (21.5, -2.5) {Trigger below (on/off),\\currently off\\(normal trigger)};

        % Arrows
        \draw[arrow] (output_on.east)                        -- (7.75, 16.2);
        \draw[arrow] (output_off.west)                       -- (14.75, 16.2);
        \draw[arrow] (altitude.east)                         -- (0.15, 2.5);
        \draw[arrow] ($(output_value.north) + (1, 0)$)       -- (5.9, 0.6);
        \draw[arrow] ($(reference_frame.north) + (-1.6, 0)$) -- (10.6, 1.55);
        \draw[arrow] (trigger.west)                          -- (16.2, 1.7);
    \end{scope}
\end{tikzpicture}
\end{center}
\vspace{12mm}

\newcommand{\titleAC}{Speed Sensor}
\phantomsection
\addcontentsline{toc}{subsection}{\TOCLabelII \titleAC}

- **\TitleFormatII{\titleAC}**
  - Speed: in km/h or mph depending on the speed unit settings
    - **IMPORTANT:** only detects the movement in the direction that the arrow points. The speed is measured from the position of the block
  - Output value: from $-1$ to $1$
  - Trigger
    - Normal: sends an output when it goes faster than the speed you set
    - Below: sends an output when it goes slower that the speed you set
  - Outputs

\vspace{2mm}
\begin{center}
\begin{tikzpicture}
    % Image in a node
    \node[anchor=south west, inner sep=0] (image) at (0,0) {\includegraphics[width=15em]{speed_sensor}};
    % Use the image as the bounding box of the tikzpicture for centering
    \useasboundingbox (image.south east) rectangle (image.north west);

    % Create scope with normalized axes
    \begin{scope}[
        x={($0.05*(image.south east)$)},
        y={($0.05*(image.north west)$)}
    ]
        % Draw grid
        %\draw[lightgray,step=1] (image.south west) grid (image.north east);

        % Draw axes labels
        %\foreach \x in {0,1,...,20} {\node [below] at (\x,0) {\tiny \x};}
        %\foreach \y in {0,1,...,20} {\node [left]  at (0,\y) {\tiny \y};}

        % Nodes
        \node[annotation, left]  (output_on)    at (-1.5, 15.4) {Output (on)\\(will send an\\input to it)};
        \node[annotation, right] (output_off)   at (21.5, 15.3) {Output (off)\\(won't send an\\input to it)};
        \node[annotation, left]  (speed)        at (-1.5, 2.1)  {Speed};
        \node[annotation, below] (output_value) at (7.7, -1.5)  {Output value};
        \node[annotation, right] (trigger)      at (21.5, 0)    {Trigger below (on/off),\\currently off\\(normal trigger)};

        % Arrows
        \draw[arrow] (output_on.east)     -- (5.25, 15.4);
        \draw[arrow] (output_off.west)    -- (11.65, 15.3);
        \draw[arrow] (speed.east)         -- (0.2, 2.1);
        \draw[arrow] (output_value.north) -- (7.7, 0.45);
        \draw[arrow] (trigger.west)       -- (12.7, 3.4);
    \end{scope}
\end{tikzpicture}
\end{center}
\vspace{10mm}

\newcommand{\titleAD}{Angle Sensor}
\phantomsection
\addcontentsline{toc}{subsection}{\TOCLabelII \titleAD}

- **\TitleFormatII{\titleAD}**
  - Direction: in degrees, changes the position of the middle point of the activation threshold
  - Width: in degrees, changes the size of the activation threshold
  - Output value: from $-1$ to $1$
  - Trigger
    - Normal: sends an output when the arrow is inside the activation threshold
    - Outside: sends an output when the arrow is outside the activation threshold
    - Note: the arrow will always try to point up no matter the orientation (in the direction of highest slope of the plane it is in)
  - Outputs

\vspace{2mm}
\begin{center}
\begin{tikzpicture}
    % Image in a node
    \node[anchor=south west, inner sep=0] (image) at (0,0) {\includegraphics[width=15em]{angle_sensor}};
    % Use the image as the bounding box of the tikzpicture for centering
    \useasboundingbox (image.south east) rectangle (image.north west);

    % Create scope with normalized axes
    \begin{scope}[
        x={($0.05*(image.south east)$)},
        y={($0.05*(image.north west)$)}
    ]
        % Draw grid
        %\draw[lightgray,step=1] (image.south west) grid (image.north east);

        % Draw axes labels
        %\foreach \x in {0,1,...,20} {\node [below] at (\x,0) {\tiny \x};}
        %\foreach \y in {0,1,...,20} {\node [left]  at (0,\y) {\tiny \y};}

        % Nodes
        \node[annotation, left]  (output_on)    at (-1.5, 17.2) {Output (on)\\(will send an\\input to it)};
        \node[annotation, right] (output_off)   at (21.5, 17)   {Output (off)\\(won't send an\\input to it)};
        \node[annotation, left]  (direction)    at (-1.5, 2)    {Direction};
        \node[annotation, below] (width)        at (6.4, -1.5)  {Width};
        \node[annotation, below] (output_value) at (13.2, -1.5) {Output value};
        \node[annotation, right] (trigger)      at (21.5, 3.5)  {Trigger outside (on/off),\\currently off\\(normal trigger)};

        % Arrows
        \draw[arrow] (output_on.east)                     -- (7.2, 17.2);
        \draw[arrow] (output_off.west)                    -- (13.45, 17);
        \draw[arrow] (direction.east)                     -- (0.2, 2);
        \draw[arrow] ($(width.north) + (0.2, 0)$)         -- (6.6, 0.7);
        \draw[arrow] ($(output_value.north) + (-2.2, 0)$) -- (11, 0.7);
        \draw[arrow] (trigger.west)                       -- (15.4, 2.25);
    \end{scope}
\end{tikzpicture}
\end{center}
\vspace{10mm}

\newcommand{\titleAE}{Compass}
\phantomsection
\addcontentsline{toc}{subsection}{\TOCLabelII \titleAE}

- **\TitleFormatII{\titleAE}**
  - Direction: in degrees, changes the position of the middle point of the activation threshold
  - Width: in degrees, changes the size of the activation threshold
  - Output value: from $-1$ to $1$
  - Trigger
    - Normal: sends an output when the arrow is inside the activation threshold
    - Outside: sends an output when the arrow is outside the activation threshold
    - Note: the arrow will always try to point north no matter the orientation
  - Outputs

\vspace{2mm}
\begin{center}
\begin{tikzpicture}
    % Image in a node
    \node[anchor=south west, inner sep=0] (image) at (0,0) {\includegraphics[width=21em]{compass}};
    % Use the image as the bounding box of the tikzpicture for centering
    \useasboundingbox (image.south east) rectangle (image.north west);

    % Create scope with normalized axes
    \begin{scope}[
        x={($0.05*(image.south east)$)},
        y={($0.05*(image.north west)$)}
    ]
        % Draw grid
        %\draw[lightgray,step=1] (image.south west) grid (image.north east);

        % Draw axes labels
        %\foreach \x in {0,1,...,20} {\node [below] at (\x,0) {\tiny \x};}
        %\foreach \y in {0,1,...,20} {\node [left]  at (0,\y) {\tiny \y};}

        % Nodes
        \node[annotation, left]  (output_on)    at (-1.5, 17)   {Output (on)\\(will send an\\input to it)};
        \node[annotation, right] (output_off)   at (21.5, 17)   {Output (off)\\(won't send an\\input to it)};
        \node[annotation, left]  (direction)    at (-1.5, 2.7)  {Direction};
        \node[annotation, below] (width)        at (6.4, -1.5)  {Width};
        \node[annotation, below] (output_value) at (11.8, -1.5) {Output value};
        \node[annotation, right] (trigger)      at (21.5, 4)    {Trigger outside (on/off),\\currently off\\(normal trigger)};

        % Arrows
        \draw[arrow] (output_on.east)                     -- (9.55, 17);
        \draw[arrow] (output_off.west)                    -- (15.9, 17);
        \draw[arrow] (direction.east)                     -- (0.15, 2.7);
        \draw[arrow] (width.north)                        -- (6.4, 1.1);
        \draw[arrow] ($(output_value.north) + (-1.2, 0)$) -- (10.6, 1.1);
        \draw[arrow] (trigger.west)                       -- (14.6, 3.3);
    \end{scope}
\end{tikzpicture}
\end{center}
\vspace{10mm}

\newcommand{\titleAF}{Logic Gates}
\phantomsection
\addcontentsline{toc}{subsection}{\TOCLabelII \titleAF}

- **\TitleFormatII{\titleAF}**
  - Keybinds: green ($1$) and red ($-1$), they act as the same input (an and gate with a green and a red keybind will send an output even when just pressing one of the 2 keybinds), but act as a different input for each seat (an and gate with a keybind will require someone in each seat that has control over it pressing the keybind to send an output)
    - Toggle: toggles **inputs**, when an input reaches a gate it will toggle on the color toggled (if there is, it's of the same color as the input and it's off), toggle it off (if there is, it's of the same color as the input and it's on, it will be toggled off after this pulse stops reaching the gate) or toggle the other color off and check again the other 2 rules (if it's not of the same color as the input and the other color it's toggled on)
      - If you want to toggle the output instead of the inputs, make the signal go through another gate with the toggle after the gate in which you want to toggle the output
  - Timers
    - The timers start as soon as the gate receives a **single input**, even if the gate doesn't meet the conditions to send an output
    - The number will be rounded to have only 2 decimal places when shown on the menu, but the number which will be used is the one you wrote rounded to 8 decimal places. Due to a bug only up to 5 characters can be written, so depending on which value you write the number of decimals which can be used will vary
    - Delay: in seconds, only applied when activating but not when deactivating. Note: each logic gate has an extra delay of $1/60 s$ due to the state of all the logic gates being updated only once per physics' frame
    - Duration and pause (previously known as active and inactive time respectively): in seconds, setting the duration to a number different than $0$ and pause to $0$ will make it send a single pulse until turned off and on again. If both of them are not $0$ it will create a cycle which will be repeated until it's deactivated. The shortest length for a pulse is $1$ frame ($1/60 s$), any value lower than this won't send an output
    - The order of the timers is as follows: delay $\rightarrow$ duration $\rightarrow$ pause $\rightarrow$ back to duration (if pause is 0 it ends after the duration ends)
    - In the case of delay and duration timers, even though their values are expressed in seconds, the game handles them as a number of frames. To calculate that number just do $\text{seconds} \cdot 60$. If this number is not an integer, it will be rounded down to the nearest integer. If this number is an integer however, it will randomly either be kept as it is or be subtracted one frame, so it's recommended to add $0.01$ to the original number to make sure it always stays in the correct number of frames. Pause timers aren't subject to this, and the exact time in seconds is used for them
  - Output value: from $-1$ to $1$
  - Outputs

\vspace{2mm}
\begin{center}
\begin{tikzpicture}
    % Image in a node
    \node[anchor=south west, inner sep=0] (image) at (0,0) {\includegraphics[width=26em]{logic_gate}};
    % Use the image as the bounding box of the tikzpicture for centering
    \useasboundingbox (image.south east) rectangle (image.north west);

    % Create scope with normalized axes
    \begin{scope}[
        x={($0.05*(image.south east)$)},
        y={($0.05*(image.north west)$)}
    ]
        % Draw grid
        %\draw[lightgray,step=1] (image.south west) grid (image.north east);

        % Draw axes labels
        %\foreach \x in {0,1,...,20} {\node [below] at (\x,0) {\tiny \x};}
        %\foreach \y in {0,1,...,20} {\node [left]  at (0,\y) {\tiny \y};}

        % Nodes
        \node[annotation, left]  (output_on)     at (-1.5, 16.4) {Output (on)\\(will send an\\input to it)};
        \node[annotation, right] (output_off)    at (21.5, 16.4) {Output (off)\\(won't send an\\input to it)};
        \node[annotation, left]  (green_keybind) at (-1.5, 4.5)  {Green keybind};
        \node[annotation, below] (red_keybind)   at (7.4, -1.5)  {Red keybind};
        \node[annotation, below] (toggle)        at (1, -1.5)    {Green/red toggle};
        \node[annotation, below] (pause)         at (11.7, -1.5) {Pause};
        \node[annotation, below] (duration)      at (15, -1.5)   {Duration};
        \node[annotation, right] (delay)         at (21.5, 10)   {Delay};
        \node[annotation, right] (output_value)  at (21.5, 3.1)  {Output value};

        % Arrows
        \draw[arrow] (output_on.east)                   -- (8.8, 16.4);
        \draw[arrow] (output_off.west)                  -- (13.35, 16.4);
        \draw[arrow] (green_keybind.east)               -- (0.1, 4.5);
        \draw[arrow] ($(red_keybind.north) + (1.2, 0)$) -- (8.6, 3.5);
        \draw[arrow] (toggle.north)                     -- (0.5, 1.7);
        \draw[arrow] (toggle.north)                     -- (4.9, 2.1);
        \draw[arrow] ($(pause.north) + (0.8, 0)$)       -- (12.5, 0.3);
        \draw[arrow] (duration.north)                   -- (13.5, 2.4);
        \draw[arrow] (delay.west)                       -- (13.5, 5.5);
        \draw[arrow] (output_value.west)                -- (16.4, 3.1);
    \end{scope}
\end{tikzpicture}
\end{center}
\vspace{10mm}

\newcommand{\titleB}{Output Value}
\phantomsection
\addcontentsline{toc}{section}{\TOCLabelI \titleB}

## \TitleFormatI{\titleB} {.unlisted .unnumbered}

- When something is activated, it acts as if you pressed the keybind. Positive values act as the green keybind and negative values act as the red keybind. For things that only have green keybind, the absolute value will be used \
- Goes from $-1$ to $1$
  - Due to a bug only up to 5 characters can be written, so depending on if the value is positive or negative you will only be able to use up to 4 or 3 decimals respectively. More decimals can be achieved by using multiple gates: if the number is expressed in scientific notation as $\pm a \cdot 10^b$, $a$ can be any number such that $0 \leq a \leq 10$ with up to 7 decimals while $b$ can be any integer such that $-81 \leq b \leq -1$. If $a$ has more than 7 decimals, it will be rounded to 7 decimals
- It's the percentage of power that whatever it activates will use, applied to the value set in the settings (if applicable)
  - For engines it affects the max speed and acceleration (the torque)
  - For thrusters/gimbals/propellers/underwater propellers/outboard boat engines it affects the power
  - For servos/hinges/large hinges it affects the angle
    - For hinges the speed depends on the max angle and not the angle achieved with the output value, resulting in faster speeds with fractional output value
    - For hinges it only works without hold position
    - Hinges are currently bugged resulting in angles way lower than they should be. There is a table at the end of this guide with the multiplier for each output value [\underline{here}](#OutputValue2Multiplier)
  - For spinning servos/helicopter engines/pistons it affects the speed
  - For tone generators it affects the volume
  - For the rest of the blocks, it doesn't affect anything
\newcommand{\titleBA}{How the output value is calculated}
- **\TitleFormatII{\titleBA}**
  \phantomsection
  \addcontentsline{toc}{subsection}{\TOCLabelII \titleBA}
  1) The gate checks if its conditions are met
     - AND gate: all inputs are on
     - OR gate: at least 1 input is on
     - XOR gate: only 1 input is on
  2) The gate adds up the output values of all of its inputs
     - If the result is $> 1$ it gets replaced with $1$
     - If the result is $< -1$ it gets replaced with $-1$
  3) The gate multiplies the result by its output value
  4) The gate sends the result as its output value. On the steam version, the final output value must also be different from 0 to send an output
  - Diagram made by Zoomah:
    \vspace{1mm}
    \begin{center}
    \hspace{-4.5em}\includegraphics[width=36.9em]{output_value_diagram}
    \end{center}
    \
  - Example

An AND gate with an output value of $0.5$ has 2 inputs, one of them has an output value of $0.8$ and the other of $0.5$. When at least one of them is off, it doesn't send an output. When both of them are on at the same time, the AND gate is able to send an output. On that case, the output values of the inputs are first added up: $0.8 + 0.5 = 1.3$. Because the sum, $1.3$, is bigger than $1$, the gate replaces it with $1$. Then that value is multiplied by the output value of the gate: $1 \cdot 0.5 = 0.5$. Finally, the AND gate sends an output with the value of that multiplication, $0.5$. On the steam version, if the sum of the inputs or the output value of the gate had been $0$, the resultant value of the multiplication would have also been $0$, in which case the gate wouldn't have sent an output

\newcommand{\titleC}{Useful Circuits}
\phantomsection
\addcontentsline{toc}{section}{\TOCLabelI \titleC}

## \TitleFormatI{\titleC} {.unlisted .unnumbered}

\newcommand{\titleCA}{NOR/NOT Gate}
\phantomsection
\addcontentsline{toc}{subsection}{\TOCLabelII \titleCA}

- **\TitleFormatII{\titleCA}**
  - Inverts the state of the input
  - Made by connecting an always on input (a sensor that is always on, all sensors can be configured to work like this but the most commonly used one is a distance sensor with 0 range and invert trigger) to a XOR gate
  - If it only has a single input that isn't the always on input it will act as a NOT gate, if it has multiple it will act as a NOR gate
  - You can make a NAND/XNOR gate by making an AND/XOR gate output to a NOT gate and taking the output from the NOT gate

\newcommand{\titleCB}{Pulse generator/Rising edge detector}
\phantomsection
\addcontentsline{toc}{subsection}{\TOCLabelII \titleCB}

- **\TitleFormatII{\titleCB}**
  - Sends a pulse of a specific length (usually a single frame which is $1/60 s$) when the input goes from off to on
  - Made by setting the duration to the length of the pulse on an OR gate

\newcommand{\titleCC}{Falling edge detector}
\phantomsection
\addcontentsline{toc}{subsection}{\TOCLabelII \titleCC}

- **\TitleFormatII{\titleCC}**
  - Sends a pulse of a specific length when the input goes from on to off
  - Made by connecting a NOT gate to a pulse generator

\newcommand{\titleCD}{Latch}
\phantomsection
\addcontentsline{toc}{subsection}{\TOCLabelII \titleCD}

- **\TitleFormatII{\titleCD}**
  - Stores a single bit of information
  - Made by activating toggle on an OR gate, requires the input to be a pulse to be easily controlled by other gates (use a pulse generator for this)

\newcommand{\titleCE}{Counter}
\phantomsection
\addcontentsline{toc}{subsection}{\TOCLabelII \titleCE}

- **\TitleFormatII{\titleCE}**
  - Can store the value of a variable with $n$ possible values
  - Depending on how it's made, it can be 1 or 2 way and have cycle or not
    - 1-way: the value can only be increased
    - 2-way: the value can be both increased and decreased
    - Cycle: determines if trying to increase/decrease the value past its maximum/minimum will result in it cycling back to the smallest/biggest value or staying at the maximum/minimum value
    - Base designs are 1-way without cycle
  - The complexity of a design is the amount of logic gates used by it without counting the ones used to create a startup pulse or always on sensors (those can be reused)
  - There are 3 ways of doing it: general circuit, base 10 and binary. Which one is least complex depends on the situation
    \newcommand{\titleCEA}{General Circuit}
    - \titleCEA
      \phantomsection
      \addcontentsline{toc}{subsubsection}{\TOCLabelIII \titleCEA}
      - $n = \text{amount of cells}$
      - The output is encoded as the position of the active gate in the row of output gates (with the one from the first cell being the minimum value and the one from the last cell being the maximum value)
      - Diagram of the circuit:
        \vspace{2mm}
        \begin{tikzpicture}[trim left=8.1em]
        % Nodes

        % Cell 1
        \node[node]       (OR_1)                          {Toggled OR gate\\with 1 frame\\delay (output)};
        \node[node]       (AND_1)   [below = 5mm of OR_1] {AND gate};
        \coordinate[above=16pt of OR_1]   (cell_1);

        % Hidden cell 1
        \node[hiddenNode] (OR_h1)   [right = of OR_1]     {};
        \node[hiddenNode] (AND_h1)  [right = of AND_1]    {};

        % Cell k
        \node[node]       (OR_k)    [right = of OR_h1]    {Toggled OR gate\\with 1 frame\\delay (output)};
        \node[node]       (AND_k)   [right = of AND_h1]   {AND gate};
        \coordinate[above=16pt of OR_k]   (cell_k);

        % Cell k+1
        \node[node]       (OR_k+1)  [right = of OR_k]     {Toggled OR gate\\with 1 frame\\delay (output)};
        \node[node]       (AND_k+1) [right = of AND_k]    {AND gate};
        \coordinate[above=16pt of OR_k+1] (cell_k+1);

        % Hidden cell 2
        \node[hiddenNode] (OR_h2)   [right = of OR_k+1]   {};
        \node[hiddenNode] (AND_h2)  [right = of AND_k+1]  {};

        % Cell n
        \node[node]       (OR_n)    [right = of OR_h2]    {Toggled OR gate\\with 1 frame\\delay (output)};
        \node[hiddenNode] (AND_n)   [right = of AND_h2]   {};
        \coordinate[above=16pt of OR_n]   (cell_n);

        % Input gate
        \node[node] (input_pulse) at ($(AND_k)!0.5!(AND_k+1) + (0, -2.25)$) {1 frame pulse\\generator (input)};

        % Cell bounding boxes
        \begin{scope}[on background layer]
            \node[node,       fit=(OR_1)(AND_1)(cell_1),       label={[anchor=north, yshift=-2.5pt]Cell $1$}] {};
            \node[hiddenNode, fit=(OR_h1)(AND_h1)]             {$\cdots$};
            \node[node,       fit=(OR_k)(AND_k)(cell_k),       label={[anchor=north, yshift=-2.5pt]Cell $k$}] {};
            \node[node,       fit=(OR_k+1)(AND_k+1)(cell_k+1), label={[anchor=north, yshift=-2.5pt]Cell $k+1$}] {};
            \node[hiddenNode, fit=(OR_h2)(AND_h2)]             {$\cdots$};
            \node[node,       fit=(OR_n)(AND_n)(cell_n),       label={[anchor=north, yshift=-2.5pt]Cell $n$}] {};
        \end{scope}

        % Arrows

        % Cell 1
        \draw[arrow] (AND_1.east)                   -- ($(AND_1.east)!0.5!(AND_h1.west)$)   |- (OR_h1.west);
        \draw[arrow] ($(OR_1.south) + (-2mm, 0)$)   -- ($(AND_1.north) + (-2mm, 0)$);
        \draw[arrow] ($(AND_1.north) + (2mm, 0)$)   -- ($(OR_1.south) + (2mm, 0)$);

        % Hidden cell 1
        \draw[arrow] (AND_h1.east)                  -- ($(AND_h1.east)!0.5!(AND_k.west)$)   |- (OR_k.west);

        % Cell k
        \draw[arrow] (AND_k.east)                   -- ($(AND_k.east)!0.5!(AND_k+1.west)$)  |- (OR_k+1.west);
        \draw[arrow] ($(OR_k.south) + (-2mm, 0)$)   -- ($(AND_k.north) + (-2mm, 0)$);
        \draw[arrow] ($(AND_k.north) + (2mm, 0)$)   -- ($(OR_k.south) + (2mm, 0)$);

        % Cell k+1
        \draw[arrow] (AND_k+1.east)                 -- ($(AND_k+1.east)!0.5!(AND_h2.west)$) |- (OR_h2.west);
        \draw[arrow] ($(OR_k+1.south) + (-2mm, 0)$) -- ($(AND_k+1.north) + (-2mm, 0)$);
        \draw[arrow] ($(AND_k+1.north) + (2mm, 0)$) -- ($(OR_k+1.south) + (2mm, 0)$);

        % Hidden cell 2
        \draw[arrow] (AND_h2.east)                  -- ($(AND_h2.east)!0.5!(AND_n.west)$)   |- (OR_n.west);

        % Input gate
        \coordinate  (input) at ($(input_pulse.north) + (0, 0.5)$);
        \draw[line]  (input_pulse.north)            -- (input);
        \draw[arrow] (input)                        -| (AND_1.south);
        \draw[arrow] (input)                        -| (AND_h2.south);
        \draw[arrow] (input -| AND_h1)              -- (AND_h1.south);
        \draw[arrow] (input -| AND_k)               -- (AND_k.south);
        \draw[arrow] (input -| AND_k+1)             -- (AND_k+1.south);
        \end{tikzpicture}\vspace{1mm}
      - To add cycle, add an AND gate to the last cell configured in the same way as the others and using the first cell as its next cell
      - To make it 2-way, add a new AND gate to each cell configured in the same way as the other one but going in the opposite direction and using a different pulse generator as input
      - Requires a startup pulse to one of the toggled OR gates to work (achieved with a 1 frame pulse generator)
      - Complexity
        - 1-way: $2n$
        - 1-way+cycle: $2n + 1$
        - 2-way: $3n$
        - 2-way+cycle: $3n + 1$
      - Takes 3 frames to update
      - Example blueprints: [\underline{1-way}](https://steamcommunity.com/sharedfiles/filedetails/?id=2134486907), [\underline{1-way+cycle}](https://steamcommunity.com/sharedfiles/filedetails/?id=2134487841), [\underline{2-way}](https://steamcommunity.com/sharedfiles/filedetails/?id=2075055361) and [\underline{2-way+cycle}](https://steamcommunity.com/sharedfiles/filedetails/?id=2134489564)
    \newcommand{\titleCEB}{Base 10}
    - \titleCEB
      \phantomsection
      \addcontentsline{toc}{subsubsection}{\TOCLabelIII \titleCEB}
      - $n = 10^\text{amount of cells}; \text{ amount of cells} = \ceil{\log_{10} n}$
      - Each cell is the general circuit for $n=10$ with cycle and no input gate, except for the last cell which can have any value $2 \leq n \leq 10$ and doesn't need to have cycle
      - The output is encoded as a decimal number with a digit stored in each cell (with the first cell being the least significant digit and the last cell being the most significant digit)
      - Diagram of the circuit:
        \vspace{2mm}
        \begin{tikzpicture}[trim left=8.1em]
        % Nodes

        % Cell 1
        \node[node]       (ORs_1)                                        {All OR gates\\except the last};
        \node[node]       (OR_final_1)    [below = 1.5mm of ORs_1]       {Last OR gate};
        \node[node]       (ANDs_1)        [below = 1.5mm of OR_final_1]  {All AND gates};
        \coordinate[above=16pt of ORs_1]       (cell_1);

        % Hidden cell 1
        \node[hiddenNode] (ORs_h1)        [right = of ORs_1]             {};
        \node[hiddenNode] (OR_final_h1)   [right = of OR_final_1]        {};
        \node[hiddenNode] (ANDs_h1)       [right = of ANDs_1]            {};

        % Cell k
        \node[node]       (ORs_k)         [right = of ORs_h1]            {All OR gates\\except the last};
        \node[node]       (OR_final_k)    [right = of OR_final_h1]       {Last OR gate};
        \node[node]       (ANDs_k)        [right = of ANDs_h1]           {All AND gates};
        \coordinate[above=16pt of ORs_k]       (cell_k);

        % Cell k+1
        \node[node]       (ORs_k+1)       [right = of ORs_k]             {All OR gates\\except the last};
        \node[node]       (OR_final_k+1)  [right = of OR_final_k]        {Last OR gate};
        \node[node]       (ANDs_k+1)      [right = of ANDs_k]            {All AND gates};
        \coordinate[above=16pt of ORs_k+1]     (cell_k+1);

        % Hidden cell 2
        \node[hiddenNode] (ORs_h2)        [right = of ORs_k+1]           {};
        \node[hiddenNode] (OR_final_h2)   [right = of OR_final_k+1]      {};
        \node[hiddenNode] (ANDs_h2)       [right = of ANDs_k+1]          {};

        % Cell n
        \node[node]       (ORs_n)         [right = of ORs_h2]            {All OR gates\\except the last};
        \node[hiddenNode] (OR_final_n)    [right = of OR_final_h2]       {};
        \node[node]       (ANDs_n)        [right = of ANDs_h2]           {All AND gates};
        \coordinate[above=16pt of ORs_n]       (cell_n);

        % Input gate
        \node[node]       (input_pulse) at ($(ANDs_k) + (0.45, -3.25)$)  {1 frame pulse\\generator (input)};
        \node[node]       (input_OR)      [right = 1.5mm of input_pulse] {OR gate};
        \coordinate[above=16pt of input_pulse] (input_cell);

        % Cell bounding boxes
        \begin{scope}[on background layer]
            \node[node,       fit=(ORs_1)(ANDs_1)(OR_final_1)(cell_1),         label={[anchor=north, yshift=-2.5pt]Cell $1$}] {};
            \node[hiddenNode, fit=(ORs_h1)(ANDs_h1)(OR_final_h1)]              {$\cdots$};
            \node[node,       fit=(ORs_k)(ANDs_k)(OR_final_k)(cell_k),         label={[anchor=north, yshift=-2.5pt]Cell $k$}] {};
            \node[node,       fit=(ORs_k+1)(ANDs_k+1)(OR_final_k+1)(cell_k+1), label={[anchor=north, yshift=-2.5pt]Cell $k+1$}] {};
            \node[hiddenNode, fit=(ORs_h2)(ANDs_h2)(OR_final_h2)]              {$\cdots$};
            \node[node,       fit=(ORs_n)(ANDs_n)(OR_final_n)(cell_n),         label={[anchor=north, yshift=-2.5pt]Cell $\ceil{\log_{10} n}$}] {};
            \node[node,       fit=(input_pulse)(input_OR)(input_cell),         label={[anchor=north, yshift=-2.5pt]Input circuit}] {};
        \end{scope}

        % Arrows

        % Points between cells (top)
        \coordinate (1-h1)    at ($(ORs_1.east)!0.5!(ORs_h1.west)   + (0, 1.75)$);
        \coordinate (h1-k)    at ($(ORs_h1.east)!0.5!(ORs_k.west)   + (0, 1.75)$);
        \coordinate (k-k+1)   at ($(ORs_k.east)!0.5!(ORs_k+1.west)  + (0, 1.75)$);
        \coordinate (k+1-h2)  at ($(ORs_k+1.east)!0.5!(ORs_h2.west) + (0, 1.75)$);
        \coordinate (h2-n)    at ($(ORs_h2.east)!0.5!(ORs_n.west)   + (0, 1.75)$);
        \coordinate (n-)      at ($(ORs_n.east)                     + (0.5, 1.75)$);
        % Points between cells (bottom)
        \coordinate (1-h1-)   at ($(1-h1)                           - (0, 4.6)$);
        \coordinate (h1-k-)   at ($(h1-k)                           - (0, 4.6)$);
        \coordinate (k-k+1-)  at ($(k-k+1)                          - (0, 4.6)$);
        \coordinate (k+1-h2-) at ($(k+1-h2)                         - (0, 4.6)$);
        \coordinate (h2-n-)   at ($(h2-n)                           - (0, 4.6)$);

        % Cell 1
        \draw[line]  (ORs_1.east)         -- (ORs_1 -| 1-h1);
        \draw[arrow] (OR_final_1.east)    -- (OR_final_1 -| 1-h1)      |- (ANDs_h1.west);

        % Hidden cell 1
        \draw[line]  (ORs_h1.east)        -- (ORs_h1 -| h1-k);
        \draw[arrow] (OR_final_h1.east)   -- (OR_final_h1 -| h1-k)     |- (ANDs_k.west);
        \draw[->-]   (ANDs_1 -| 1-h1)     -- (1-h1-) -- (h1-k-)        -- (h1-k |- ANDs_k);
        \draw[->-]   (ORs_1  -| 1-h1)     -- (1-h1)  -- (h1-k)         -- (h1-k |- ORs_k);

        % Cell k
        \draw[line]  (ORs_k.east)         -| (k-k+1);
        \draw[arrow] (OR_final_k.east)    -- (OR_final_k -| k-k+1)     |- (ANDs_k+1.west);
        \draw[->-]   (h1-k-)              -- (k-k+1-);
        \draw[->-]   (h1-k)               -- (k-k+1);
        \draw[line]  (ANDs_k -| k-k+1)    -- (k-k+1-);

        % Cell k+1
        \draw[line]  (ORs_k+1.east)       -| (k+1-h2);
        \draw[arrow] (OR_final_k+1.east)  -- (OR_final_k+1 -| k+1-h2)  |- (ANDs_h2.west);
        \draw[->-]   (k-k+1-)             -- (k+1-h2-);
        \draw[->-]   (k-k+1)              -- (k+1-h2);

        % Hidden cell 2
        \draw[line]  (ORs_h2.east)        -- (ORs_h2 -| h2-n);
        \draw[arrow] (OR_final_h2.east)   -- (OR_final_h2 -| h2-n)     |- (ANDs_n.west);
        \draw[->-]   (ANDs_k+1 -| k+1-h2) -- (k+1-h2-) -- (h2-n-)      -- (h2-n |- ANDs_n);
        \draw[->-]   (k+1-h2)             -- (h2-n);

        % Cell n
        \draw[arrow] (ORs_n.east)         -- (ORs_n -| n-)             |- (input_OR.east);
        \draw[->-]   (ORs_h2 -| h2-n)     -- (h2-n) -- (n-)            -- (n- |- ORs_n);

        % Input gate
        \coordinate  (input) at ($(input_pulse.north) + (0, 1.25)$);
        \draw[arrow] (input_pulse.north)  -- (input)                   -| (ANDs_1.south);
        \draw[line]  (input_OR.north)     |- (input);
        \draw[->-]   (ANDs_1 |- 1-h1-)    -- (1-h1-);
        \end{tikzpicture}\vspace{1mm}
      - To add cycle, add cycle to the last cell and remove the OR gate from the input circuit
      - To make it 2-way, duplicate the input circuit but connect all OR gates except the first from each cell to the OR gate. Then, make each cell 2-way, connect the cells in the same direction using the first OR gate of each cell rather than the last, and connect the new input circuit to all AND gates for the second direction
      - Might require a decoder (unless you want to show numbers on a screen)
        - To create it, take $n$ AND gates and assign a different combination of 1 output gate from each cell to each of them (if you only need to use it combined with other circuits, you can combine all of their decoders into a single one to use less gates)
        - Has a complexity of $n$ gates
      - Requires a startup pulse to one of the toggled OR gates on each cell to work (achieved with a 1 frame pulse generator)
      - Complexity
        - 1-way: $2 \ceil[\Big]{\frac{n}{10^{\ceil{\log_{10} n} - 1}}} + 20 \ceil{\log_{10} n} - 19$
        - 1-way+cycle: $2 \ceil[\Big]{\frac{n}{10^{\ceil{\log_{10} n} - 1}}} + 20 \ceil{\log_{10} n} - 19$
        - 2-way: $3 \ceil[\Big]{ \frac{n}{10^{\ceil{\log_{10} n} - 1}}} + 30 \ceil{\log_{10} n} - 28$
        - 2-way+cycle: $3 \ceil[\Big]{\frac{n}{10^{\ceil{\log_{10} n} - 1}}} + 30 \ceil{\log_{10} n} - 28$
      - Takes 3 frames to update with cycle and 4 frames otherwise
      - Example blueprints: [\underline{1-way}](https://steamcommunity.com/sharedfiles/filedetails/?id=2134491881), [\underline{1-way+cycle}](https://steamcommunity.com/sharedfiles/filedetails/?id=2134492935), [\underline{2-way}](https://steamcommunity.com/sharedfiles/filedetails/?id=2134494676) and [\underline{2-way+cycle}](https://steamcommunity.com/sharedfiles/filedetails/?id=2134496082)
    \newcommand{\titleCEC}{Binary}
    - \titleCEC
      \phantomsection
      \addcontentsline{toc}{subsubsection}{\TOCLabelIII \titleCEC}
      - Works best when $n$ is a power of $2$. If it isn't, more gates are needed to cap the value at $n$
      - $n = 2^\text{amount of cells}; \text{ amount of cells} = \ceil{\log_2 n}$
      - The output is encoded as a binary number with a bit stored in each cell (with the first cell being the least significant digit and the last cell being the most significant digit)
      - Diagram of the circuit:
        \vspace{2mm}
        \begin{tikzpicture}[trim left=8.1em]
        % Nodes

        % Cell 1
        \node[node]       (OR_1)                                         {Toggled OR gate\\(output)};
        \node[node]       (AND_1)         [below = 5mm of OR_1]          {AND gate};
        \coordinate[above=16pt of OR_1]        (cell_1);

        % Hidden cell 1
        \node[hiddenNode] (OR_h1)         [right = of OR_1]              {};
        \node[hiddenNode] (AND_h1)        [right = of AND_1]             {};

        % Cell k
        \node[node]       (OR_k)          [right = of OR_h1]             {Toggled OR gate\\(output)};
        \node[node]       (AND_k)         [right = of AND_h1]            {AND gate};
        \coordinate[above=16pt of OR_k]        (cell_k);

        % Cell k+1
        \node[node]       (OR_k+1)        [right = of OR_k]              {Toggled OR gate\\(output)};
        \node[node]       (AND_k+1)       [right = of AND_k]             {AND gate};
        \coordinate[above=16pt of OR_k+1]      (cell_k+1);

        % Hidden cell 2
        \node[hiddenNode] (OR_h2)         [right = of OR_k+1]            {};
        \node[hiddenNode] (AND_h2)        [right = of AND_k+1]           {};

        % Cell n
        \node[node]       (OR_n)          [right = of OR_h2]             {Toggled OR gate\\(output)};
        \node[node]       (AND_n)         [right = of AND_h2]            {AND gate};
        \coordinate[above=16pt of OR_n]        (cell_n);

        % Input circuit
        \node[node]       (input_pulse) at ($(AND_k) + (0.45, -2.75)$)   {1 frame pulse\\generator (input)};
        \node[node]       (input_NAND)    [right = 1.5mm of input_pulse] {NAND gate};
        \coordinate[above=16pt of input_pulse] (input_cell);

        % Cell bounding boxes
        \begin{scope}[on background layer]
            \node[node,       fit=(OR_1)(AND_1)(cell_1),                 label={[anchor=north, yshift=-2.5pt]Cell $1$}] {};
            \node[hiddenNode, fit=(OR_h1)(AND_h1)]                       {$\cdots$};
            \node[node,       fit=(OR_k)(AND_k)(cell_k),                 label={[anchor=north, yshift=-2.5pt]Cell $k$}] {};
            \node[node,       fit=(OR_k+1)(AND_k+1)(cell_k+1),           label={[anchor=north, yshift=-2.5pt]Cell $k+1$}] {};
            \node[hiddenNode, fit=(OR_h2)(AND_h2)]                       {$\cdots$};
            \node[node,       fit=(OR_n)(AND_n)(cell_n),                 label={[anchor=north, yshift=-2.5pt]Cell $\ceil{\log_2 n}$}] {};
            \node[node,       fit=(input_pulse)(input_NAND)(input_cell), label={[anchor=north, yshift=-2.5pt]Input Circuit}] {};
        \end{scope}

        % Arrows

        % Points between cells
        \coordinate (1-h1)   at ($(OR_1.east)!0.5!(OR_h1.west)   + (0, 1.75)$);
        \coordinate (h1-k)   at ($(OR_h1.east)!0.5!(OR_k.west)   + (0, 1.75)$);
        \coordinate (k-k+1)  at ($(OR_k.east)!0.5!(OR_k+1.west)  + (0, 1.75)$);
        \coordinate (k+1-h2) at ($(OR_k+1.east)!0.5!(OR_h2.west) + (0, 1.75)$);
        \coordinate (h2-n)   at ($(OR_h2.east)!0.5!(OR_n.west)   + (0, 1.75)$);
        \coordinate (n-)     at ($(OR_n.east)                    + (0.5, 1.75)$);

        % Cell 1
        \draw[arrow] (AND_1.north)       -- (OR_1.south);
        \draw[arrow] (OR_1.east)         -- (OR_1 -| 1-h1)     |- (AND_h1.west);

        % Hidden cell 1
        \draw[arrow] (OR_h1.east)        -- (OR_h1 -| h1-k)    |- (AND_k.west);
        \draw[->-]   (OR_1 -| 1-h1)      -- (1-h1) -- (h1-k)   -- (h1-k |- OR_k);

        % Cell k
        \draw[arrow] (AND_k.north)       -- (OR_k.south);
        \draw[arrow] (OR_k.east)         -- (OR_k -| k-k+1)    |- (AND_k+1.west);
        \draw[->-]   (h1-k)              -- (k-k+1);
        \draw[line]  (OR_k -| k-k+1)     -- (k-k+1);

        % Cell k+1
        \draw[arrow] (AND_k+1.north)     -- (OR_k+1.south);
        \draw[arrow] (OR_k+1.east)       -- (OR_k+1 -| k+1-h2) |- (AND_h2.west);
        \draw[->-]   (k-k+1)             -- (k+1-h2);
        \draw[line]  (OR_k+1 -| k+1-h2)  -- (k+1-h2);

        % Hidden cell 2
        \draw[arrow] (OR_h2.east)        -- (OR_h2 -| h2-n)    |- (AND_n.west);
        \draw[->-]   (k+1-h2)            -- (h2-n);

        % Cell n
        \draw[arrow] (AND_n.north)       -- (OR_n.south);
        \draw[arrow] (OR_n.east)         -- (OR_n -| n-)       |- (input_NAND.east);
        \draw[->-]   (OR_h2 -| h2-n)     -- (h2-n) -- (n-)     -- (n- |- OR_n);

        \coordinate  (input) at ($(input_pulse.north) + (0, 1.25)$);
        \draw[line]  (input_pulse.north) -- (input);
        \draw[line]  (input_NAND.north)  -- (input_NAND |- input);
        \draw[arrow] (input)             -| (AND_1.south);
        \draw[arrow] (input)             -| (AND_n.south);
        \draw[arrow] (input -| AND_h1)   -| (AND_h1.south);
        \draw[arrow] (input -| AND_k)    -| (AND_k.south);
        \draw[arrow] (input -| AND_k+1)  -| (AND_k+1.south);
        \draw[arrow] (input -| AND_h2)   -| (AND_h2.south);
        \end{tikzpicture}\vspace{1mm}
      - To add cycle, remove the NAND gate from the input circuit and the AND gate on the first cell, and connect the 1 frame pulse generator directly to the OR gate in the first cell
      - To make it 2-way, add a NOT gate to each cell with its OR gate as input and a new AND gate connected in the same way as the old AND gate, but using the NOT gate of all previous cells as input instead of the OR gates. Then replace the NAND gate on the input circuit with an OR gate and duplicate it (with the copy being connected to the new AND gates on each cell rather than the old ones). Connect the NOT gate of all the cells to the OR gate of the first input circuit, and the OR gate of all the cells to the OR gate of the second input circuit
      - Might require a decoder
        - To create it, add a NOT gate to each cell and replace the NAND gate of the input circuit with an OR gate like in the 2-way version (if using the 1-way versions). Then, take $n$ AND gates and assign each of them a different combination of either the OR or NOT from each cell (if you only need to use it combined with other circuits you can combine all of their decoders into a single one to use less gates)
        - Has a complexity of $\ceil{\log_2 n} + n - 1$ for the 1-way version, $\ceil{\log_2 n} + n$ for the 1-way+cycle version and $n$ for the 2-way versions
      - Complexity
        - 1-way: $2 \ceil{\log_2 n} + 3$
        - 1-way+cycle: $2 \ceil{\log_2 n}$
        - 2-way: $4 \ceil{\log_2 n} + 4$
        - 2-way+cycle: $4 \ceil{\log_2 n}$
      - Takes 3 frames to update for 1-way+cycle and 4 frames otherwise
      - Example blueprints: [\underline{1-way}](https://steamcommunity.com/sharedfiles/filedetails/?id=2134497489), [\underline{1-way+cycle}](https://steamcommunity.com/sharedfiles/filedetails/?id=2134498845), [\underline{2-way}](https://steamcommunity.com/sharedfiles/filedetails/?id=2134500019) and [\underline{2-way+cycle}](https://steamcommunity.com/sharedfiles/filedetails/?id=2134500705)
    \newcommand{\titleCED}{When to use each method}
    - \titleCED
      \phantomsection
      \addcontentsline{toc}{subsubsection}{\TOCLabelIII \titleCED}
      - Calculated for $n \geq 3$, for $n = 2$ a latch is always best

\vspace{2mm}
\hspace{-1.25cm}
\begin{tabular}{|c|m{18.75em}|m{18.75em}|}
    \cline{2-3}
    \multicolumn{1}{c|}{} & \thead{1-way} & \thead{2-way} \\
    \hline
    % In order for the "Without cycle" text to be properly vertically centered, the other columns need to be vertically centered as well. To make them look like they are aligned at the top, they must have the same amount of lines
    \rotatebox[origin=c]{90}{\thead{Without cycle}}
    &
    Doesn't require a decoder:
    \begin{itemize}
        \item For $n \leq 3$ use the general circuit
        \item For $n > 3$ use the binary circuit
    \end{itemize}
    Doesn't require an individual decoder:
    \begin{itemize}
        \item For $n \leq 5$ use the general circuit
        \item For $n > 5$ use the binary circuit
    \end{itemize}
    Requires an individual decoder:
    \begin{itemize}
        \item For $n \leq 14$ or $n = 17$ use the general circuit
        \item For $n > 14$ and $n \neq 17$ use the binary circuit
    \end{itemize}
    Show values directly on a screen (only numbers for $n > 12$):
    \begin{itemize}
        \item For $n \leq 12$ use the general circuit
        \item For $n > 12$ use the base 10 circuit
        \newline
    \end{itemize}
    &
    Doesn't require a decoder:
    \begin{itemize}
        \item For $n \leq 5$ use the general circuit
        \item For $n > 5$ use the binary circuit
    \end{itemize}
    Doesn't require an individual decoder:
    \begin{itemize}
        \item For $n \leq 5$ use the general circuit
        \item For $n > 5$ use the binary circuit
    \end{itemize}
    Requires an individual decoder:
    \begin{itemize}
        \item For $n \leq 10$ use the general circuit
        \item For $n > 10$ use the binary circuit
        \newline
        \newline
    \end{itemize}
    Show values directly on a screen (only numbers for $n > 16$):
    \begin{itemize}
        \item For $n \leq 10$ use the general circuit
        \item For $10 < n \leq 16$ use the binary circuit
        \item For $n > 16$ use the base 10 circuit
    \end{itemize} \\
    \hline
    \rotatebox[origin=c]{90}{\thead{With cycle}}
    &
    Doesn't require a decoder:
    \begin{itemize}
        \item Use the binary circuit
    \end{itemize}
    Doesn't require an individual decoder:
    \begin{itemize}
        \item Use the binary circuit
    \end{itemize}
    Requires an individual decoder:
    \begin{itemize}
        \item For $n \leq 11$ use the general circuit
        \item For $n > 11$ use the binary circuit
    \end{itemize}
    Show values directly on a screen (only numbers for $n > 12$):
    \begin{itemize}
        \item For $n < 12$ use the general circuit
        \item For $n = 12$ use the binary circuit
        \item For $n > 12$ use the base 10 circuit
        \newline
    \end{itemize}
    &
    Doesn't require a decoder:
    \begin{itemize}
        \item Use the binary circuit
    \end{itemize}
    Doesn't require an individual decoder:
    \begin{itemize}
        \item Use the binary circuit
    \end{itemize}
    Requires an individual decoder:
    \begin{itemize}
        \item For $n \leq 3$ or $n = 5$ use the general circuit
        \item For $n = 4$ or $n > 5$ use the binary circuit
    \end{itemize}
    Show values directly on a screen (only numbers for $n > 17$):
    \begin{itemize}
        \item For $n \leq 3$ or $n = 5$ use the general circuit
        \item For $n = 4$ or $5 < n \leq 17$ use the binary circuit
        \item For $n > 17$ use the base 10 circuit
    \end{itemize} \\
    \hline
\end{tabular}
\

Note: this is just based on the amount of logic gates each circuit uses (unless there is a tie, in which case update speed is used). However, the amount of time it takes for the system to update might also matter depending on the situation. In that case, the fastest is the general and base 10 with cycle circuits, followed by the 1-way binary circuit with cycle, then by the base 10 circuit without cycle and lastly the binary circuit without cycle or with 2-way

\clearpage

\newcommand{\titleD}{Output value to multiplier for hinges}
\phantomsection
\addcontentsline{toc}{section}{\TOCLabelI \titleD}

## \TitleFormatI{\titleD} {#OutputValue2Multiplier .unlisted .unnumbered}

- Final angle is the resulting angle of the hinge measured with a max angle of $90$ degrees and an error of $\pm 0.005$ degrees

- The multiplier was calculated by doing $\text{multiplier} = \frac{\text{final angle}}{90}$

\setlength\LTleft{-0.95cm}
\begin{longtable}{|c|c|c !{\vrule width 3pt} c|c|c !{\vrule width 3pt} c|c|c|}
    \hline
    \thead{Output\\value} & \thead{Final\\angle} & \thead{Multiplier} & \thead{Output\\value} & \thead{Final\\angle} & \thead{Multiplier} & \thead{Output\\value} & \thead{Final\\angle} & \thead{Multiplier} \\
    \HLine{2pt}
    1.000 & 90.000 & 1.00000000 & 0.810 & 31.275 & 0.34750000 & 0.480 & 05.640 & 0.06266667 \\
    \hline
    0.995 & 88.345 & 0.98161111 & 0.805 & 30.215 & 0.33572222 & 0.470 & 05.295 & 0.05883333 \\
    \hline
    0.990 & 86.680 & 0.96311111 & 0.800 & 29.195 & 0.32438889 & 0.460 & 04.960 & 0.05511111 \\
    \hline
    0.985 & 85.000 & 0.94444444 & 0.795 & 28.225 & 0.31361111 & 0.450 & 04.640 & 0.05155556 \\
    \hline
    0.980 & 83.315 & 0.92572222 & 0.790 & 27.300 & 0.30333333 & 0.440 & 04.335 & 0.04816667 \\
    \hline
    0.975 & 81.620 & 0.90688889 & 0.785 & 26.425 & 0.29361111 & 0.430 & 04.040 & 0.04488889 \\
    \hline
    0.970 & 79.920 & 0.88800000 & 0.780 & 25.595 & 0.28438889 & 0.420 & 03.760 & 0.04177778 \\
    \hline
    0.965 & 78.215 & 0.86905556 & 0.775 & 24.825 & 0.27583333 & 0.410 & 03.495 & 0.03883333 \\
    \hline
    0.960 & 76.505 & 0.85005556 & 0.770 & 24.105 & 0.26783333 & 0.400 & 03.245 & 0.03605556 \\
    \hline
    0.955 & 74.795 & 0.83105556 & 0.765 & 23.440 & 0.26044444 & 0.390 & 03.005 & 0.03338889 \\
    \hline
    0.950 & 73.085 & 0.81205556 & 0.760 & 22.830 & 0.25366667 & 0.380 & 02.775 & 0.03083333 \\
    \hline
    0.945 & 71.380 & 0.79311111 & 0.755 & 22.280 & 0.24755556 & 0.370 & 02.560 & 0.02844444 \\
    \hline
    0.940 & 69.675 & 0.77416667 & 0.750 & 21.790 & 0.24211111 & 0.360 & 02.355 & 0.02616667 \\
    \hline
    0.935 & 67.975 & 0.75527778 & 0.740 & 20.920 & 0.23244444 & 0.350 & 02.160 & 0.02400000 \\
    \hline
    0.930 & 66.280 & 0.73644444 & 0.730 & 20.075 & 0.22305556 & 0.340 & 01.980 & 0.02200000 \\
    \hline
    0.925 & 64.595 & 0.71772222 & 0.720 & 19.255 & 0.21394444 & 0.330 & 01.805 & 0.02005556 \\
    \hline
    0.920 & 62.920 & 0.69911111 & 0.710 & 18.460 & 0.20511111 & 0.320 & 01.645 & 0.01827778 \\
    \hline
    0.915 & 61.250 & 0.68055556 & 0.700 & 17.685 & 0.19650000 & 0.310 & 01.495 & 0.01661111 \\
    \hline
    0.910 & 59.595 & 0.66216667 & 0.690 & 16.930 & 0.18811111 & 0.300 & 01.350 & 0.01500000 \\
    \hline
    0.905 & 57.955 & 0.64394444 & 0.680 & 16.200 & 0.18000000 & 0.290 & 01.220 & 0.01355556 \\
    \hline
    0.900 & 56.325 & 0.62583333 & 0.670 & 15.490 & 0.17211111 & 0.280 & 01.095 & 0.01216667 \\
    \hline
    0.895 & 54.715 & 0.60794444 & 0.660 & 14.800 & 0.16444444 & 0.270 & 00.980 & 0.01088889 \\
    \hline
    0.890 & 53.125 & 0.59027778 & 0.650 & 14.135 & 0.15705556 & 0.269 & 00.970 & 0.01077778 \\
    \hline
    0.885 & 51.550 & 0.57277778 & 0.640 & 13.485 & 0.14983333 & 0.268 & 00.955 & 0.01061111 \\
    \hline
    0.880 & 49.995 & 0.55550000 & 0.630 & 12.860 & 0.14288889 & 0.267 & 00.945 & 0.01050000 \\
    \hline
    0.875 & 48.465 & 0.53850000 & 0.620 & 12.250 & 0.13611111 & 0.266 & 00.935 & 0.01038889 \\
    \hline
    0.870 & 46.960 & 0.52177778 & 0.610 & 11.660 & 0.12955556 & 0.265 & 00.925 & 0.01027778 \\
    \hline
    0.865 & 45.480 & 0.50533333 & 0.600 & 11.095 & 0.12327778 & 0.264 & 00.915 & 0.01016667 \\
    \hline
    0.860 & 44.025 & 0.48916667 & 0.590 & 10.545 & 0.11716667 & 0.263 & 00.905 & 0.01005556 \\
    \hline
    0.855 & 42.600 & 0.47333333 & 0.580 & 10.010 & 0.11122222 & 0.262 & 00.000 & 0.00000000 \\
    \hline
    0.850 & 41.200 & 0.45777778 & 0.570 & 09.500 & 0.10555556 & 0.261 & 00.000 & 0.00000000 \\
    \hline
    0.845 & 39.830 & 0.44255556 & 0.560 & 09.000 & 0.10000000 & 0.260 & 00.000 & 0.00000000 \\
    \hline
    0.840 & 38.505 & 0.42783333 & 0.550 & 08.525 & 0.09472222 & 0.250 & 00.000 & 0.00000000 \\
    \hline
    0.835 & 37.200 & 0.41333333 & 0.540 & 08.065 & 0.08961111 & 0.200 & 00.000 & 0.00000000 \\
    \hline
    0.830 & 35.940 & 0.39933333 & 0.530 & 07.620 & 0.08466667 & 0.150 & 00.000 & 0.00000000 \\
    \hline
    0.825 & 34.715 & 0.38572222 & 0.520 & 07.190 & 0.07988889 & 0.100 & 00.000 & 0.00000000 \\
    \hline
    0.820 & 33.530 & 0.37255556 & 0.510 & 06.780 & 0.07533333 & 0.050 & 00.000 & 0.00000000 \\
    \hline
    0.815 & 32.380 & 0.35977778 & 0.500 & 06.380 & 0.07088889 & 0.000 & 00.000 & 0.00000000 \\
    \hline
    \multicolumn{3}{c!{\vrule width 3pt}}{} & 0.490 & 06.005 & 0.06672222 & \multicolumn{3}{c}{} \\
    \cmidrule(l{-3pt}){4-6}
\end{longtable}

\vspace{-2mm}
\hspace{-3.5em}
\begin{tikzpicture}
    \begin{axis}[
        height=27.5em,
        width=42em,
        title={Multiplier as a function of the output value},
        xlabel={Output value},
        ylabel={Multiplier},
        domain = 0:1,
        xmin=0, xmax=1,
        ymin=0, ymax=1,
        minor tick num=1,
        grid=both
    ]
        \addplot[color=blue, mark=*] file {Output_Value_to_Multiplier.dat} node[above left, midway] {$f(x)$};
        \addplot[color=black, samples=3] {x} node[above left, midway] {$y=x$};
    \end{axis}
\end{tikzpicture}

\newcommand{\titleE}{Tips}
\phantomsection
\addcontentsline{toc}{section}{\TOCLabelI \titleE}

## \TitleFormatI{\titleE} {.unlisted .unnumbered}

- If you want your system to not modify the input that passes through, configure all of the logic gates to have an output value of 1. Then, if a gate needs to have more inputs other than the original one, make sure the sum of the output values of those other inputs is 0. This will make the output which reaches whatever your system activates be the output that the sensors/keybinds had
- Organize the logic gates on a testbed while working with them before adding them to your vehicle, having the logic gates organized as opposed to scattered across your entire vehicle will make remembering what each gate does easier. There is no wrong way to organize them as long as they aren't randomly placed, but the way I do it is by splitting the gates into groups depending on function, inside each group the arrows of logic gates point towards the outputs of that gate and away from its inputs, then I put the groups of logic gates that a group outputs to in the direction the arrows of the logic gates that the group uses as output are pointing, while I put the groups that group uses as input in the opposite direction
- If you have problems figuring out how to do something with logic gates, draw it on paper first, being able to see all connections at once helps a lot. Another method is writing it with if statements as they translate to logic gates easily (each logic gate is an individual if statement)
- If you still have any questions or need help with something, feel free to contact me on the [\underline{official trailmakers discord server}](https://discord.gg/trailmakers)

## \large Made by ALVAROPING1#6682 {.unlisted .unnumbered}
