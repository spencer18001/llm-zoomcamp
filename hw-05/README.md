uses Github Codespaces

- github codespaces setting:
    - Machine type > 4-core 16GB RAM

- edit llm/requirements.txt
```
python-docx
elasticsearch
```

- edit docker-compose.yml
```
elasticsearch:
  deploy:
    resources:
      limits:
        memory: 4G
```
- start mageai
  ```
  chmod +x scripts/start.sh
  ./scripts/start.sh
  ```
  - :6789 open mageai web 介面
  - Q1: v0.9.72

- Overview > New pipeline > Retrieval Argumented Generation
  - Edit pipeline

- Ingestion:
  - Custom > Python block
  - Variables: `file_id` "1qZjwHkvP0lXHiE4zdbWyUXSVfmVGzougDD6N37bat3E"
  - Q2: 1

- Chunking:
  - Custom > Python block
  - Q3: 86

- Tokenization:

- Export:
  - All blocks > Data exporter > Export > Vector database -> Elasticsearch
  ```
  connection_string = kwargs.get('connection_string', 'http://elasticsearch:9200')
  ```
  - Q4: 'fa136280'

- Retrieval:
  - Custom > Python block
  - Q5: bf024675
  ```
  from elasticsearch import Elasticsearch

  def search_elastic(client, index_name, query):
      search_query = {
          "size": 1,
          "query": {
              "bool": {
                  "must": {
                      "multi_match": {
                          "query": query,
                          "fields": ["question", "text", "section"],
                          "type": "best_fields"
                      }
                  }
              }
          }
      }
      response = client.search(index=index_name, body=search_query)

      result_docs = []
      for hit in response['hits']['hits']:
          result_docs.append(hit['_source'])
      return result_docs

  @custom
  def transform_custom(*args, **kwargs):
      connection_string = kwargs.get('connection_string', 'http://elasticsearch:9200')
      index_name = kwargs['index_name']

      es_client = Elasticsearch(connection_string)

      results = search_elastic(es_client, index_name, 'When is the next cohort?')
      return results
  ```
- Reindexing:
  - Variables: `file_id` "1T3MdwUvqCL3jrh3d3VCXQ8xE0UqRzI3bfgpfBq3ZWG0"
  - Q6: b6fa77f3