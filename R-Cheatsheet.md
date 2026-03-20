# R Cheatsheet - Umfassender Guide

Ein detaillierter Leitfaden für R Programmierung mit Grundlagen, Statistik, Verteilungen und Visualisierung.

---

## 1. GRUNDLAGEN & SYNTAX

### 1.1 Variablen und Datentypen

#### Variablen zuweisen
```r
# Mit <- oder =
x <- 5
y = 10
name <- "Max"

# Variablennamen ansehen
ls()

# Variablen löschen
rm(x)
rm(list = ls())  # Alle Variablen löschen
```

#### Datentypen
```r
# Numerisch (Double)
a <- 3.14
class(a)  # "numeric"

# Integer
b <- 5L
class(b)  # "integer"

# Logisch/Boolean
c <- TRUE
d <- FALSE
class(c)  # "logical"

# Character/String
text <- "Hallo Welt"
class(text)  # "character"

# Überprüfe Datentyp
is.numeric(a)    # TRUE
is.character(text)  # TRUE
is.logical(c)    # TRUE
```

#### Typkonvertierung
```r
# In numerisch konvertieren
as.numeric("42")    # 42
as.numeric(TRUE)    # 1

# In Character konvertieren
as.character(123)   # "123"
as.character(TRUE)  # "TRUE"

# In Integer konvertieren
as.integer(3.14)    # 3

# In Logical konvertieren
as.logical(1)       # TRUE
as.logical(0)       # FALSE
```

---

### 1.2 Vektoren

#### Vektoren erstellen
```r
# Mit c() kombinieren
v1 <- c(1, 2, 3, 4, 5)
v2 <- c("a", "b", "c")
v3 <- c(TRUE, FALSE, TRUE)

# Mit Sequenzen
seq1 <- 1:10              # 1 2 3 4 5 6 7 8 9 10
seq2 <- seq(1, 10, by=2) # 1 3 5 7 9
seq3 <- seq(0, 1, length.out=5)  # 0.00 0.25 0.50 0.75 1.00

# Mit Wiederholungen
rep1 <- rep(1, 5)        # 1 1 1 1 1
rep2 <- rep(c(1,2), 3)   # 1 2 1 2 1 2
rep3 <- rep(1:3, each=2) # 1 1 2 2 3 3
```

#### Vektoren indexieren
```r
v <- c(10, 20, 30, 40, 50)

# Einzelnes Element
v[1]      # 10 (erste Element)
v[3]      # 30 (drittes Element)

# Mehrere Elemente
v[c(1,3,5)]  # 10 30 50
v[1:3]       # 10 20 30

# Negative Indizierung (ausschließen)
v[-1]        # 20 30 40 50 (alle außer erstem)
v[-c(1,3)]   # 20 40 50

# Logische Indizierung
v[v > 25]    # 30 40 50
v[v %% 2 == 0]  # 10 20 30 40 50 (gerade Zahlen)
```

#### Vektoroperationen
```r
v1 <- c(1, 2, 3)
v2 <- c(10, 20, 30)

# Arithmetische Operationen
v1 + v2     # 11 22 33
v1 * v2     # 10 40 90
v1 / v2     # 0.1 0.1 0.1
v1 ^ 2      # 1 4 9

# Vergleichsoperationen
v1 > 2      # FALSE FALSE TRUE
v1 == 2     # FALSE TRUE FALSE

# Vektorlänge
length(v1)  # 3

# Summe, Mittelwert, Min, Max
sum(v1)     # 6
mean(v1)    # 2
min(v1)     # 1
max(v1)     # 3
```

---

### 1.3 Listen und Data Frames

#### Listen
```r
# Liste erstellen
meine_liste <- list(
  name = "Max",
  alter = 25,
  hobbys = c("Lesen", "Sport"),
  details = list(stadt = "Berlin", land = "Deutschland")
)

# Auf Elemente zugreifen
meine_liste$name           # "Max"
meine_liste[["alter"]]     # 25
meine_liste[[3]]           # c("Lesen", "Sport")
meine_liste$details$stadt  # "Berlin"
```

#### Data Frames
```r
# Data Frame erstellen
df <- data.frame(
  name = c("Alice", "Bob", "Charlie"),
  alter = c(25, 30, 35),
  stadt = c("Berlin", "München", "Hamburg")
)

# Data Frame ansehen
head(df)        # Erste 6 Zeilen
tail(df)        # Letzte 6 Zeilen
str(df)         # Struktur
dim(df)         # Dimensionen: 3 3

# Auf Spalten zugreifen
df$name         # c("Alice", "Bob", "Charlie")
df[, "alter"]   # c(25, 30, 35)
df[1, ]         # Erste Zeile

# Auf einzelnes Element zugreifen
df[2, 3]        # "München"
df$name[1]      # "Alice"

# Neue Spalte hinzufügen
df$beruf <- c("Ingenieur", "Arzt", "Lehrer")

# Zeilen filtern
df[df$alter > 26, ]  # Alle mit alter > 26
```

---

### 1.4 Operatoren

#### Arithmetische Operatoren
```r
5 + 3      # 8
5 - 3      # 2
5 * 3      # 15
5 / 3      # 1.667
5 ^ 3      # 125 (Potenz)
5 %% 3     # 2 (Modulo/Rest)
5 %/% 3    # 1 (Ganzzahldivision)
```

#### Vergleichsoperatoren
```r
5 > 3      # TRUE
5 < 3      # FALSE
5 == 5     # TRUE
5 != 3     # TRUE
5 >= 5     # TRUE
5 <= 3     # FALSE
```

#### Logische Operatoren
```r
TRUE & FALSE   # FALSE (AND)
TRUE | FALSE   # TRUE (OR)
!TRUE          # FALSE (NOT)

# Beispiel mit Vektoren
x <- c(1, 2, 3, 4, 5)
x > 2 & x < 5  # FALSE FALSE TRUE TRUE FALSE
x < 2 | x > 4  # TRUE FALSE FALSE FALSE TRUE
```

---

### 1.5 Kontrollstrukturen

#### if-else Statement
```r
x <- 15

if (x > 10) {
  print("x ist größer als 10")
} else if (x == 10) {
  print("x ist gleich 10")
} else {
  print("x ist kleiner als 10")
}

# Output: "x ist größer als 10"
```

#### for Schleife
```r
# Einfache for Schleife
for (i in 1:5) {
  print(i)
}

# Mit Vektor
farben <- c("rot", "grün", "blau")
for (farbe in farben) {
  print(farbe)
}

# Mit Nested Loop
for (i in 1:3) {
  for (j in 1:2) {
    print(paste(i, j))
  }
}
```

#### while Schleife
```r
x <- 1
while (x <= 5) {
  print(x)
  x <- x + 1
}
```

#### repeat Schleife
```r
x <- 1
repeat {
  print(x)
  x <- x + 1
  if (x > 5) break  # Schleife unterbrechen
}
```

#### apply Familie
```r
# apply() - auf Matrix anwenden
m <- matrix(1:9, nrow=3)
apply(m, 1, sum)    # Summe pro Zeile
apply(m, 2, mean)   # Mittelwert pro Spalte

# lapply() - auf Liste anwenden (gibt Liste zurück)
liste <- list(a=1:3, b=4:6)
lapply(liste, sum)  # list(a=6, b=15)

# sapply() - wie lapply aber vereinfacht
sapply(liste, sum)  # c(a=6, b=15)

# mapply() - mehrere Argumente
mapply(function(x, y) x + y, c(1,2,3), c(10,20,30))
# 11 22 33
```

---

### 1.6 Funktionen schreiben

#### Funktionsdefinition
```r
# Einfache Funktion
quadrat <- function(x) {
  return(x ^ 2)
}
quadrat(5)  # 25

# Funktion mit mehreren Parametern
addiere <- function(a, b, c = 0) {
  return(a + b + c)
}
addiere(2, 3)      # 5
addiere(2, 3, 4)   # 9

# Funktion ohne return (letzter Ausdruck wird zurückgegeben)
quadrat2 <- function(x) {
  x ^ 2
}
quadrat2(5)  # 25

# Funktion mit Vektor
summe_quadrate <- function(v) {
  v ^ 2 |> sum()
}
summe_quadrate(c(1,2,3))  # 14

# Funktion mit ... (variable Argumente)
summe_alles <- function(...) {
  args <- list(...)
  sum(unlist(args))
}
summe_alles(1, 2, 3, 4, 5)  # 15
```

---

## 2. STATISTIK & VERTEILUNGEN

### 2.1 Deskriptive Statistik

#### Grundlegende Funktionen
```r
daten <- c(2, 5, 8, 3, 9, 1, 7, 4, 6)

# Mittelwert
mean(daten)         # 5.111111

# Median
median(daten)       # 5

# Standardabweichung
sd(daten)           # 2.934721

# Varianz
var(daten)          # 8.611111

# Minimum und Maximum
min(daten)          # 1
max(daten)          # 9
range(daten)        # 1 9

# Spannweite
max(daten) - min(daten)  # 8

# Quantile/Perzentile
quantile(daten)     # 0%, 25%, 50%, 75%, 100%
quantile(daten, 0.25)   # 25. Perzentil
quantile(daten, c(0.25, 0.75))  # 25. und 75. Perzentil
```

#### Summary Funktion
```r
df <- data.frame(
  alter = c(22, 25, 28, 30, 35),
  gewicht = c(65, 70, 72, 75, 80),
  groesse = c(165, 170, 172, 175, 180)
)

# Gesamtzusammenfassung
summary(df)

# Output:
#     alter          gewicht         groesse
# Min.   :22.00   Min.   :65.00   Min.   :165.0
# 1st Qu.:25.00   1st Qu.:70.00   1st Qu.:170.0
# Median :28.00   Median :72.00   Median :172.0
# Mean   :28.00   Mean   :72.40   Mean   :172.4
# 3rd Qu.:30.00   3rd Qu.:75.00   3rd Qu.:175.0
# Max.   :35.00   Max.   :80.00   Max.   :180.0

# Nur eine Spalte
summary(df$alter)
```

#### Häufigkeitsverteilungen
```r
# Häufigkeitstabelle
daten <- c("rot", "blau", "rot", "grün", "blau", "rot")
table(daten)
# blau grün  rot
#    2    1    3

# Mit prop.table (Anteile)
prop.table(table(daten))
# blau  grün   rot
# 0.333 0.167 0.500

# Mit zwei Variablen
geschlecht <- c("m", "w", "m", "w", "m", "w")
table(geschlecht, daten)
```

---

### 2.2 Normalverteilung (Gaussian Distribution)

#### Normalverteilungsfunktionen
```r
# dnorm() - Wahrscheinlichkeitsdichtefunktion (PDF)
# Wie wahrscheinlich ist ein bestimmter Wert?
dnorm(0)        # 0.3989 (Standard-Normalverteilung bei x=0)
dnorm(1, mean=0, sd=1)  # 0.2420

# pnorm() - Kumulative Verteilungsfunktion (CDF)
# Wie groß ist die Wahrscheinlichkeit, dass X ≤ x?
pnorm(0)        # 0.5 (50% unter dem Mittelwert)
pnorm(1)        # 0.8413 (84.13% unter 1)
pnorm(1) - pnorm(-1)  # 0.6826 (68.26% zwischen -1 und 1)

# qnorm() - Quantilfunktion (Inverse CDF)
# Welcher Wert hat eine bestimmte Wahrscheinlichkeit?
qnorm(0.5)      # 0 (Median bei 50%)
qnorm(0.975)    # 1.96 (95% Konfidenzintervall)

# rnorm() - Zufallszahlen generieren
rnorm(10)       # 10 zufällige Normalverteilungswerte
rnorm(5, mean=100, sd=15)  # Mit Mittelwert 100 und SD 15
```

#### Beispiel: Normalverteilung
```r
# Erzeuge 1000 normalverteilte Daten
daten <- rnorm(1000, mean=100, sd=15)

# Zusammenfassung
summary(daten)
mean(daten)     # ≈ 100
sd(daten)       # ≈ 15

# Wahrscheinlichkeitsberechnung
# Wie groß ist P(X ≤ 110)?
pnorm(110, mean=100, sd=15)  # 0.7475

# Wie groß ist P(X > 85)?
1 - pnorm(85, mean=100, sd=15)  # 0.8413

# 95% Konfidenzintervall
qnorm(c(0.025, 0.975), mean=100, sd=15)
# 70.6 129.4
```

---

### 2.3 Binomialverteilung

#### Binomialverteilungsfunktionen
```r
# dbinom() - Wahrscheinlichkeitsmassefunktion (PMF)
# Wie wahrscheinlich sind genau k Erfolge?
dbinom(5, size=10, prob=0.5)  # P(X=5) wenn n=10, p=0.5

# pbinom() - Kumulative Verteilungsfunktion
# Wie groß ist die Wahrscheinlichkeit für X ≤ k?
pbinom(5, size=10, prob=0.5)  # P(X ≤ 5)

# qbinom() - Quantilfunktion
qbinom(0.5, size=10, prob=0.5)  # Median

# rbinom() - Zufallszahlen generieren
rbinom(5, size=10, prob=0.5)  # 5 zufällige Binomial-Werte
```

#### Beispiel: Münzwurf
```r
# 10 Münzwürfe, 100 Mal wiederholen
# Wie oft bekommen wir genau 5 Kopf?
ergebnisse <- rbinom(100, size=10, prob=0.5)
table(ergebnisse)

# Wahrscheinlichkeit für genau 5 Kopf
dbinom(5, size=10, prob=0.5)  # 0.2461

# Wahrscheinlichkeit für 5 oder weniger Kopf
pbinom(5, size=10, prob=0.5)  # 0.6230
```

---

### 2.4 Poissonverteilung

#### Poissonverteilungsfunktionen
```r
# dpois() - Wahrscheinlichkeitsmassefunktion
# Wie wahrscheinlich sind genau k Ereignisse?
dpois(3, lambda=2)  # P(X=3) wenn λ=2

# ppois() - Kumulative Verteilungsfunktion
ppois(3, lambda=2)  # P(X ≤ 3)

# qpois() - Quantilfunktion
qpois(0.5, lambda=2)  # Median

# rpois() - Zufallszahlen
rpois(10, lambda=2)  # 10 zufällige Poisson-Werte
```

#### Beispiel: Telefonanrufe
```r
# Im Durchschnitt 3 Anrufe pro Stunde
# Wie wahrscheinlich sind genau 5 Anrufe?
dpois(5, lambda=3)  # 0.1008

# Wie wahrscheinlich sind 5 oder weniger?
ppois(5, lambda=3)  # 0.9161

# Simuliere 100 Stunden
anrufe <- rpois(100, lambda=3)
mean(anrufe)  # ≈ 3
table(anrufe)
```

---

### 2.5 Weitere Verteilungen

#### Exponentialverteilung (Wartezeiten)
```r
# dexp() - PDF
dexp(1, rate=1)     # 0.3679

# pexp() - CDF
pexp(1, rate=1)     # 0.6321

# rexp() - Zufallszahlen
rexp(100, rate=1)   # 100 exponentialverteilte Werte
```

#### Gleichverteilung (Uniform Distribution)
```r
# dunif() - PDF
dunif(0.5, min=0, max=1)  # 1

# punif() - CDF
punif(0.5, min=0, max=1)  # 0.5

# runif() - Zufallszahlen
runif(100, min=0, max=1)  # 100 Zufallszahlen zwischen 0 und 1
```

#### t-Verteilung (für kleine Stichproben)
```r
# dt() - PDF
dt(0, df=10)

# pt() - CDF
pt(1.96, df=10)

# qt() - Quantil
qt(0.975, df=10)    # Kritischer Wert für 95% KI

# rt() - Zufallszahlen
rt(100, df=10)
```

---

### 2.6 Hypothesentests

#### t-Test (Mittelwertsvergleich)
```r
# Eine Stichprobe: Ist der Mittelwert = 100?
daten <- rnorm(30, mean=102, sd=10)
t.test(daten, mu=100)

# Output enthält t-Statistik, p-Wert, Konfidenzintervall

# Zwei unabhängige Stichproben
gruppe1 <- rnorm(20, mean=100, sd=10)
gruppe2 <- rnorm(20, mean=105, sd=10)
t.test(gruppe1, gruppe2)

# Gepaarte Stichproben (vor/nach)
vorher <- c(80, 85, 90, 95, 100)
nachher <- c(85, 88, 92, 98, 105)
t.test(vorher, nachher, paired=TRUE)
```

#### Chi-Quadrat Test (Unabhängigkeit)
```r
# Kontingenztabelle
tabelle <- matrix(c(10, 20, 30, 40), nrow=2)
chisq.test(tabelle)

# Beispiel: Geschlecht und Vorliebe
tabelle <- table(
  geschlecht = c("m", "m", "m", "w", "w", "w", "m", "w"),
  vorliebe = c("A", "A", "B", "B", "A", "B", "A", "A")
)
chisq.test(tabelle)
```

#### ANOVA (Vergleich mehrerer Gruppen)
```r
# Drei Gruppen
gruppe1 <- rnorm(20, mean=100)
gruppe2 <- rnorm(20, mean=105)
gruppe3 <- rnorm(20, mean=102)

daten <- data.frame(
  wert = c(gruppe1, gruppe2, gruppe3),
  gruppe = factor(rep(c("A", "B", "C"), each=20))
)

anova_result <- aov(wert ~ gruppe, data=daten)
summary(anova_result)
```

---

## 3. VISUALISIERUNG & PLOTS

### 3.1 Base R Plots

#### Streudiagramm (Scatter Plot)
```r
# Einfaches Streudiagramm
x <- c(1, 2, 3, 4, 5)
y <- c(2, 4, 5, 4, 6)
plot(x, y)

# Mit Anpassungen
plot(x, y,
     main="Mein Streudiagramm",     # Titel
     xlab="X-Achse",                 # X-Label
     ylab="Y-Achse",                 # Y-Label
     col="blue",                     # Farbe
     pch=19,                         # Punkttyp (19=ausgefüllter Kreis)
     cex=2,                          # Punktgröße
     xlim=c(0, 6),                   # X-Achsen-Bereich
     ylim=c(0, 7))                   # Y-Achsen-Bereich

# Linie hinzufügen
abline(a=1, b=1, col="red", lty=2)  # y = 1 + 1*x
```

#### Histogramm
```r
daten <- rnorm(1000, mean=100, sd=15)

# Einfaches Histogramm
hist(daten)

# Mit Anpassungen
hist(daten,
     main="Verteilung der Daten",
     xlab="Werte",
     ylab="Häufigkeit",
     col="lightblue",
     breaks=30,              # Anzahl der Balken
     border="navy")

# Mit Dichte-Kurve
hist(daten, freq=FALSE, breaks=30)
lines(density(daten), col="red", lwd=2)
```

#### Boxplot
```r
# Einfacher Boxplot
daten <- rnorm(100, mean=100, sd=15)
boxplot(daten)

# Mehrere Boxplots
gruppe1 <- rnorm(50, mean=100)
gruppe2 <- rnorm(50, mean=105)
gruppe3 <- rnorm(50, mean=102)
boxplot(gruppe1, gruppe2, gruppe3,
        names=c("Gruppe A", "Gruppe B", "Gruppe C"),
        main="Vergleich der Gruppen",
        ylab="Werte",
        col=c("lightblue", "lightgreen", "lightcoral"))

# Boxplot mit Formel (aus Data Frame)
df <- data.frame(
  wert = c(gruppe1, gruppe2, gruppe3),
  gruppe = factor(rep(c("A", "B", "C"), each=50))
)
boxplot(wert ~ gruppe, data=df)
```

#### Balkendiagramm (Bar Plot)
```r
# Häufigkeitsdiagramm
daten <- c("A", "B", "A", "C", "B", "A")
barplot(table(daten),
        main="Häufigkeiten",
        ylab="Anzahl",
        col="steelblue")

# Mit eigenen Werten
werte <- c(10, 15, 7, 12)
names(werte) <- c("Q1", "Q2", "Q3", "Q4")
barplot(werte,
        main="Vierteljahres-Verkäufe",
        ylab="Verkäufe (Tausend)",
        col="orange",
        border="darkred")
```

#### Liniengrafik
```r
# Zeitreihe
monate <- 1:12
verkaufe <- c(10, 12, 11, 15, 18, 20, 19, 22, 25, 23, 20, 18)

plot(monate, verkaufe,
     type="l",           # "l" für Linien
     main="Monatliche Verkäufe",
     xlab="Monat",
     ylab="Verkäufe",
     lwd=2,              # Linienstärke
     col="darkblue")

# Mit Punkten
plot(monate, verkaufe,
     type="b",           # "b" für Punkte und Linien
     col="red",
     pch=21,
     bg="yellow",
     lwd=2)
```

#### QQ-Plot (Normalverteilungsprüfung)
```r
daten <- rnorm(100, mean=100, sd=15)
qqnorm(daten)       # Q-Q Plot zeichnen
qqline(daten)       # Referenzlinie hinzufügen

# Wenn Punkte auf der Linie liegen → Normalverteilung!
```

---

### 3.2 Mehrere Plots nebeneinander

#### par(mfrow) - Mehrere Plots in einer Figure
```r
# 2 Zeilen, 2 Spalten
par(mfrow=c(2, 2))

# Plot 1
plot(1:10, main="Plot 1")

# Plot 2
hist(rnorm(100), main="Plot 2")

# Plot 3
boxplot(rnorm(100), main="Plot 3")

# Plot 4
barplot(c(10, 15, 20), main="Plot 4")

# Zurück zu 1 Plot
par(mfrow=c(1, 1))
```

#### par(mfcol) - Nach Spalten füllen
```r
par(mfcol=c(2, 2))  # Nach Spalten, nicht Zeilen
# ... Plots ...
```

#### layout() - Komplexere Anordnungen
```r
# Layout mit unterschiedlichen Größen
layout(matrix(c(1,1,2,3), 2, 2, byrow=TRUE))

plot(1:10, main="Großer Plot")
hist(rnorm(100), main="Histogramm")
boxplot(rnorm(100), main="Boxplot")
```

---

### 3.3 ggplot2 - Moderne Grafiken

#### ggplot2 installieren und laden
```r
# Installieren (einmalig)
install.packages("ggplot2")

# Laden
library(ggplot2)
```

#### Grundstruktur
```r
# ggplot() + geom_...()
ggplot(data, aes(x=var1, y=var2)) + 
  geom_point() +
  labs(title="Titel", x="X-Achse", y="Y-Achse") +
  theme_minimal()
```

#### Streudiagramm mit ggplot2
```r
library(ggplot2)

# Beispieldaten
df <- data.frame(
  x = rnorm(100),
  y = rnorm(100),
  gruppe = sample(c("A", "B"), 100, replace=TRUE)
)

# Einfacher Scatterplot
ggplot(df, aes(x=x, y=y)) +
  geom_point()

# Mit Farben nach Gruppe
ggplot(df, aes(x=x, y=y, color=gruppe)) +
  geom_point(size=3) +
  labs(title="Scatterplot mit Gruppen",
       x="Variable X",
       y="Variable Y",
       color="Gruppe") +
  theme_minimal()

# Mit Regressionslinie
ggplot(df, aes(x=x, y=y)) +
  geom_point() +
  geom_smooth(method="lm", se=TRUE, color="red")
```

#### Histogramm mit ggplot2
```r
daten <- rnorm(1000, mean=100, sd=15)
df <- data.frame(werte = daten)

ggplot(df, aes(x=werte)) +
  geom_histogram(binwidth=5, fill="lightblue", color="black") +
  labs(title="Verteilung der Werte",
       x="Werte",
       y="Häufigkeit") +
  theme_minimal()

# Mit Dichte-Kurve
ggplot(df, aes(x=werte)) +
  geom_histogram(aes(y=after_stat(density)), binwidth=5, fill="lightblue") +
  geom_density(color="red", linewidth=1) +
  theme_minimal()
```

#### Boxplot mit ggplot2
```r
df <- data.frame(
  wert = c(rnorm(50, 100), rnorm(50, 105), rnorm(50, 102)),
  gruppe = factor(rep(c("A", "B", "C"), each=50))
)

ggplot(df, aes(x=gruppe, y=wert, fill=gruppe)) +
  geom_boxplot() +
  geom_jitter(width=0.1, alpha=0.3) +  # Punkte hinzufügen
  labs(title="Boxplot mit Datenpunkten",
       x="Gruppe",
       y="Wert") +
  theme_minimal() +
  theme(legend.position="none")
```

#### Balkendiagramm mit ggplot2
```r
df <- data.frame(
  quartal = c("Q1", "Q2", "Q3", "Q4"),
  verkaufe = c(10, 15, 12, 18)
)

ggplot(df, aes(x=quartal, y=verkaufe, fill=quartal)) +
  geom_bar(stat="identity") +
  labs(title="Vierteljahres-Verkäufe",
       x="Quartal",
       y="Verkäufe") +
  theme_minimal() +
  theme(legend.position="none")
```

#### Liniengrafik mit ggplot2
```r
df <- data.frame(
  monat = 1:12,
  verkaufe = c(10, 12, 11, 15, 18, 20, 19, 22, 25, 23, 20, 18)
)

ggplot(df, aes(x=monat, y=verkaufe)) +
  geom_line(color="darkblue", linewidth=1) +
  geom_point(color="red", size=3) +
  labs(title="Monatliche Verkäufe",
       x="Monat",
       y="Verkäufe") +
  theme_minimal()
```

#### Facetting - Mehrere Subplots
```r
df <- data.frame(
  x = rnorm(300),
  y = rnorm(300),
  gruppe = rep(c("A", "B", "C"), each=100)
)

ggplot(df, aes(x=x, y=y)) +
  geom_point() +
  facet_wrap(~gruppe, nrow=2) +  # 2 Zeilen
  theme_minimal()

# Oder mit facet_grid
ggplot(df, aes(x=x, y=y)) +
  geom_point() +
  facet_grid(~gruppe) +  # Spaltenweise
  theme_minimal()
```

#### Themes und Anpassungen
```r
ggplot(df, aes(x=x, y=y)) +
  geom_point() +
  theme_minimal() +           # Minimalistisch
  # theme_classic() +         # Klassisch
  # theme_dark() +            # Dunkel
  # theme_void() +            # Leer
  theme(
    plot.title = element_text(size=16, face="bold", hjust=0.5),
    axis.title = element_text(size=12, face="bold"),
    panel.grid = element_blank(),
    legend.position = "right"
  )
```

---

## 4. DATENMANIPULATION (Kurzer Überblick)

### 4.1 Basis-Funktionen
```r
# subset() - Zeilen filtern
df <- data.frame(name=c("Alice", "Bob", "Charlie"), alter=c(25, 30, 35))
subset(df, alter > 26)

# merge() - Tabellen verbinden
df1 <- data.frame(id=c(1,2,3), name=c("A", "B", "C"))
df2 <- data.frame(id=c(1,2,3), alter=c(25, 30, 35))
merge(df1, df2, by="id")

# aggregate() - Gruppieren und zusammenfassen
aggregate(df$alter ~ df$name, FUN=mean)
```

### 4.2 dplyr Paket (moderner Ansatz)
```r
library(dplyr)

# Filter, Select, Arrange, Mutate
df %>%
  filter(alter > 26) %>%
  select(name, alter) %>%
  arrange(desc(alter)) %>%
  mutate(alter_kategorie = ifelse(alter > 30, "alt", "jung"))
```

---

## Zusammenfassung

Diese Cheatsheet deckt ab:
- ✅ Grundlagen: Variablen, Datentypen, Vektoren, Funktionen
- ✅ Statistik: Deskriptive Statistik, Verteilungen, Tests
- ✅ Visualisierung: Base R, ggplot2, mehrere Plots
- ✅ Datenmanipulation: Grundlagen

**Mehr lernen:**
- `help(function_name)` - Hilfe in R
- `?function_name` - Schnelle Hilfe
- https://www.r-project.org/ - Offizielle Website
- https://ggplot2.tidyverse.org/ - ggplot2 Dokumentation

---

Erstellt: 2026-03-20
Autor: GitHub Copilot
