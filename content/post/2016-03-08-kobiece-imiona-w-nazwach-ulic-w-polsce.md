---
title: Kobiece imiona w nazwach ulic w Polsce
author: sms
type: post
date: 2016-03-08T10:40:56+00:00
url: /2016/03/08/kobiece-imiona-w-nazwach-ulic-w-polsce/
dsq_thread_id:
  - 4644171380
categories:
  - Ranking

---
Bawię się ostatnio katalogiem ulic, bazą prowadzoną przez Główny Urząd Statystyczny w ramach rejestru TERYT. Jako, że dzisiaj Dzień Kobiet to BiqData opublikował fajne badanie &#8222;[Mapa stolicy. Zobacz, gdzie patronkami ulic są kobiety][1]&#8222;. Nie będę gorszy :-), więc zadałem sobie proste pytanie: ile polskich ulic ma kobiety za patronki?

<!--more-->

W katalogu znajdują się 256 tys. 852 ulice. Sporo. Wyłuskanie ręczne kobiet patronek jest możliwe, ale trwałoby pewnie do przyszłorocznego Dnia Kobiet, dlatego musiałem sobie wymyślić jakiś sposób.

W katalogu ulic występują dwie zmienne: Nazwa\_1 i Nazwa\_2. Pierwsza zawiera Nazwisko patrona, druga jego imię. Niestety gdyby tak było dokładnie, to byłoby za prosto, dlatego urzędnicy nadający nazwy ulic postanowili nieco utrudnić sprawę podając np. w zmiennych inne elementy występujące w nazwach np. tytuł (&#8222;prof.&#8221;, &#8222;św.&#8221; etc.), drugie imię etc. Z drugiej jednak strony chwała urzędnikom za to, że nazwy ulic są podane w formie odmienionej, co baaaardzo ułatwia sprawę.

Sam algorytm okazał się dość prosty:

  1. Wyszukaj w zmiennej Nazwa_1 wszystkie wystąpienia, gdzie wyraz kończy się na &#8222;i&#8221; lub &#8222;y&#8221;, czyli np. &#8222;Marii&#8221; albo &#8222;Anny&#8221;.
  2. Usuń te, które składają się z więcej niż 1 wyrazu, czyli wszystkie typu &#8222;Marii Magdaleny&#8221;

Punkt 2 algorytmu wprowadza pewną niedokładność, bo przykładowa &#8222;Maria Magdalena&#8221; z pewnością była kobietą, a więc jako patronka powinna być uwzględniona. Świadomie jednak zdecydowałem się na takie uproszczenie z prostej przyczyny: to nie doktorat, więc nie chciałem poświęcać za dużo czasu. Poza tym nawet uwzględniwszy dwuczłonowe nazwy, ogólna liczba patronek znacząco się nie zwiększy.

Komputer zabuczał i po chwili miałem 2887 nazw ulic w których występują kobiece imiona (156 unikalnych), co stanowi 1.1 proc. wszystkich (256 tys.852) nazw ulic w Polsce. Czy to dużo czy mało? Oczywiście mało.

Na koniec zrobiłem ranking popularności imion i graficznie przedstawiającą go chmurkę. Wynika z niego, że z kobiecych imion najczęściej w nazwach ulic występuje imię &#8222;Maria&#8221; (1065 razy). Potem długo, długo nic i &#8222;Eliza&#8221; (305 razy). Trzecie miejsce to &#8222;Zofia&#8221; (175 razy).

Poniżej chmurka z imionami i na koniec dla ciekawskich <a href="http://dziennikarz.pl/inne/kobietyimiona.html" target="_blank">pełny ranking imion</a>.

<img class="aligncenter size-full wp-image-1538" src="http://dziennikarz.pl/wp-content/uploads/2016/03/kobietyImiona.png" alt="kobiece Imiona w nazwach polskich ulic" width="884" height="544" srcset="http://dziennikarz.pl/wp-content/uploads/2016/03/kobietyImiona.png 884w, http://dziennikarz.pl/wp-content/uploads/2016/03/kobietyImiona-300x185.png 300w, http://dziennikarz.pl/wp-content/uploads/2016/03/kobietyImiona-768x473.png 768w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 1362px) 62vw, 840px" />

&nbsp;

No i na koniec: wszystkim dziewczynkom, dziewczynom i kobietom w dniu ich święta: po prostu szczęścia.

&nbsp;

 [1]: http://biqdata.wyborcza.pl/warszawskie-ulice-zobacz-jak-malo-kobiet-jest-patronkami-ulic