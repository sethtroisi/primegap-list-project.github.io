---
layout: post
author: Graham Higgins
category: project
title: How to process SQL results of checking
tags: post project
excerpt: A walkthrough of the process of updating the list of known first occurrence prime gaps
---

#### Publication format

The list of first known occurrence gaps is published as a plaintext file of SQL statements `allgaps.sql` which, when read into a SQL-aware application, constructs two relational tables of data: `gaps` and `credits`.

The `gaps` table contains the data previously published by Dr Thomas Ray Nicely as a spatially-formatted plaintext file `allgaps.dat`. Archival versions of this data [remain accessible as captures](https://web.archive.org/web/*/http://www.trnicely.net/gaps/allgaps.dat) courtesy of archive.org’s “Wayback Machine”.

The `credits` table is taken from the one published by Dr. Nicely in a web page “First known occurrence of prime gaps”, [similarly accessible](https://web.archive.org/web/*/http://www.trnicely.net/gaps/gaplist.html) as captured by the “Wayback Machine”. The `credits` table provides a mapping from the abbreviations of names of discoverers used in the `gaps` table to the full details.

##### Database schema for `gaps` table

```sql
CREATE TABLE gaps(
  "gapsize" INTEGER,
  "ismax" BOOLEAN,
  "primecat" TEXT,
  "isfirst" TEXT,
  "primecert" TEXT,
  "discoverer" TEXT,
  "year" INTEGER,
  "merit" REAL,
  "primedigits" INTEGER,
  "startprime" TEXT
);
```

The domain semantics of the data fields are described [in a separate document](/prime-gap-record-data-fields/) and are reproduced below for convenience.

> The text of this characterisation is taken from Dr. Thomas R. Nicely‘s original description presented in [“First Occurrence Prime Gaps”](https://web.archive.org/web/20191118035255/http://www.trnicely.net/gaps/gaplist.html). Dr. Nicely’s references to spatial positioning and sequence have been replaced by *ad hoc* terminological labels in order to distinguish the data fields.
> 
> i) ***gapsize***
> 
> This field contains the size or measure of the gap (difference of the bounding primes).
> 
> ii) ***ismax***
> 
> The gap is a MAXIMAL gap, strictly exceeding in measure all the prime gaps preceding it (those between consecutive prime numbers smaller in magnitude). In this case, it will in addition always be a definite first occurrence and certified.
> 
> iii) ***primecat***
> 
> This field indicates the type of the gap. All of the gaps in this list are “conventional” (common, classic, standard, regular, ordinary, normal) prime gaps, indicated by the letter “C”; in other words, consecutive prime numbers differing by the measure of the gap, as defined by conditions (1) and (2) alone from the above definition of first occurrence prime gaps. This is the default; if the term “prime gap” is used without further qualification or elaboration, it refers to a conventional prime gap. Additional lists are planned, enumerating other types of prime gaps.
> 
> iv) ***isfirst***
> 
> This field indicates the first occurrence status of the prime gap.
> 
> - The character “F” signifies that the gap has definitely been established (by an exhaustive scan to or beyond that point) as a first occurrence prime gap.
> - The character “N” signifies that the gap is definitely not a first occurrence (a prior occurrence is known).
> - The character “?” signifies that the gap is a first known occurrence (no such gap with smaller bounding primes has been found), but that it is not presently known if it is the first occurrence (i.e., whether or not a gap of equal measure with smaller bounding primes exists).
> 
> All gaps presently in this list are first known occurrences not known (or expected) to be first occurrences; presumably, as the list evolves, entries will occasionally be replaced by newly discovered smaller instances of gaps.
> 
> v) ***primecert***
> 
> This field indicates whether the bounding integers of the gap are certified primes (“C”) or probabilistic primes (“P”). The bounding integers of certified gaps (also titled confirmed, conclusive, deterministic, definite, definitive, or proven) have been conclusively proven prime, using trial prime divisors to the square root of the prime, or a test such as APRCL2 (Adleman-Pomerance-Rumely-Cohen-Lenstra-Lenstra).
> 
> The gap is probabilistic (also titled “Monte Carlo”) if the bounding integers have only been shown statistically prime (with a probability extremely close to one), using, for example, Miller’s test with multiple bases. For extremely large integers (hundreds or thousands of digits), probabilistic tests are orders of magnitude faster than deterministic tests, but nonetheless become time consuming in the thousands of digits.
> 
> > I attempt to personally certify the smaller gaps (to perhaps 100 digits), and to verify probabilistically larger gaps (to perhaps 500 digits). For gaps with even larger initiating primes, I must rely on the discoverer’s report and the vigilance of third parties. *Declaration by originator and maintainer Dr. Thomas R. Nicely*
> 
> In all cases, the interior integers of the gaps have been certified deterministically to be composite, using, for example, trial divisors, Fermat’s test, or Miller’s test.
> 
> vi) ***discoverer***
> 
> This field contains an abbreviation of the listed discoverers. A key of abbreviations to full names (and credit acknowledgements) is maintained separately.
> 
> vii) ***year***
> 
> This field reflects the most accurate value known for the actual date of discovery; if this is not known, the date of publication or the date of the preprint is shown; if this is not known, an estimate is given.
> 
> viii) ***merit***
> 
> This field states a so-called figure of merit for the gap. This indicates how much larger the gap is than the average gap (approximately ln(x), as a consequence of the Prime Number Theorem) between primes near that point; the greater the merit, the more unusual the gap. The merit is computed as <math>G/ln(p<sub>1</sub>)</math>; variations in use (and at one time employed in these tables) include <math>G/ln(p<sub>2</sub>)</math> and <math>G/ln((p<sub>1</sub> + p<sub>2</sub>)/2)</math>, where <math>p<sub>1</sub></math> and <math>p<sub>2</sub></math> are the initiating and terminating primes of the gap. For all but the first few gaps, the differences among these formulas are trivial; indeed, if the results are rounded to two decimal places (as herein), I (Dr. Thomas R. Nicely) have found no discrepancies in the resulting values for any gap exceeding 112.
> 
> ix) ***primedigits***
> 
> This field indicates the number of decimal digits in the initiating prime.
> 
> x) ***primestart***
> 
> This field shows the initiating prime (smaller bounding integer) of the gap.
> 
> Initiating primes longer than 200 decimal digits are subject to abbreviation, unless they can be represented by a simple formula (such as <math>10^999 + 7</math>). This unfortunate policy is implemented due primarily to a shortage of bandwidth. As the listing grows, additional restrictions of this type may become necessary, including bounds on gap sizes, figures of merit, or the size of the initiating primes.
> 
> If the complete expansion of an abbreviated prime is desired, I recommend that you contact the discoverer.


##### Database schema for `credits` table


```sql
CREATE TABLE credits(
  "abbreviation" TEXT,
  "name" TEXT,
  "ack" TEXT,
  "display" TEXT
);
```

In which `abbreviation` is a key to the abbreviations used in `gaps` for discoverers’ names and `name` is the indexed-to string originally published by Dr. Nicely (see below) with the credit acknowledgements (e.g. “(PGS)”, “Computer codes by Tomás Oliveira e Silva.”) separated out into the `ack` field. The `display` field is used for display purposes and is the discoverer’s name(s) plus a shortened form of the credit acknowledgement (e.g. “Robert W. Smith [Dana Jacobsen]”).

**“Abbreviations for Discoverers” as last published by Dr. Thomas Ray Nicely**

    ANair_MF---Anand S. Nair (PGS).
    APinhTOS---Armando Pinho. Computer codes by Tomás Oliveira e Silva.
    A.Walker---Andrew John Walker.
    AEWestrn---A. E. Western.
    Andersen---Jens Kruse Andersen.
    ApplRssr---Kenneth I. Appel and J. Barkley Rosser.
    ATeixTOS---António Teixera. Computer codes by Tomás Oliveira e Silva.
    Be.Nyman---Bertil Nyman.
    Blnchtte---Gilles Blanchette.
    CBastTOS---Carlos Bastos. Computer codes by Tomás Oliveira e Silva.
    CKernTOS---Cristian Kern. Computer codes by Tomás Oliveira e Silva.
    ColeStev---Steve Cole (PGS).
    DanielH.---Daniel Hermle.
    DBghFOH---D.; Baugh and F. O'Hara.
    DHLehmer---Derrick Henry Lehmer.
    DonKnuth---Donald Ervin Knuth.
    Erickson---Eddie Erickson.
    Euclid  ---Euclid.
    Fougeron---Jim Fougeron.
    GABandAR---F. J. Gruenberger, G. Armerding, and C. L. Baker (1959, 1961),
           and independently, Kenneth I. Appel and J. Barkley Rosser (1961).
    Gapcoin----The Gapcoin network,
           a Bitcoin derivative, employs a hashing algorithm which searches
           for prime gaps of high merit. Jonnie Frey, developer.
    Glaisher---J. W. L. Glaisher.
    H.Dubner---Harvey Dubner.
    HrzogTOS---Siegfried "Zig" Herzog. Computer codes by Tomás Oliveira e Silva.
    Jacobsen---Dana Jacobsen, running code using C and Perl.
    JamesFry---James Fry.
    JdeGroot---Jeroen de Groot.
    JFNSTOeS---John Fettig and Nahil Sobh, NCSA. Computer codes by Tomás Oliveira e Silva.
    JLGPardo---Jose Luis Gomez Pardo.
    JRdrgTOS---João Manuel Rodrigues. Computer codes by Tomás Oliveira e Silva.
    K.Conrow---Kenneth Conrow.
    KOGrndln---Kjell-Olav Grøndalen.
    _Kokales---David Kokales. Also contributed deterministic primality proofs.
    LLnhardy---Leif Leonhardy.
    LMorelli---Luigi Morelli (PGS).
    LndrPrkn---L. J. Lander and Thomas R. Parkin.
    M.Jansen---Michiel Jansen.
    MJandJKA---Michiel Jansen and Jens Kruse Andersen.
    MJPCJKA---Michiel; Jansen, Pierre Cami, and Jens Kruse Andersen.
    ML.Brown---Milton L. Brown.
    MrtnRaab---Martin Raab.
    NicelyHD---Thomas R. Nicely. Computer codes inspired by Harvey Dubner's work.
    NoAttrib---Anonymous contributors who do not wish attribution.
    NuuKuosa---Nuutti Kuosa.
    PardiTOS---Silvio Pardi. Computer codes by Tomás Oliveira e Silva.
    PDeGeest---Patrick De Geest.
    PierCami---Pierre Cami.
    Pinho_MF---Carlos Eduardo Leal de Pinho (PGS).
    R.Athale---Rahul Ramesh Athale.
    RFischer---Richard Fischer.
    Ritschel---Thomas Ritschel (PGS).
    RobSmith---Robert W. Smith. Some of Smith's results after 2014 employ
           Perl code written by Dana Jacobsen. Coordinator, PGS.
    Rosnthal---Hans Rosenthal.
    RosntlJA---Hans Rosenthal. Computer codes by Jens Kruse Andersen.
    RosntlJF---Hans Rosenthal. Computer codes by Jim Fougeron.
    RP.Brent---Richard P. Brent.
    Shepherd---Rick L. Shepherd.
    Spielaur---Helmut Spielauer.
    TAlmFMJA---Torbjörn Alm. Computer codes by Jens Kruse Andersen.
               Deterministic primality proofs by François Morain.
    T.Hadley---Thomas Hadley.
    TOeSilva---Tomás Oliveira e Silva.
    Toni_Key---Antonio Key, using Perl codes developed by Dana Jacobsen.
    TorAlmJA---Torbjörn Alm. Computer codes by Jens Kruse Andersen.
    TRNicely---Thomas R. Nicely.
    Weslwski---Arkadiusz Wesołowski.
    Yng&Ptlr---Jeff; Young and Aaron Potler.
    YPPauloR---Jeff Young and Aaron Potler, as reported by Paulo Ribenboim.

This list of discoverers was hand-formatted as CSV

##### A relational database representation of the list of known first occurrence prime gaps

A [SQLite](https://www.sqlite.org/) database is a single disk file. The file format is cross-platform. A database that is created on one machine can be copied and used on a different machine with a different architecture. SQLite databases are portable across 32-bit and 64-bit machines and between big-endian and little-endian architectures. 


Each value stored in an SQLite database (or manipulated by the database engine) has one of the following storage classes:

    NULL. The value is a NULL value.

    INTEGER. The value is a signed integer, stored in 1, 2, 3, 4, 6, or 8 
             bytes depending on the magnitude of the value.

    REAL. The value is a floating point value, stored as an 8-byte
          IEEE floating point number.

    TEXT. The value is a text string, stored using the database
          encoding (UTF-8, UTF-16BE or UTF-16LE).

    BLOB. The value is a blob of data, stored exactly as it was input.


**Create schema for `gaps` and `credits` tables**

(Lines split for presentation, so not copy’n’pastable as displayed, needs collapsing into one line)

```shell
printf 'CREATE TABLE gaps (
    gapsize INTEGER,
    ismax BOOLEAN,
    primecat TEXT,
    isfirst TEXT,
    primecert TEXT,
    discoverer TEXT,
    year INTEGER,
    merit REAL,
    primedigits INTEGER,
    startprime BLOB
    );\n
    CREATE TABLE credits (
        abbreviation TEXT,
        name TEXT,
        ack TEXT,
        display TEXT
    );\n
    .save allgaps.db\n' | sqlite3
```

### Construction of contemporary list of first known occurrences from archive.org captures

**Dump entire database as SQL**

```shell
sqlite3 allgaps.db .dump > allgaps.sql
```

```shell
printf '.open allgaps.db\n
    .read allgaps.sql\n
    .mode csv\n
    .import credits.csv credits\n' | sqlite3
```
### Publishing of contemporary list for committing to primegap-list-project.github.io

**Publish `allgaps.csv`**

```shell
sqlite3 -csv allgaps.db "select * from gaps;" > allgaps.csv
```

**Publish `credits.csv`**

```shell
sqlite3 -csv allgaps.db "select * from credits;" > credits.csv
```

### Loading of contemporary list prior to loading results from javascript checker

**Load from SQL**

```shell
sqlite>.read allgaps.sql
```

### One-line shell idioms

```shell
printf '.mode csv\n.import /tmp/deleteme.csv users\n' | sqlite3 test.db
```

```shell
sqlite3 allgaps.db <<<$'.mode csv\n.import /tmp/deleteme.csv users\n'
```

```shell
sqlite3 allgaps.db <<<$'.dump\n' > allgaps.sql
```
