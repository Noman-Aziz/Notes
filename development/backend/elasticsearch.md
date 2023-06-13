# ElasticSearch

### Basic Queries <a href="#basic-queries" id="basic-queries"></a>

#### `GET _cat/indices` <a href="#get-_catindices" id="get-_catindices"></a>

* Returns all the indices we have

#### `GET <indice_name>/_search` <a href="#get-indice_name_search" id="get-indice_name_search"></a>

* Searches all the documents on the specified index

#### `GET <indice_name>/_doc/<doc_id>` <a href="#get-indice_name_docdoc_id" id="get-indice_name_docdoc_id"></a>

* Get the specified document

***

### Basic Fields <a href="#basic-fields" id="basic-fields"></a>

#### `_source` <a href="#_source" id="_source"></a>

* Specifies what field do you want to return

#### `size` <a href="#size" id="size"></a>

* How many documents do you want to return, can not be greater than `10000`

#### `min_score` <a href="#min_score" id="min_score"></a>

* Whenever we write a query, elasticsearch gives it a score by default, you can filter the min score

***

### Query Hierarchy <a href="#query-hierarchy" id="query-hierarchy"></a>

#### Level 1 <a href="#level-1" id="level-1"></a>

* `query`

#### Level 2 <a href="#level-2" id="level-2"></a>

* `bool`

#### Level 3 <a href="#level-3" id="level-3"></a>

* `must`
  * Stands for AND operator
* `filter`
  * Used for filtering
* `should`
  * Stands for OR operator
* `must_not`
  * Stands for NOT operator

#### Level 4 <a href="#level-4" id="level-4"></a>

* `match`
  * Used for partial matching like `elk search` will return all texts which have `elk` or `search` in them
* `match_phrase`
  * Used for exact matching like `elk search` will return all texts which have `elk search` in them

***

### Nested Boolean Operators <a href="#nested-boolean-operators" id="nested-boolean-operators"></a>

* Sometimes, we need queries like `TITLE IS ( A OR B ) NOT ( C OR D )`

```json
GET learn/_search
{
    "_source": [
        "title"
    ],
    "size": 10,
    "min_score": 0.5,
    "query": {
        "bool": {
            "should": [
                {
                    "match": {
                        "title": "King"
                    }
                },
                {
                    "match": {
                        "title": "Nazi"
                    }
                }
            ],
            "must_not": [
                {
                    "bool": {
                        "should": [
                            {
                                "match": {
                                    "title": "Peking"
                                }
                            },
                            {
                                "match": {
                                    "title": "jack"
                                }
                            }
                        ]
                    }
                }
            ]
        }
    }
}
```

***

### Pagination Methods <a href="#pagination-methods" id="pagination-methods"></a>

[https://opster.com/guides/elasticsearch/how-tos/elasticsearch-pagination-techniques/](https://opster.com/guides/elasticsearch/how-tos/elasticsearch-pagination-techniques/)

#### When to use pagination? <a href="#when-to-use-pagination" id="when-to-use-pagination"></a>

* When you need free access to pages and you’re not planning to offer deep pagination.

#### When to use Search-After? <a href="#when-to-use-search-after" id="when-to-use-search-after"></a>

* When a “next” button is suited for you and you want to give efficient access to many pages.

#### When to use the Point in Time API? <a href="#when-to-use-the-point-in-time-api" id="when-to-use-the-point-in-time-api"></a>

* When you need consistent order across search result pages.
* When you’re running Elasticsearch with X-Pack >7.10 or >7.13.

#### When to use Scroll? <a href="#when-to-use-scroll" id="when-to-use-scroll"></a>

* Scroll can be used to list all hits to a query. However it should be a rare request, probably alright in expert applications or for very rare end-user requests.
* When you need consistent order across search result pages.
* When your Elasticsearch version does not support Point in Time.

***

### ElasticSearch Query Generator <a href="#elasticsearch-query-generator" id="elasticsearch-query-generator"></a>

* Python library used to assist generation of elastic search queries
* [https://pypi.org/project/elasticsearchquerygenerator/](https://pypi.org/project/elasticsearchquerygenerator/)

***

### Aliases <a href="#aliases" id="aliases"></a>

* We can create an alias of document which can contain subset of that document

***
