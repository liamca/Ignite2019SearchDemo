# Content for Ignite 2019 Session BRK4003

## Index Schema for Phonetic Custom Analyzer Support

```
{
    "name": "hotels",
    "defaultScoringProfile": "",
    "fields": [
        {
            "name": "HotelID",
            "type": "Edm.String",
            "searchable": false,
            "filterable": false,
            "retrievable": true,
            "sortable": false,
            "facetable": false,
            "key": true,
            "indexAnalyzer": null,
            "searchAnalyzer": null,
            "analyzer": null,
            "synonymMaps": []
        },
        {
            "name": "HotelName",
            "type": "Edm.String",
            "searchable": true,
            "filterable": false,
            "retrievable": true,
            "sortable": false,
            "facetable": false,
            "key": false,
            "indexAnalyzer": null,
            "searchAnalyzer": null,
            "analyzer": "en.microsoft",
            "synonymMaps": []
        },
        {
            "name": "HotelNamePhonetic",
            "type": "Edm.String",
            "searchable": true,
            "filterable": false,
            "retrievable": true,
            "sortable": false,
            "facetable": false,
            "key": false,
            "indexAnalyzer": null,
            "searchAnalyzer": null,
            "analyzer": "my_phonetic",
            "synonymMaps": []
        },        
        {
            "name": "Description",
            "type": "Edm.String",
            "searchable": true,
            "filterable": false,
            "retrievable": true,
            "sortable": false,
            "facetable": false,
            "key": false,
            "indexAnalyzer": null,
            "searchAnalyzer": null,
            "analyzer": "en.microsoft",
            "synonymMaps": []
        },
        {
            "name": "Category",
            "type": "Edm.String",
            "searchable": false,
            "filterable": true,
            "retrievable": true,
            "sortable": false,
            "facetable": true,
            "key": false,
            "indexAnalyzer": null,
            "searchAnalyzer": null,
            "analyzer": null,
            "synonymMaps": []
        },
        {
            "name": "Rating",
            "type": "Edm.Double",
            "searchable": false,
            "filterable": true,
            "retrievable": true,
            "sortable": false,
            "facetable": false,
            "key": false,
            "indexAnalyzer": null,
            "searchAnalyzer": null,
            "analyzer": null,
            "synonymMaps": []
        },
        {
            "name": "StreetAddress",
            "type": "Edm.String",
            "searchable": false,
            "filterable": false,
            "retrievable": true,
            "sortable": false,
            "facetable": false,
            "key": false,
            "indexAnalyzer": null,
            "searchAnalyzer": null,
            "analyzer": null,
            "synonymMaps": []
        },
        {
            "name": "City",
            "type": "Edm.String",
            "searchable": false,
            "filterable": true,
            "retrievable": true,
            "sortable": false,
            "facetable": true,
            "key": false,
            "indexAnalyzer": null,
            "searchAnalyzer": null,
            "analyzer": null,
            "synonymMaps": []
        },
        {
            "name": "State",
            "type": "Edm.String",
            "searchable": false,
            "filterable": false,
            "retrievable": true,
            "sortable": false,
            "facetable": false,
            "key": false,
            "indexAnalyzer": null,
            "searchAnalyzer": null,
            "analyzer": null,
            "synonymMaps": []
        },
        {
            "name": "ZipCode",
            "type": "Edm.String",
            "searchable": false,
            "filterable": false,
            "retrievable": true,
            "sortable": false,
            "facetable": false,
            "key": false,
            "indexAnalyzer": null,
            "searchAnalyzer": null,
            "analyzer": null,
            "synonymMaps": []
        },
        {
            "name": "GeoLocation",
            "type": "Edm.GeographyPoint",
            "searchable": false,
            "filterable": true,
            "retrievable": true,
            "sortable": false,
            "facetable": false,
            "key": false,
            "indexAnalyzer": null,
            "searchAnalyzer": null,
            "analyzer": null,
            "synonymMaps": []
        },
        {
            "name": "ImageUrl",
            "type": "Edm.String",
            "searchable": false,
            "filterable": false,
            "retrievable": true,
            "sortable": false,
            "facetable": false,
            "key": false,
            "indexAnalyzer": null,
            "searchAnalyzer": null,
            "analyzer": null,
            "synonymMaps": []
        },
        {
            "name": "keyphrases",
            "type": "Collection(Edm.String)",
            "searchable": true,
            "filterable": true,
            "retrievable": true,
            "sortable": false,
            "facetable": true,
            "key": false,
            "indexAnalyzer": null,
            "searchAnalyzer": null,
            "analyzer": "standard.lucene",
            "synonymMaps": []
        },
        {
            "name": "translated_text",
            "type": "Edm.String",
            "searchable": true,
            "filterable": false,
            "retrievable": true,
            "sortable": false,
            "facetable": false,
            "key": false,
            "indexAnalyzer": null,
            "searchAnalyzer": null,
            "analyzer": "de.lucene",
            "synonymMaps": []
        }
    ],
    "scoringProfiles": [],
    "corsOptions": null,
    "suggesters": [
        {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields": [
                "HotelName"
            ]
        }
    ],
    "analyzers": [
        {"name":"my_phonetic","@odata.type":"#Microsoft.Azure.Search.CustomAnalyzer","tokenizer":"microsoft_language_tokenizer","tokenFilters": [ "lowercase", "asciifolding", "phonetic_token_filter" ]}
    ],
	"tokenFilters":[  
	{  
	  "name":"phonetic_token_filter",  
	  "@odata.type":"#Microsoft.Azure.Search.PhoneticTokenFilter",  
	  "encoder":"doubleMetaphone"
	}],
    "charFilters": []
}
  ```
## Analyze API Call
POST: https://liamca-ignite.search.windows.net/indexes/hotels/analyze?api-version=2019-05-06&search=kavanaugh
```
{
  "text": "Cavanagh",
  "analyzer": "my_phonetic"
}
```

RESPONSE:
```
{
    "@odata.context": "https://liamca-ignite.search.windows.net/$metadata#Microsoft.Azure.Search.V2019_05_06.AnalyzeResult",
    "tokens": [
        {
            "token": "KFNK",
            "startOffset": 0,
            "endOffset": 8,
            "position": 0
        }
    ]
}
```
