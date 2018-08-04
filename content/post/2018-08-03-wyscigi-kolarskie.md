---
title: Wyscigi kolarskie
author: sms
date: '2018-08-03'
slug: wyscigi-kolarskie
categories: []
tags: []
---

Jutro startuje [Tour de Pologne](http://tourdepologne.pl) i chociaż nie jestem specjalnie fanem kolarstwa, to zawsze to jakaś okazja by coś się dowiedzieć. Pomyslałem: a gdyby tak sprawdzić ile jest i od kiedy są wyścigi kolarskie?

Idealnie do takiego zadania nadaje się Wikipedia, a najlepiej jej semantyczna odmiana [Wikidata](http://wikidata.org). Napisałem niewielkie zapytanie, jak poniżej i po chwili miałem odpowiedź w postaci prostej, ale całkiem fajnej osi czasu (timeline).

```
#defaultView:Timeline
SELECT ?wyscig ?wyscigLabel ?dut ?placeLabel ?photo ?art
WHERE {
  ?wyscig wdt:P31 wd:Q18608583;
          wdt:P641 wd:Q3609;
          wdt:P571 ?dut;
          wdt:P17 ?place.
  ?art schema:about ?wyscig.
  ?art schema:isPartOf <https://en.wikipedia.org/> .
  OPTIONAL {?wyscig wdt:P18 ?photo.} 
  
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],pl". }

}

ORDER BY (YEAR(?dut))

```
Jeśli chcesz zobaczyć jak wynik działania skryptu w Wikidata to [kliknij tu](http://tinyurl.com/ybo958py). Można też kod do wyniku osadzić na stronie i będzie wyglądał tak jak poniżej. Jakby komuś coś nie teges, albo oglada na smartfoniu, [to tu w wersji tabelarycznej.](http://tinyurl.com/ydc3uqhe)

To by było na tyle. Miłego klikania.

Adieu

*Dodane 04.08.2018* 
Po opublikowaniu twita okazało się, że życie nie jest takie proste. Odezwała się [Arlena Sokalska](https://twitter.com/ArlenaSokalska), dziennikarka i znawca kolarstwa, która wytknęła wiele braków w spisie.

{{< tweet 1025424985639153666 >}}

Poprawienie wyników wymagało odemnie zmiany konstrukcji zapytania. Nie będę teraz tłumaczył dlaczego, to w osobnym wpisie, bo to ciekawe, w każdym razie nowa wersja zapytania wygląda tak:

````
# Wyścigi kolarskie jedno i wieloetapowe

SELECT ?wyscigLabel ?rok ?czestotliwosc ?panstwoLabel ?artykul ?foto
WHERE {
  ?wyscig wdt:P641 wd:Q3609 ;
          wdt:P2257 ?czestotliwosc .
  OPTIONAL {?wyscig wdt:P31 wd:Q18608583 .}
  OPTIONAL {?wyscig wdt:P279 wd:Q2912397.}
  OPTIONAL {?wyscig wdt:279 wd:Q1318941 .}
  ?wyscig wdt:P571 ?dut. 
  BIND (YEAR(?dut) AS ?rok) .
  OPTIONAL {?wyscig wdt:P17 ?panstwo .}
  OPTIONAL {?wyscig wdt:P18 ?foto .}
  OPTIONAL {?artykul schema:about ?wyscig .
            ?artykul schema:isPartOf <https://en.wikipedia.org/> .}
 
  
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],pl, en, fr, de, it, nl, es". }

}
ORDER BY (?rok)
````
Jeśli chcesz zobaczyć wynik działania skryptu w [Wikidata](http://wikidata.org) to [kliknij tu](http://tinyurl.com/yb5noq3f)

Końcowy wynik z ponad siedemset wyścigami kolarskimi od końca XIX wieku do czasów współczesnych wygląda tak:

<iframe style="width: 80vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#%23%20Wy%C5%9Bcigi%20kolarskie%20jedno%20i%20wieloetapowe%0A%0ASELECT%20%3FwyscigLabel%20%3Frok%20%3Fczestotliwosc%20%3FpanstwoLabel%20%3Fartykul%20%3Ffoto%0AWHERE%20%7B%0A%20%20%3Fwyscig%20wdt%3AP641%20wd%3AQ3609%20%3B%0A%20%20%20%20%20%20%20%20%20%20wdt%3AP2257%20%3Fczestotliwosc%20.%0A%20%20OPTIONAL%20%7B%3Fwyscig%20wdt%3AP31%20wd%3AQ18608583%20.%7D%0A%20%20OPTIONAL%20%7B%3Fwyscig%20wdt%3AP279%20wd%3AQ2912397.%7D%0A%20%20OPTIONAL%20%7B%3Fwyscig%20wdt%3A279%20wd%3AQ1318941%20.%7D%0A%20%20%3Fwyscig%20wdt%3AP571%20%3Fdut.%20%0A%20%20BIND%20%28YEAR%28%3Fdut%29%20AS%20%3Frok%29%20.%0A%20%20OPTIONAL%20%7B%3Fwyscig%20wdt%3AP17%20%3Fpanstwo%20.%7D%0A%20%20OPTIONAL%20%7B%3Fwyscig%20wdt%3AP18%20%3Ffoto%20.%7D%0A%20%20OPTIONAL%20%7B%3Fartykul%20schema%3Aabout%20%3Fwyscig%20.%0A%20%20%20%20%20%20%20%20%20%20%20%20%3Fartykul%20schema%3AisPartOf%20%3Chttps%3A%2F%2Fen.wikipedia.org%2F%3E%20.%7D%0A%20%0A%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cpl%2C%20en%2C%20fr%2C%20de%2C%20it%2C%20nl%2C%20es%22.%20%7D%0A%0A%7D%0AORDER%20BY%20%28%3Frok%29" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

Można te dane przedstawić w innej, zbiorczej formie. [Na przykład w którym kraju jest najwięcej wyścigów kolarskich?](http://tinyurl.com/y9prltsw) Niestety wynik, który poniżej, może być obarczony sporym błędem bo przy ponad 200 wyścigach na ogólną sumę ponad 700, nie ma informacji o kraju w którym się impreza odbywa.

![](/static/img/wyscigi_bubble.png)









