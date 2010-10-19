!SLIDE

# CouchDB Zucker #

!SLIDE

# CouchApps #

!SLIDE bullets incremental

* Web-Applikationen
* Komplett in JavaScript
* Direkt aus der Datenbank geliefert

!SLIDE bullets incremental

# CouchDB ist #

* Datenbank
* Web-Server
* Application-Server

!SLIDE bullets incremental

# Was gibt es nicht? #

* Transaktionen
* Update immer nur von einzelnen Dokumenten
* Updates sind ACID

!SLIDE bullets incremental

# Was gibt es nicht? #

* Joins
* Immer nur ein Dokument ist relevant in einer Abfrage
* Oder mehrere bei Views

!SLIDE javascript

## Views können "verlinkte" Dokumente ausgeben ##

    @@@ javascript
    function(doc) {
      emit(doc.title, {'_id': doc.author_id})
    }

!SLIDE bullets incremental

# Was gibt es nicht? #

* Relationale Integrität
* Dokumente kennen keine anderen Dokumente
* Verlinkungen sind lose

!SLIDE bullets incremental

## Problem? ##

!SLIDE bullets incremental

## It Depends™ ##

!SLIDE bullets incremental

## Problematisch ##

* Viele Updates und viele Reads von Views
* Disk-I/O ist der wahre Bottleneck

!SLIDE bullets incremental

## Worauf achten? ##

* Regelmäßige Compaction notwendig
