### 1. Rozkład normalny (Gaussa)

**Rozpoznawanie w zadaniu:**
- Mowa o "normalności" rozkładu, cechy antropometryczne (wzrost, waga)
- Wyniki testów, pomiarów ciągłych, błędy pomiarowe
- Zmienne o dużej liczbie niezależnych czynników (Centralne Twierdzenie Graniczne)
- Słowa kluczowe: średnia, odchylenie standardowe, zmienne ciągłe, krzywa dzwonowa

**Charakterystyki:**
- Parametry: μ (średnia), σ² (wariancja)
- Wartość oczekiwana: E(X) = μ
- Wariancja: Var(X) = σ²
- Symetryczny, dzwonowy kształt
- Funkcja gęstości: f(x) = (1/(σ√(2π))) * e^(-(x-μ)²/(2σ²))

**W R:**
- Gęstość: `dnorm(x, mean=μ, sd=σ)`
- Dystrybuanta: `pnorm(x, mean=μ, sd=σ)`
- Kwantyle: `qnorm(p, mean=μ, sd=σ)`
- Generowanie: `rnorm(n, mean=μ, sd=σ)`

### 2. Rozkład dwumianowy (Bernoulliego)

**Rozpoznawanie w zadaniu:**
- Eksperymenty z dwoma możliwymi wynikami (sukces/porażka)
- Liczba sukcesów w n niezależnych próbach o stałym prawdopodobieństwie p
- Słowa kluczowe: prawdopodobieństwo sukcesu, liczba prób, niezależne próby, zmienne dyskretne
- Przykłady: rzuty monetą, testy tak/nie, kontrola jakości (wadliwy/niewadliwy)

**Charakterystyki:**
- Parametry: n (liczba prób), p (prawdopodobieństwo sukcesu)
- Wartość oczekiwana: E(X) = n·p
- Wariancja: Var(X) = n·p·(1-p)
- Funkcja prawdopodobieństwa: P(X=k) = (n po k)·p^k·(1-p)^(n-k)

**W R:**
- Prawdopodobieństwo: `dbinom(x, size=n, prob=p)`
- Dystrybuanta: `pbinom(x, size=n, prob=p)`
- Kwantyle: `qbinom(p, size=n, prob=p)`
- Generowanie: `rbinom(m, size=n, prob=p)`

### 3. Rozkład Poissona

**Rozpoznawanie w zadaniu:**
- Liczba rzadkich zdarzeń w ustalonym przedziale (czasu, przestrzeni)
- Stała intensywność występowania zdarzeń
- Słowa kluczowe: intensywność, rzadkie zdarzenia, przedział czasu, liczba wystąpień
- Przykłady: liczba awarii, przybyć klientów, wad w materiale, wypadków

**Charakterystyki:**
- Parametr: λ (średnia liczba zdarzeń w przedziale)
- Wartość oczekiwana: E(X) = λ
- Wariancja: Var(X) = λ
- Funkcja prawdopodobieństwa: P(X=k) = (e^(-λ)·λ^k)/k!

**W R:**
- Prawdopodobieństwo: `dpois(x, lambda=λ)`
- Dystrybuanta: `ppois(x, lambda=λ)`
- Kwantyle: `qpois(p, lambda=λ)`
- Generowanie: `rpois(n, lambda=λ)`

### 4. Rozkład wykładniczy

**Rozpoznawanie w zadaniu:**
- Czas oczekiwania na zajście zdarzenia losowego
- Czas życia urządzeń, czas między awariami
- Związek z rozkładem Poissona (czas między zdarzeniami Poissona)
- Słowa kluczowe: czas oczekiwania, czas życia, intensywność, bez pamięci

**Charakterystyki:**
- Parametr: λ (intensywność)
- Wartość oczekiwana: E(X) = 1/λ
- Wariancja: Var(X) = 1/λ²
- Funkcja gęstości: f(x) = λe^(-λx) dla x ≥ 0

**W R:**
- Gęstość: `dexp(x, rate=λ)`
- Dystrybuanta: `pexp(x, rate=λ)`
- Kwantyle: `qexp(p, rate=λ)`
- Generowanie: `rexp(n, rate=λ)`

### 5. Rozkład jednostajny (równomierny)

**Rozpoznawanie w zadaniu:**
- Równe prawdopodobieństwo dla wszystkich wartości z przedziału
- Losowy wybór liczby z przedziału
- Wartości zaokrąglane do ustalonej liczby miejsc po przecinku
- Słowa kluczowe: równe szanse, przedział, losowy wybór

**Charakterystyki:**
- Parametry: a (minimum), b (maksimum)
- Wartość oczekiwana: E(X) = (a+b)/2
- Wariancja: Var(X) = (b-a)²/12
- Funkcja gęstości: f(x) = 1/(b-a) dla x ∈ [a,b]

**W R:**
- Gęstość: `dunif(x, min=a, max=b)`
- Dystrybuanta: `punif(x, min=a, max=b)`
- Kwantyle: `qunif(p, min=a, max=b)`
- Generowanie: `runif(n, min=a, max=b)`

### 6. Rozkład t-Studenta

**Rozpoznawanie w zadaniu:**
- Przedziały ufności dla średniej przy małych próbach i nieznanej wariancji
- Testowanie hipotez dotyczących średniej
- Słowa kluczowe: średnia, mała próba, nieznana wariancja, przedział ufności

**Charakterystyki:**
- Parametr: ν (stopnie swobody)
- Wartość oczekiwana: E(X) = 0 dla ν > 1
- Wariancja: Var(X) = ν/(ν-2) dla ν > 2
- Podobny do normalnego, ale ma cięższe ogony

**W R:**
- Gęstość: `dt(x, df=ν)`
- Dystrybuanta: `pt(x, df=ν)`
- Kwantyle: `qt(p, df=ν)`
- Generowanie: `rt(n, df=ν)`

### 7. Rozkład chi-kwadrat

**Rozpoznawanie w zadaniu:**
- Przedziały ufności dla wariancji
- Testy zgodności, testy niezależności
- Testowanie hipotez dotyczących wariancji
- Słowa kluczowe: wariancja, tabele kontyngencji, test zgodności

**Charakterystyki:**
- Parametr: k (stopnie swobody)
- Wartość oczekiwana: E(X) = k
- Wariancja: Var(X) = 2k
- Suma kwadratów k niezależnych zmiennych standardowych normalnych

**W R:**
- Gęstość: `dchisq(x, df=k)`
- Dystrybuanta: `pchisq(x, df=k)`
- Kwantyle: `qchisq(p, df=k)`
- Generowanie: `rchisq(n, df=k)`

### 8. Rozkład F Snedecora

**Rozpoznawanie w zadaniu:**
- Porównywanie wariancji dwóch populacji
- Analiza wariancji (ANOVA)
- Testowanie istotności w regresji liniowej
- Słowa kluczowe: porównanie wariancji, analiza wariancji, ANOVA, regresja

**Charakterystyki:**
- Parametry: d₁, d₂ (stopnie swobody)
- Wartość oczekiwana: E(X) = d₂/(d₂-2) dla d₂ > 2
- Wariancja: Var(X) = [2d₂²(d₁+d₂-2)]/[d₁(d₂-2)²(d₂-4)] dla d₂ > 4
- Iloraz dwóch niezależnych zmiennych chi-kwadrat podzielonych przez ich stopnie swobody

**W R:**
- Gęstość: `df(x, df1=d₁, df2=d₂)`
- Dystrybuanta: `pf(x, df1=d₁, df2=d₂)`
- Kwantyle: `qf(p, df1=d₁, df2=d₂)`
- Generowanie: `rf(n, df1=d₁, df2=d₂)`

### Wskazówki do rozpoznawania rozkładów w zadaniach:

1. **Normalny**: zmienne ciągłe z dużą liczbą czynników, pomiary fizyczne, biologiczne
2. **Dwumianowy**: zliczanie sukcesów w ustalonej liczbie prób
3. **Poissona**: rzadkie zdarzenia w czasie lub przestrzeni
4. **Wykładniczy**: czas do wystąpienia zdarzenia, czas życia urządzeń
5. **t-Studenta**: gdy wnioskujemy o średniej z małej próby
6. **Chi-kwadrat**: gdy wnioskujemy o wariancji lub testujemy zgodność
7. **F Snedecora**: gdy porównujemy wariancje lub oceniamy model regresji

### Przykłady słów-kluczy w zadaniach:

- **"Prawdopodobieństwo sukcesu"** → rozkład dwumianowy
- **"Czas do awarii"** → rozkład wykładniczy
- **"Liczba klientów w ciągu godziny"** → rozkład Poissona
- **"Wyniki testu z dużej grupy"** → rozkład normalny
- **"Przedział ufności dla średniej przy małej próbie"** → rozkład t-Studenta
- **"Test zgodności"** → rozkład chi-kwadrat
- **"Porównanie wariancji z dwóch grup"** → rozkład F Snedecora