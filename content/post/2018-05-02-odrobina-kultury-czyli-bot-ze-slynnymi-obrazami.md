---
title: Odrobina kultury czyli bot ze słynnymi obrazami
author: sms
date: '2018-05-02'
slug: odrobina-kultury-czyli-bot-ze-slynnymi-obrazami
categories:
  - Twitter
tags: []
---

Od kilku tygodni na moim twiterowym koncie hula bot, który zrobiłem niejako przy okazji, bawiąc się danymi z Wikipedii. Trzy razy dziennie publikowana jest reprodukcja losowo wybranego obrazu wraz z linkiem do jego opisu na Wikipedii. Trudno jeszcze powiedzieć o efektach, więc krótko o pomyśle i jego realizacji.

![#OdrobinaKultury. Tweet z obrazem](/post/2018-05-02-odrobina-kultury-czyli-bot-ze-slynnymi-obrazami_files/Screenshot-2018-5-2 tag #odrobinaKultury na Twitterze.png)

W marcu potrzebowałem do jednego z projektów trochę danych, które zawierałyby współrzędne geograficzne. Wtedy też przypomniałem sobie o odłożonym "na kiedyś" pomyśle by nauczyć się pobierania danych z Wikipedii, co teraz gdy projekt Wikidata - czyli semantycznej bazy wiedzy - mocno okrzepł jest stosunkowo proste. 

Wikidata, a właściwie po polsku Wikidane, jesli ktoś nie wie, to bardzo ciekawy projekt, rozwijany od kilku lat przez fundację Wikimedia, który zyskał ogromne wsparcie od Googla, gdy ten przestał rozwijać swój podobny projekt Freebase. O semantycznym internecie mówi się od dobrych kilku lat, ale teraz rzeczywiście zaczyna on się realizować i sądzę, że za rok, dwa, to Wikidane będą dla nas jednym z ważniejszych źródeł pozyskiwania danych. 

Czym różni się Wikipedia od Wikidanych? Nieco upraszczając, w tej pierwszej, wiedza zgromadzona jest w artykułach, które grupowane są na różny sposób np. w formie list. Wikipedia składa się z wielu (ponad 200) narodowych wersji, w których spora część haseł się pokrywa, ale wielkość i zawartość artykułów, jest najczęściej inna. Wikidane to pomysł by fakty i informacje zebrać w jednej, niezależnej od języka bazie, a obiekty i ich właściwości miały unikalne identyfikatory. Dzięki czemu np. jeśli zapytamy o "Fyderyka Szopena"" to Wikidane znajdą nam te same informacje, jak byśmy zapytali o "Frederic Chopin". 

Niestety nie ma nic za darmo. O ile Wikipedią może posługiwać się praktycznie każdy, kto potrafi w wyszukiwarce wpisać szukane hasło, to w przypadku Wikidanych, musimy tworzyć mini skrypty w specjalnym języku SPARQL. Nie jest on bardzo trudny, ale dla osób, które nigdy nie programowały, niewątpliwie będzie stanowił wyzwanie. Trud nauczenia się posługiwania Wikidanymi nagrodzony jest zupełnie nowymi możliwościami zdobywania informacji. Na przykład możemy w czasie mniejszym niż minuta znaleźć kompozytorów, którzy mieli na imię "Jan". Tak wygląda skrypt wykonujący to zadanie:

```
SELECT ?osoba ?osobaLabel WHERE {
  ?osoba wdt:P106 wd:Q36834;    # Osoba zajmuje się komponowaniem
         wdt:P735 wd:Q12173670. # Osoba ma na imię Jan
  
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }

}
```
Zobacz jak wygląda [efekt działania skryptu](http://tinyurl.com/y9pxr72t).

Robiąc sobie wprawki w SPARQL wykonałem pewnie kilkaset  różnych zapytań. Jednym z nich było zapytanie o obrazy jakie znajdują się w Wikidanych. Zdefiniowałem, że chcę następujące elementy:

- plik graficzny z obrazem, 
- datę powstania obrazu, 
- imię i nazwisko malarza
- oraz miejsce gdzie obraz się znajduje. 

Dodatkowo zleciłem by do każdego obrazu pobrany został link do artykułu w Wikipedii - bo lubię sobie poczytać o czymś, co mi się spodoba, a w artykułach często są bardzo ciekawe informacje np. o historii obrazu, jego losach, osobach czy miejscach, które przedstawia itp. Ograniczyłem też pobieranie danych jedynie do polskiej Wikipedii, bo po pierwsze z wszystkich Wikipedii skrypt pobrał kilkadziesiąt tysięcy obrazów, a po drugie uznałem, że może jak artykuły będą po polsku, to internauci chętniej je przeczytają. 

W sumie mój skrypt wyszukał 2150 obrazów, które spełniały wszystkie warunki, to znaczy był plik graficzny, data powstania obrazu, autor i link do artykułu w polskiej Wikipedii. 

Gdy zobaczyłem obrazy i dodatkowe o nich informacje natychmiast pojawiła się myśl, by zrobić z tego bota, który będzie je publikował na Twitterze. Tworzenie skryptów-automatów nie jest dla mnie tajemnicą i kilka takich działa na moim koncie, więc po 10 minutach gotowy był nowy bot, który trzy razy dziennie:

- wykonuje zapytanie do Wikidanych i pobiera obrazy i dane o nich
- usuwa te, które zostały już opublikowane
- losuje jeden z obrazów
- z danych o obrazie tworzy opis
- publikuje tweeta
- zapisuje w specjalnym pliku, obrazy już opublikowane

Opis tworzony jest wg. szablonu gdzie część tekstu jest z góry określona, a niektóre elementy jak np. nazwa obrazu, nazwisko malarza etc. są wstawiane z danych o obrazie. Dodatkowo skrypt bota oblicza liczbę lat jaka upłynęła od powstania obrazu. 

No i tak sobie ten skrypt działa i mniej więcej przez trzy tygodnie - łącznie z różnymi próbami, "opublikował" 61 obrazów. Dodałem jeszcze  hashtag #odrobinaKultury by można było w prosty sposób grupować opublikowane obrazy np. gdy ktoś przegapił tweeta, albo wyjechał na urlop. Mała rzecz, a przydatna.

Jak wspomniałem, jednym z powodów powstania bota była chęć wykorzystania wiedzy w posługiwaniu się Wikidanymi. Drugi powód wynikał z obserwacji Twittera, w którym strasznie dużo jest polityki - co zasadniczo mi nie przeszkadza - ale niestety gdzieś znikły ciekawe nieraz wymiany poglądów, które zastąpione zostały "okładaniem się maczugami" przez zaantagonizowane strony. W efekcie, po 5 minutach czytania tajmlajna wiem doskonale jakie są "przekazy dnia" i jakich argumentów używać będą zaangażowani twitterowicze. To na dłuższą metę nudne. Pomyślałem więc, że może z jednej strony obrazy wielkich malarzy wpłyną odrobinę na rozpalone głowy, które na chwilkę przynajmniej zasępią się i pomyślą nad obrazem. Czy to się udało? Nie wiem i raczej wątpię. Po drugie - z czysto egostycznego punktu widzenia - zachciałem mieć codziennie kilka obrazów, którym mógłbym nacieszyć oko.

Po kilku tygodniach, mogę śmiało powiedzieć, że mnie ta codzienna dawka sztuki bardzo się podoba, a skrypt o papu nie woła, więc na razie zostanie. Jedyną wątpliwośc jaką mam, to pytanie czy nie przenieść bota z mojego konta na inne - dedykowane. Na świecie większośc autorów botów tak robi. Nie mam tu gotowej odpowiedzi. Są zalety takiego rozwiązania zarówno dla mnie, jak i tych, którzy chcą oglądać obrazy. Na razie zostaje na moim koncie, bo tak coś czuję, że przeniesienie na dedykowane, skończyłoby się tym, że pewnie sporej części obrazów bym po prostu nie zauważył. 

Jesli macie jakieś uwagi, sugestie, komentarze to proszę albo na dole, pod tekstem, albo na [Twitterze](http://twitter.com/dziennikarz)

Jeśli ktoś niewidział obrazów już opublikowanych z hashtagiem #odrobinaKultury to wystarczy kliknąć w [ten link](https://twitter.com/hashtag/odrobinaKultury?src=hash) by zobaczyć dotychczas opublikowane.