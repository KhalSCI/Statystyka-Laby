# Przedziały ufności w R - podsumowanie metod

## Spis treści
- [Wprowadzenie](#wprowadzenie)
- [Przedziały ufności dla średniej](#przedziały-ufności-dla-średniej)
- [Przedziały ufności dla proporcji](#przedziały-ufności-dla-proporcji)
- [Przedziały ufności dla wariancji](#przedziały-ufności-dla-wariancji)
- [Przedziały ufności dla różnicy średnich](#przedziały-ufności-dla-różnicy-średnich)
- [Przedziały ufności dla różnicy proporcji](#przedziały-ufności-dla-różnicy-proporcji)
- [Tabela podsumowująca](#tabela-podsumowująca)
- [Przykłady użycia](#przykłady-użycia)

## Wprowadzenie

Przedział ufności to zakres wartości, który z określonym prawdopodobieństwem (poziomem ufności) zawiera prawdziwą wartość parametru populacji. Wybór odpowiedniej metody do obliczenia przedziału ufności zależy od:

- Rodzaju parametru (średnia, proporcja, wariancja, itp.)
- Rozkładu zmiennej (normalny, inny)
- Wielkości próby (mała, duża)
- Znajomości parametrów populacji (np. czy znana jest wariancja populacji)

## Przedziały ufności dla średniej

### 1. Znane odchylenie standardowe populacji (σ)

**Funkcja**: `z.test()` z pakietu BSDA

**Kiedy używać**:
- Zmienna ma rozkład normalny lub próba jest dostatecznie duża (n ≥ 30)
- Znamy odchylenie standardowe populacji (σ)

**Składnia**:
```r
library(BSDA)
z.test(x, sigma.x = znane_sigma, conf.level = 0.95)
```

### 2. Nieznane odchylenie standardowe populacji, mała próba

**Funkcja**: `t.test()` (wbudowana w R)

**Kiedy używać**:
- Zmienna ma rozkład normalny
- Nie znamy odchylenia standardowego populacji
- Mała próba (n < 30)

**Składnia**:
```r
t.test(x, conf.level = 0.95)
```

### 3. Nieznane odchylenie standardowe populacji, duża próba

**Funkcja**: `t.test()` (wbudowana w R) lub `zsum.test()` z pakietu BSDA

**Kiedy używać**:
- Nie znamy odchylenia standardowego populacji
- Duża próba (n ≥ 30)
- Z funkcji `zsum.test()` korzystamy, gdy znamy tylko statystyki z próby, a nie surowe dane

**Składnia**:
```r
# Gdy mamy surowe dane:
t.test(x, conf.level = 0.95)

# Gdy znamy tylko statystyki z próby:
library(BSDA)
zsum.test(mean.x = średnia_próby, sigma.x = odchylenie_std_próby, 
          n.x = liczebność_próby, conf.level = 0.95)
```

## Przedziały ufności dla proporcji

### 1. Metoda dokładna (rozkład dwumianowy)

**Funkcja**: `binom.test()` (wbudowana w R)

**Kiedy używać**:
- Mała próba
- Proporcja bliska 0 lub 1
- Potrzebna jest wysoka dokładność

**Składnia**:
```r
binom.test(x = liczba_sukcesów, n = liczebność_próby, conf.level = 0.95)
```

### 2. Metoda przybliżona (rozkład normalny)

**Funkcja**: `prop.test()` (wbudowana w R)

**Kiedy używać**:
- Duża próba (spełnione warunki: n·p ≥ 5 i n·(1-p) ≥ 5)
- Proporcja nie jest bliska 0 ani 1

**Składnia**:
```r
prop.test(x = liczba_sukcesów, n = liczebność_próby, conf.level = 0.95)
```

## Przedziały ufności dla wariancji

**Funkcja**: `sigma.test()` z pakietu TeachingDemos

**Kiedy używać**:
- Zmienna ma rozkład normalny

**Składnia**:
```r
library(TeachingDemos)
sigma.test(x, conf.level = 0.95)
```

## Przedziały ufności dla różnicy średnich

### 1. Znane odchylenia standardowe populacji

**Funkcja**: `zsum.test()` z pakietu BSDA

**Kiedy używać**:
- Znamy odchylenia standardowe obu populacji
- Obie zmienne mają rozkład normalny lub próby są duże

**Składnia**:
```r
library(BSDA)
zsum.test(mean.x = średnia_próby1, sigma.x = odchylenie_std_próby1, n.x = liczebność_próby1,
          mean.y = średnia_próby2, sigma.y = odchylenie_std_próby2, n.y = liczebność_próby2,
          conf.level = 0.95)
```

### 2. Nieznane, ale równe wariancje populacji

**Funkcja**: `t.test()` z parametrem `var.equal = TRUE`

**Kiedy używać**:
- Nie znamy odchyleń standardowych populacji
- Zakładamy, że wariancje są równe
- Obie zmienne mają rozkład normalny

**Składnia**:
```r
t.test(x, y, var.equal = TRUE, conf.level = 0.95)
```

### 3. Nieznane i nierówne wariancje populacji

**Funkcja**: `t.test()` z parametrem `var.equal = FALSE` (domyślnie)

**Kiedy używać**:
- Nie znamy odchyleń standardowych populacji
- Nie zakładamy równości wariancji
- Obie zmienne mają rozkład normalny

**Składnia**:
```r
t.test(x, y, conf.level = 0.95)  # var.equal = FALSE jest domyślne
```

## Przedziały ufności dla różnicy proporcji

**Funkcja**: `prop.test()`

**Kiedy używać**:
- Duże próby (spełnione warunki: n₁·p₁ ≥ 5, n₁·(1-p₁) ≥ 5, n₂·p₂ ≥ 5, n₂·(1-p₂) ≥ 5)

**Składnia**:
```r
prop.test(x = c(liczba_sukcesów1, liczba_sukcesów2), 
          n = c(liczebność_próby1, liczebność_próby2), 
          conf.level = 0.95)
```

## Tabela podsumowująca

| Parametr | Warunki | Funkcja | Pakiet |
|----------|---------|---------|--------|
| Średnia | Znane σ, rozkład normalny | `z.test()` | BSDA |
| Średnia | Nieznane σ, rozkład normalny, mała próba | `t.test()` | Wbudowana |
| Średnia | Nieznane σ, duża próba | `t.test()` lub `zsum.test()` | Wbudowana / BSDA |
| Proporcja | Mała próba lub p blisko 0/1 | `binom.test()` | Wbudowana |
| Proporcja | Duża próba | `prop.test()` | Wbudowana |
| Wariancja | Rozkład normalny | `sigma.test()` | TeachingDemos |
| Różnica średnich | Znane σ | `zsum.test()` | BSDA |
| Różnica średnich | Nieznane, równe wariancje | `t.test(var.equal = TRUE)` | Wbudowana |
| Różnica średnich | Nieznane, nierówne wariancje | `t.test()` | Wbudowana |
| Różnica proporcji | Duże próby | `prop.test()` | Wbudowana |

## Przykłady użycia

### Przykład 1: Przedział ufności dla średniej (znane σ)

```r
library(BSDA)
dane <- c(25.2, 26.4, 25.8, 24.9, 25.5, 26.1, 25.7)
# Załóżmy, że znane σ = 0.5
z.test(dane, sigma.x = 0.5, conf.level = 0.95)
```

### Przykład 2: Przedział ufności dla średniej (nieznane σ)

```r
dane <- c(25.2, 26.4, 25.8, 24.9, 25.5, 26.1, 25.7)
t.test(dane, conf.level = 0.95)
```

### Przykład 3: Przedział ufności dla proporcji

```r
# 42 sukcesy w próbie 100 obserwacji
prop.test(x = 42, n = 100, conf.level = 0.95)
```

### Przykład 4: Przedział ufności dla różnicy średnich

```r
grupa1 <- c(25.2, 26.4, 25.8, 24.9, 25.5, 26.1, 25.7)
grupa2 <- c(24.8, 25.2, 24.5, 25.1, 24.9, 25.3, 24.7)
t.test(grupa1, grupa2, conf.level = 0.95)
```

### Przykład 5: Przedział ufności przy znanych statystykach z próby

```r
library(BSDA)
# Gdy mamy tylko statystyki z dużej próby
zsum.test(mean.x = 25.7, sigma.x = 0.5, n.x = 100, conf.level = 0.95)
```