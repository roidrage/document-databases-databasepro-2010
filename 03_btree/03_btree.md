!SLIDE

## ”CouchDB is just a B-Tree and a Transformation Engine.“ ##

<p class="caption">
<a href="http://twitter.com/bitdiddle/status/19645939355">Anonymous Tweeter</a>
</p>

!SLIDE center

# Der B-Tree #

![B-Tree](btree.png)

!SLIDE

## Alle Daten werden in einem B-Tree gespeichert. ##

!SLIDE

## Daten werden immer nur angehängt, ##
## niemals aktualisiert. ##

!SLIDE

## Wie kann ich meine Daten abfragen? ##

!SLIDE bullets incremental

* Queries werden als Views gespeichert
* Views werden in JavaScript geschrieben
* Views sind Teil von Design-Dokumenten

!SLIDE bullets incremental

# Views #

* Sind ein B-Tree
* Mapping von Key auf ein Document oder Value

!SLIDE bullets incremental

# Views - Keys #

* Keys können beliebige Objekte sein

!SLIDE

## Views - Keys ##

    "Why Riak Search Matters..."

    ["riak", "full text search"]

    {title: "Why Riak...", published_at: ".."}

!SLIDE

# Views - Values #

* Meistens `null`
* Beliebige JSON Objekte
* Werden im View gespeichert

!SLIDE

# Views #


!SLIDE bullets incremental

# Map/Reduce #

* Map emits the desired lookup keys
* Reduce aggregates the results

!SLIDE 

# Map Phase #

## Find by Name ##

    function(doc) {
      emit(doc.name, doc);
    }

!SLIDE javascript

## Find by tag ##

    function(doc) {
      for (var index in doc.tags) {
        emit(doc.tags[index], 1);
      }
    }

!SLIDE javascript small

## Find by tag ##

    function(keys, values, rereduce) {
      var sum = 0;
      for (var i = 0; i < values.length; i++) {
         sum += values[i];
      }
      return sum;
    }

!SLIDE smaller

## Querying Views ##

    /jaoo/_design/conferences/_view/by_name?key="JAOO 2010"

!SLIDE bullets incremental

# Design Documents #

* Collect map/reduce functions
* Name convention: `_design/<document>`
* Regular JSON document

!SLIDE javascript small

# Design Documents #

    {
      "_id": "_design/conferences"
      "views": {
        "by_name": {
          "map": "function(doc)...",
          "reduce": "function(keys, values, rereduce)"
        }
      }
    }

!SLIDE bullets incremental

# Views #

* Are only updated on read
* Are always read from disk
* Are invalidated when design documents are updated
