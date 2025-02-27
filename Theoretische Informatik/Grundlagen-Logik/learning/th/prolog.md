# TODO

-   Du kannst mit der Aufgabe 8 & 10 in den Übungsklausuren rumprobieren
-   Definiere eine Funktion "zipper", die ähnlich we "conc", zwei Listen zu einer macht. Die beiden Listen sollen aber Reisverschluss-mäßig zusammen genommen werden.
    -   [1, 2, 3], [4, 5, 6, 7, 8] => [1, 4, 2, 5, 3, 6, 7, 8]
    -   [1, 2, 3, 4], [-1, -2] => [1, -1, 2, -2, 3, 4]
-   Definiere eine Funktion "oddpossum", die alle ungeraden Zahlen einer Liste zusammen addiert
    -   [1, 2, 3, 4] => 1+3 = 4
    -   [0, 3, 12, -53, 2] => 3 + (-53) = -50

# Tipps

-   `%` notiert einen Kommentar in Prolog.
-   Alle Funktionen müssen in Prolog mit einem `.` beendet werden.
-   Eine Funktion sieht normalerweise so aus: `name(_, _, ...).` bzw. `name(_, _, ...) :- ..., ... .`

## Dateien ausführen

-   Speicher deine Prolog Dateien im selben Ordner wie deine Prolog App
-   Öffne die App -> Prolog müsste sich öffnen mit einem `?-`
-   Schreibe `[Name der Datei].` und drücke enter
-   Wenn keine Fehler in der Datei sind, müsste `true.` ausgegeben werden. (Gelbe Warnungen können meistens ignoriert werden)
-   Jetzt kannst du alle Funktionen in der Datei ausführen und testen (z.B.: `rev([1, 2, 3], X).` müsste dann `X = [3, 2, 1]` als Ergebnis geben).

# CS 16

## 8

### a)

p1(\[\[X|Y]|\[X,Y]],\[\[Z]|X]) = p1(\[A|\[B|B]],C)

[ [X|Y] | [X, Y] ] = [ [X|Y], X, Y]

Bsp.: [ [1|[2]], 1, [2] ] = [ [1, 2], 1, [2] ]

[1|[2]] = [1, 2]

[A | [B | B]] = [A, B, Z]

Z <- [B]

Bsp.: [1 | [ [2] | [2] ]] = [1, [2], 2]

#### Die eigentliche Aufgbe

A <- \[X|Y]

Notiz: \[B|B] = \[X,Y] = \[B|\[Y]] => \[B, Y]

B <-> X <- \[Y]

C <- \[\[Z]|X]

==> Ist unifizierbar

### b)

p2(\[\[X|R]|Y],\[Y|X]) = p2(\[Y1|A],\[Y1])

\[Y1|A] = \[\[X|R]|Y] = \[\[\[]|R]|Y]

[ [ [] | R ] | Y ]

\[Y1] = \[Y|X]

X <- \[]

Y1 <-> Y <-> A <-> \[X|R] <-> \[\[]|R]

### c)

p3(\[X|\[\[Y]|\[]]],\[\[Y]|X]) = p3(\[A|R],\[R|A])

R <- [ [Y] | [] ] <- [ [Y] ]

\[1, 2] = \[1, 2|\[]] = \[1|\[2|\[]]]

X = 1, Rest = \[2]
\[A|R] = \[X|\[\[Y]|\[]]] = \[A, \[Y]]

\[R|A] = \[\[Y]|X]

A <-> X

R <- \[\[Y]] <- \[Y] !!! occur check

==> nein

### d)

p4(\[X,\[Y]|\[\[X]]],\[X]) = p4(\[A|\[B,\[A]]],A)

\[X,\[Y]|\[\[X]]] = \[X, \[Y], \[X]]

\[A|\[B,\[A]]] = \[A, B, \[A]]

A <-> X

B <- \[Y]

\[X] -> A

A <-> X <- \[X] occur check!!!

==> nein

### e)

p5(X,[Y|[Y|X]]) = p5([A],[B|[A|B]])

X <- [A]

Y <-> B

Y <-> A

[A] -> X <-> B <-> Y <-> A occur check!!!

==> nein

# CS 17

## Aufgabe 8

### a)

p1([[X,Y]|[X|Y]],[Y|Y]) = p1([A|B],A)

[X, Y] -> A <- [Y|Y]

X <-> Y

[Y] -> Y occur check!!!

==> nein

### b)

p2([[X|R1]|Y],R1) = p2([A|R2],[A])

R1 <- [A]

A <- [X|R1]

R2 <-> Y

R1 <- [A] = [ [X|R1] ] occur check!!!

==> nein

### c)

p3([X|[[]|Y]],[Y]) = p3([A|[]],[B|A])

X <-> A

[] = [ [] | Y ] = [ [] ] occur check!!!

==> nein

### d)

p4([[X],[Y,Y]],Y) = p4([A|[B,C]],B)

[X] -> A

[Y, Y] -> B

C nicht gebunden => occur check!!!

==> nein

### e)

p5(X,[Y,X,X|[Y]]) = p5([A],[B,[A]|B])

[Y,X,X|[Y]] = [Y,X,X,Y]

X <- [A]

Y <-> B

[X|[Y]] = [X, Y] -> B <-> Y occur check!!!

==> nein

# Generell

## Wann welche Pfeile?

\[X] -> Y

\[X] = \[Y]

X <-> Y

## Beispiel für Widerspruch

p1(\[X], X) = p1(A, A)

A <- \[X]

A <-> X

\[X] -> X !!! Occur Check

## Generelles Vorgehen:

\[X] => \[X|\[]]

\[X, Y] => \[X|\[Y]]

\[1, 2, 3]

\[X|Rest] => \[1 |\[2, 3]] => \[1, 2, 3]

Rest = \[2, 3]
