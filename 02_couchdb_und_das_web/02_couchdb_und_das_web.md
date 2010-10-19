!SLIDE center

![CouchDB](couchdb-logo.png)

!SLIDE

## ”CouchDB is built of the Web“ ##
<p class="caption">
<a href="http://jacobian.org/writing/of-the-web/">Jacob Kaplan-Moss</a>
</p>

!SLIDE bullets incremental

# CouchDB und das Web #

* Spricht HTTP
* JSON als Datentransport
* RESTful API

!SLIDE code smaller

# Alles spricht HTTP #

    GET /powerdays

    HTTP/1.1 404 Object Not Found
    Server: CouchDB/1.0.0 (Erlang OTP/R13B)
    Date: Sun, 03 Oct 2010 18:26:03 GMT
    Content-Type: text/plain;charset=utf-8
    Content-Length: 44
    Cache-Control: must-revalidate
     
    {"error":"not_found","reason":"no_db_file"}

!SLIDE code smaller

# Alles spricht HTTP #

    PUT /powerdays

    HTTP/1.1 201 Created
    Server: CouchDB/1.0.0 (Erlang OTP/R13B)
    Location: http://localhost:5984/powerdays
    Date: Sun, 03 Oct 2010 18:27:14 GMT
    Content-Type: text/plain;charset=utf-8
    Content-Length: 12
    Cache-Control: must-revalidate
     
    {"ok":true}

!SLIDE code smaller

# Alles spricht HTTP #

    GET /powerdays

    HTTP/1.1 200 OK
    ...

    {"db_name":"powerdays","doc_count":0,"doc_del_count":0,
    "update_seq":0,"purge_seq":0,"compact_running":false,
    "disk_size":79,"instance_start_time":"1286130434654709",
    "disk_format_version":5}

!SLIDE code smaller

# Alles ist eine Ressource #

    PUT /powerdays/eb28b751a33d1bf9d7dfffd6700006d5

    HTTP/1.1 201 Created
    Server: CouchDB/1.0.0 (Erlang OTP/R13B)
    Location: http://localhost:5984/powerdays/eb28b...
    Etag: "1-6f773089b853fd5f7867562b179a854a"
    Date: Sun, 03 Oct 2010 19:32:38 GMT
    Content-Type: text/plain;charset=utf-8
    Content-Length: 67
    Cache-Control: must-revalidate

    {"ok":true,"id":"eb28b751a33d1bf9d7dfffd6700006d5",
    "rev":"1-6f773089b853fd5f7867562b179a854a"}
    
!SLIDE code small

    {
      "_id": "eb28b751a33d1bf9d7dfffd6700006d5",
      "_rev": "1-6f773089b853fd5f7867562b179a854a",
      "title": "Why Riak Search Matters...",
      "published_at": "2010/10/08 17:00:00 +0000",
      "tags": ["riak", "full text search"]
    }

!SLIDE

## Dokumente haben Attachments ##

!SLIDE code small

    {
      "_id": "eb28b751a33d1bf9d7dfffd6700006d5",
      ...
      "_attachments": {
        "logo.gif": {
          "content_type": "image/gif",
          "revpos": 3,
          "length": 1929,
          "stub": true
        }
      }
    }

!SLIDE small

## Attachments sind Ressourcen ##

!SLIDE code smaller

    GET /powerdays/eb28b751a33d1bf9d7dfffd6700006d5/logo.gif
