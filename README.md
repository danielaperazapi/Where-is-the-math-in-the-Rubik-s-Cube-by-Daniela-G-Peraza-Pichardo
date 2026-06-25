# Where is the math in the Rubik's Cube? by Daniela G. Peraza Pichardo
This repository explores the mathematical principles behind the best-selling toy in history: the Rubik's Cube. While the Rubik's Cube is often seen only as a mechanical puzzle from the 80's, it is deeply connected to several areas of mathematics, in particular, group theory and permutations.

![](header.png)

-----------------------------------------------------------------------------------------

The objective of this project is to understand the Rubik's Cube through mathematical concepts, to describe its possible configurations, and to analyze the algorithms used to solve it through this mathematical perspective. As mentioned earlier, the Rubik’s Cube may appear as a mere entertaining puzzle, but each move performed in any of its faces rearranges its pieces according to precise rules. Therefore, by representing the changes in the pieces' configuration as permutations, it is possible to create a model that helps understand the cube’s behavior, which could even predict the resulting rearrangement of entire sequences of face rotations.

The motivation for this project comes from my personal interest in _speedcubing_, a hobby that consists of solving the Rubik’s Cube and its variants in the shortest possible time, which relies on pattern recognition and memorized algorithms. Hence, it is precisely the need of _algorithms_ in the last two steps of cube-solving which provokes the question of what the math behind these _algorithms_ looks like and most importantly why they work. In other words, the aim is, through the study of permutations and commutators, to show how group theory provides a framework for predicting and controlling the movement of cube pieces.

![](1_d5ghk6ZEXbIQVGSfUR9l3w.png)

To better appreciate the mathematics behind the Rubik's Cube, it is useful to first understand how the puzzle is typically solved. Modern speedsolving methods, such as **CFOP (Cross, First Two Layers, Orientation of the Last Layer, and Permutation of the Last Layer)**, divide the solution process into several stages.

![](cross.png)

The first step is the **cross**, where four edge pieces are positioned and oriented correctly relative to one another. This stage is usually solved intuitively, meaning that the solver analyzes the cube and determines the necessary moves without relying on memorized algorithms.

![](f2l.png)

The second stage is known as **First Two Layers (F2L)**. Here, corner-edge pairs are inserted into their correct slots to simultaneously solve the first and second layers of the cube. While advanced solvers often learn specialized algorithms to perform F2L efficiently, the process can largely be understood through logical reasoning and visualization. A solver identifies a corner and its matching edge, pairs them together, and inserts them into the correct position. Because only a small number of pieces are involved at a time, many beginners are able to discover solutions on their own without extensive memorization.

However, as the cube becomes more solved, the problem becomes more and more complex. Once the first two layers are completed, it is only the last layer which remains unsolved. This is where the transition from intuitive solving to algorithmic solving occurs.

![](OLL.png)

The first last-layer step is called **Orientation of the Last Layer (OLL)**. The goal is to rotate all last-layer pieces so that the entire top face becomes a single color, usually yellow. It is important to mention that OLL does not necessarily place the pieces in their correct positions; it only ensures that they are **facing** the correct direction. Depending on the arrangement of the last-layer pieces, there are 57 possible OLL cases, each with its own algorithm. Experienced solvers learn to recognize these patterns and apply the corresponding sequence of moves in a matter of just a couple of seconds.

![](PLL.png)

Once all last-layer pieces are correctly oriented, the solver proceeds to **Permutation of the Last Layer (PLL)**. During this step, the pieces are already facing the correct direction, but many of them remain in the wrong locations. The objective of PLL is to **move the pieces into their correct positions without changing their orientation**. There are 21 possible PLL cases, each solved by a different algorithm. After applying the appropriate PLL algorithm, the cube becomes **completely solved**.

What makes OLL and PLL particularly interesting for this project is that the algorithms used are carefully designed permutations of cube pieces. Rather than moving every cubie randomly, these algorithms affect only specific regions of the cube while preserving most of the cube that has already been solved. ThHence, the algorithms can be analyzed as permutations of individual cube pieces.

Below is the link to a motivaional video that inspired and guided the development of this project. The video explores the mathematical ideas behind Rubik's Cube algorithms and explains how solving methods are connected to concepts such as permutations, commutators, and group theory.

https://youtu.be/_Zv3YcQeNVI

Rather than presenting algorithms as sequences of moves to be memorized, the video investigates why certain algorithms work and how they manipulate specific cube pieces while leaving others unchanged. It introduces the concept of commutators, which is a fundamental tool which will be used in the analysis of algorithms, and discusses the challenges of understanding increasingly complex algorithms due to the enormous number of possible cube configurations.

This resource is particularly helpful because it bridges the gap between practical cube solving and the mathematical structures that govern it. It provides an accessible introduction to the ideas that are developed more rigorously in the technical section of this repository, helping readers understand how abstract mathematical concepts can be applied to analyze and solve a real-world puzzle.

-----------------------------------------------------------------------------------------

## PRESENTING THE PROPOSAL
The following video presents the initial proposal for this project, _The Math Behind the 3×3 Rubik's Cube_. In this video, the main objectives of the project are introduced, as well as the mathematical concepts required to analyze the puzzle, and the motivation for studying the Rubik's Cube from a mathematical perspective. It also introduces fundamental concepts such as cycle notation, composition of permutations, and the commutator, which serves as one of the key mathematical tools used throughout this project.

This video provides the foundation for the more detailed analysis presented in the **Hands-on** section of the repository. It is intended to help viewers understand the problem being investigated, the mathematical framework that will be used, and the questions that guide the development of the project, including how algorithms affect cube pieces and why certain cube configurations are impossible to obtain through legal moves.

https://youtu.be/mN8gmh6tW7c

-----------------------------------------------------------------------------------------

## TECHNICALITIES OF THE PROJECT

### MOTIVATION

A standard 3×3 Rubik's Cube has approximately 4.3 × 10¹⁹ possible configurations, meaning that there are more than 43 quintillion ways to arrange its pieces. Despite this enormous complexity, every **legal move** follows precise mathematical rules.

![](rubiks-cube-line.jpg)

Each face rotation rearranges the cube's pieces and since these rearrangements correspond to permutations of the cube pieces, the Rubik's Cube can be studied using permutations and group theory. In this repository, the focus is set particularly on the last-layer solving stages known as **OLL (Orientation of the Last Layer)** and **PLL (Permutation of the Last Layer)** which we had already mentioned.

### RUBIK'S CUBE NOTATION

Before constructing a mathematical model, it is necessary to establish a notation for describing cube movements. Supposing the cube is facing an arbitrary direction, with one face facing toward us, the six faces of the cube are denoted by the letters:

**U (Up)**

**D (Down)**

**F (Front)**

**B (Back)**

**R (Right)**

**L (Left)**

![](RUBIKSNOTATION.png)

A letter by itself represents a **90-degree clockwise rotation** of that face. For example: [R]

A prime symbol indicates a **90-degree counterclockwise rotation**: [R']

A number 2 indicates a **180-degree rotation**: [R2]

![](R-on-Rubiks-cube.jpg)

These symbols allow move sequences, commonly called algorithms, to be written in a more standardized way.

### IDENTIFYING CUBE PIECES

To refer to an individual cubie, or cube piece, we use as many letters as stickers on them are. The letters used are the ones that correspond to the side of the cubie we are referring to. The cube consists of three types of cubies:

#### Centers

Center pieces have one visible sticker and are identified by a single letter.

Examples:

U, D, F, B, R, L

![](CENTERPIECES.png)

#### Edges

Edge pieces have two stickers and are identified by two letters.

Examples:

UF, UB, UL, UR, ...

![](EDGEPIECES.png)

#### Corners

Corner pieces have three stickers and are identified by three letters.

Examples:

UFR, UFL, UBR, UBL, ...

![](CORNERPIECES.png)

### PERMUTATIONS

A permutation is a rearrangement of objects. As an example:

(1 2 3)

1→2,  2→3,  3→1

Every move of the Rubik's Cube can be viewed as a permutation because it rearranges the positions of cubies.

For example, a U move rotates the top layer and cycles the four upper corners:

(UFR UBR UBL UFL)

This means:

**UFR moves to UBR**

**UBR moves to UBL**

**UBL moves to UFL**

**UFL moves to UFR**

Similarly, the upper edges are permuted according to:

(UF UR UB UL)

Therefore, the complete permutation produced by U is

U = (UFR UBR UBL UFL)(UF UR UB UL)

Cycle notation therefore provides a precise description of how cube pieces move. 

### GROUPS

### THE COMMUTATOR

### APPLICATION TO OLL AND PLL

### WHY GROUP THEORY IS NECESSARY

### ALTERNATIVE APPROACHES


-----------------------------------------------------------------------------------------

## CONCLUSIONS

-----------------------------------------------------------------------------------------

## REFERENCES
