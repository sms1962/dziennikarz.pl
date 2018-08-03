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

<iframe style="width: 80vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#%23defaultView%3ATimeline%0ASELECT%20%3FwyscigLabel%20%3Fdut%20%3FplaceLabel%20%3Fphoto%20%3Fart%0AWHERE%20%7B%0A%20%20%3Fwyscig%20wdt%3AP31%20wd%3AQ18608583%3B%0A%20%20%20%20%20%20%20%20%20%20wdt%3AP641%20wd%3AQ3609%3B%0A%20%20%20%20%20%20%20%20%20%20wdt%3AP571%20%3Fdut%3B%0A%20%20%20%20%20%20%20%20%20%20wdt%3AP17%20%3Fplace.%0A%20%20%3Fart%20schema%3Aabout%20%3Fwyscig.%0A%20%20%3Fart%20schema%3AisPartOf%20%3Chttps%3A%2F%2Fen.wikipedia.org%2F%3E%20.%0A%20%20OPTIONAL%20%7B%3Fwyscig%20wdt%3AP18%20%3Fphoto.%7D%20%0A%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cpl%22.%20%7D%0A%0A%7D%0AORDER%20BY%20%28YEAR%28%3Fdut%29%29" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>



