---
title: Przykry błąd w nowej wersji WordPressa
author: sms
type: post
date: 2008-07-16T06:31:28+00:00
url: /2008/07/16/przykry-blad-w-nowej-wersji-wordpressa/
dsq_thread_id:
  - 2793738
  - 2793738
categories:
  - Internet
  - Technologie
tags:
  - błąd
  - permalink
  - WordPress

---
<a title="Google's new social networking site" href="http://www.flickr.com/photos/8044389@N04/2487944487/" target="_self"><img src="http://farm3.static.flickr.com/2250/2487944487_17afb0be23_m.jpg" border="0" alt="Google's new social networking site" /></a>
  
<small><a title="Attribution-ShareAlike License" href="http://creativecommons.org/licenses/by-sa/2.0/" target="_blank"><img src="http://www.dziennikarz.pl/wp-content/plugins/photo-dropper/images/cc.png" border="0" alt="Creative Commons License" width="16" height="16" align="absmiddle" /></a> <a href="http://www.photodropper.com/photos/" target="_blank">photo</a> credit: <a title="solbronumberone" href="http://www.flickr.com/photos/8044389@N04/2487944487/" target="_blank">solbronumberone</a></small>

Pojawiła się nowa wersja WordPressa a z nim dla wielu &#8211; szczególnie mało doświadczonych w hackowaniu blogerów &#8211; kłopot: poprawne generowanie permalinków. W efekcie czytelnicy mogą zamiast nowej notki zobaczyć błąd&#8230;404. Może to poważnie wpływać na oglądalność zarówno bezpośrednich odwiedzin jak i tych z np. Googla.<!--more-->

Problem polega w generowaniu permalinku. Standardowo w <a class="zem_slink" title="WordPress" rel="homepage" href="http://wordpress.org/">WordPress</a> adres notki przybiera format mało praktyczny np.  &#8222;http://www.dziennikarz.pl/?p=123&#8221; dlatego wielu blogerów zamienia go na lepiej indeksowany i pozycjonowany np.  &#8222;http://www.dziennikarz.pl/index.php/2008/07/16/sample-post/&#8221; .   No i tu pojawia się problem. Po upgradzie do wersji 2.6 te lepiej pozycjonowane czyli zawierające &#8222;index.php&#8221; przestają być widoczne, to znaczy po ich kliknięciu pojawia się owy błąd &#8222;404&#8221;.  Osobiście problem zauważyłem dopiero przed chwilą, już miałem zgłosić&#8230; gdy zobaczyłem, że sprawa jest <a href="http://trac.wordpress.org/ticket/7306" target="_self">znana</a>.

Całe szczęście, że rozwiązanie problemu jest banalnie proste. Wystarczy w ustawieniach permalinków dopisać (ustawienia opcjonalne) &#8222;category&#8221; oraz &#8222;tag&#8221; i wszystko wraca do normy.

<img class="alignnone" title="Permalink w WP" src="http://farm3.static.flickr.com/2362/2672924165_d6d7ec3a1a.jpg" alt="" width="500" height="214" />

Innym sposobem, którego nie próbowałem, ale <a href="http://wordpress.org/support/topic/189058" target="_self">opisane jest</a> w na forum WP, to usunięcie owego &#8222;index.php&#8221;.

Problem jak piszą w wyjaśnieniu twórcy WP leżał w błędnym opracowaniu rozwiązania permalinków aby były kompatybilne z serwerami IIS. Błąd ma być ostatecznie usunięty w kolejnej wersji WordPress.

<div class="zemanta-pixie" style="margin-top: 10px; height: 15px;">
  <a class="zemanta-pixie-a" title="Zemified by Zemanta" href="http://reblog.zemanta.com/zemified/f149d621-4d8f-46df-aad3-a6082a26bfbc/"><img class="zemanta-pixie-img" style="border: medium none; float: right;" src="http://img.zemanta.com/reblog_e.png?x-id=f149d621-4d8f-46df-aad3-a6082a26bfbc" alt="Zemanta Pixie" /></a>
</div>