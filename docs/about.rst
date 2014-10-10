Über das Projekt
================

Composer ist eine Paketverwaltung für PHP, entwickelt von `Nils Adermann`_ und `Jordi Boggiano`_.
Im Gegensatz zu anderen Paketverwaltungen für PHP (wie PEAR und PECL) ist Composer selbst
in PHP geschrieben und lässt sich daher auf jedem PHP fähigen System benutzen, also auch auf Shared Hostern.

Die Integration von Composer in Contao wurde Anfang 2013 von `Dominik Zogg`_ und `Tristan Lins`_ initiiert.
Aus einer einfachen Integration auf Konsolenbasis wurde ein umfangreicher Client mit Integration in das Contao Backend
- der sogenannte *Contao Composer Client*. Um diesen Client entwickelt sich ein entsprechendes Ökosystem,
dass zusammenfassend als als *Contao Composer Projekt* bezeichnet wird.

Das *Contao Composer Projekt* umfasst folgende Teilprojekte:

* Der :ref:`contao_composer_client` ist die Integration in Contao.
* Das :ref:`contao_composer_plugin` stellt den Installer für Composer bereit.
* Das :ref:`contao_composer_repository` ist ein für das Contao Umfeld angepasster Paketserver auf Basis von
  `Packagist <https://packagist.org/>`_.
* Die :ref:`contao_composer_documentation` ist *diese* Dokumentation.

Unterstützung des Extension Repository 2
----------------------------------------

Für den vereinfachten Übergang von dem Extension Repository 2 betreibt die `Contao Community Alliance`_ ein `Repository
<http://legacy-packages-via.contao-community-alliance.org/>`_, über das die alten *Legacy* Pakete aus dem Extension
Repository 2 mit Composer installiert werden können.

Finanzierung
------------

Langfristig soll soll das Projekt durch die `Contao Association`_ finanziell
gefördert werden. Ein entsprechender Antrag wird noch 2014 eingereicht.

Maintainer
----------

Heute wird das Projekt von `Christian Schiffler`_ und `Tristan Lins`_ betreut, die bereits hinter der Planung
zum Extension Repository 3 (auch bekannt als RFCCC-1) stehen.

Mitwirkende
-----------

.. role:: contributors

.. compound::

   :contributors:`Die Liste der Mitwirkenden kann online eingesehen werden:`

   * `contao-community-alliance/composer-client
     <https://github.com/contao-community-alliance/composer-client/graphs/contributors>`_
   * `contao-community-alliance/composer-plugin
     <https://github.com/contao-community-alliance/composer-plugin/graphs/contributors>`_
   * `contao-community-alliance/composer-repository
     <https://github.com/contao-community-alliance/composer-repository/graphs/contributors>`_
   * `contao-community-alliance/composer-docs-de
     <https://github.com/contao-community-alliance/composer-docs-de/graphs/contributors>`_

.. raw:: html

   <script>
   (function(){
       var contributors = {};
       var repositories = [
           'contao-community-alliance/composer-client',
           'contao-community-alliance/composer-plugin',
           'contao-community-alliance/composer-repository',
           'contao-community-alliance/composer-docs-de'
       ];

       var load = function(repository) {
           var request = new XMLHttpRequest();
           request.onreadystatechange = function() {
               if (request.readyState == 4) {
                   if (request.status == 200) {
                       var list = JSON.parse(request.responseText);
                       list.forEach(function(contributor) {
                           if (contributors[contributor.login]) {
                               contributors[contributor.login].contributions += contributor.contributions;
                           } else {
                               contributors[contributor.login] = {
                                   name: contributor.login,
                                   url: contributor.html_url,
                                   avatar: contributor.avatar_url,
                                   contributions: contributor.contributions
                               };
                           }
                       });
                   }
                   if (repositories.length) {
                       load(repositories.shift());
                   } else {
                       build();
                   }
               }
           }
           request.open('GET', 'https://api.github.com/repos/' + repository + '/contributors', true);
           request.send(null);
       };

       var build = function() {
           var sorted = [];
           Object.keys(contributors).forEach(function(key) {
               sorted.push(contributors[key]);
           });

           sorted = sorted.sort(function(left, right) {
               if (left.contributions == right.contributions) {
                   return right.name.localeCompare(left.name);
               } else {
                   return right.contributions - left.contributions;
               }
           });

           var html = '<ul>';
           sorted.forEach(function(contributor) {
               html += '<li>';
               html += '<a href=":href:" target="_blank"><img src=":src:" width="24" style="vertical-align:middle;"> :name:</a>'
                   .replace(':name:', contributor.name)
                   .replace(':href:', contributor.url)
                   .replace(':src:', contributor.avatar);
               html += '</li>';
           });
           html += '</ul>';

           var container = document.querySelector('.contributors').parentNode.parentNode;
           container.innerHTML = html + container.innerHTML;
       }

       load(repositories.shift());
   })();
   </script>

.. _Contao Community Alliance: https://c-c-a.org
.. _Contao Association: https://association.contao.org/

.. _Nils Adermann: http://naderman.de/
.. _Jordi Boggiano: http://nelm.io/jordi
.. _Dominik Zogg: https://github.com/dominikzogg
.. _Tristan Lins: https://github.com/tristanlins
.. _Christian Schiffler: https://github.com/discordier
