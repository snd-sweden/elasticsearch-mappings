# elasticsearch-mappings
Elastic Search mappings for SND:s metadata

## To set up indexes

``curl -XPUT 'http://localhost:9200/sndcatalogue-en' -d @sndcatalogue-en.json``

``curl -XPUT 'http://localhost:9200/sndcatalogue-sv' -d @sndcatalogue-sv.json``

## Insert example

``curl -XPUT 'http://localhost:9200/sndcatalogue-sv/study/SND0001' -d @SND0001.json``

## Search the documents

### Aggregatons and filters
```
curl -XPOST "http://localhost:9200/sndcatalogue-sv/study/_search" -d'
{
   "query": {
      "filtered": {
         "query": {
            "match_all": {}
         },
         "filter": {
            "bool": {
               "must": [
                  {
                     "term": {
                        "subject.value.raw": "massmedia"
                     }
                  },
                  {
                     "term": {
                        "subject.value.raw": "inrikespolitiska frågor"
                     }
                  }
               ]
            }
         }
      }
   },
   "aggregations": {
      "kindofdata": {
         "terms": {
            "field": "kindofdata.value.raw"
         }
      },
      "keyword": {
         "nested": {
            "path": "keyword"
         },
         "aggs": {
            "keyword": {
               "terms": {
                  "field": "keyword.value.raw"
               }
            }
         }
      },
      "subject": {
         "nested": {
            "path": "subject"
         },
         "aggs": {
            "subject": {
               "terms": {
                  "field": "subject.value.raw"
               }
            }
         }
      },
      "availabilitystatus": {
         "terms": {
            "field": "availabilitystatus.value.raw"
         }
      },
      "universe": {
         "terms": {
            "field": "universe.value.raw"
         }
      }      
   }
}'
```
