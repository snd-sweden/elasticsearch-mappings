# elasticsearch-mappings
Elastic Search mappings for SND:s metadata

## To set up indexes

``curl -XPUT 'http://localhost:9200/sndcatalogue-en' -d @sndcatalogue-en.json``

``curl -XPUT 'http://localhost:9200/sndcatalogue-sv' -d @sndcatalogue-sv.json``

## Insert example

``curl -XPUT 'http://localhost:9200/sndcatalogue-sv/study/SND0001' -d @SND0001.json``
