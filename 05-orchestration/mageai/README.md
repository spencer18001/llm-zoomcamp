#### Module overview
- Overview > New pipeline > Retrieval Argumented Generation
- Pipelines > 右鍵點 pipeline > Open pipeline

#### Ingest
- Data preparation > Load > Ingest > Add block > API Data Loader
	- Endpoint URL: https://raw.githubusercontent.com/DataTalksClub/llm-zoomcamp/main/01-intro/documents.json
	- Run、Edit

#### Chunk
- Transform > Chunking > Add block > Custom Code > Edit
	- 貼上 05-orchestration/mageai/llm/rager/transformers/radiant_photon.py 的程式碼
	- Run

#### Tokenization
- Transform > Tokenization > Add block > Lemmatization (spaCy) > Edit
	- 貼上 05-orchestration/mageai/llm/rager/transformers/vivid_nexus.py 的程式碼 (印出 progress)
	- Run
```shell
pip install spacy
python -m spacy download en_core_web_sm
```

#### Embed
- Transform > Embed > Add block > spaCy embeddings
	- 貼上 05-orchestration/mageai/llm/rager/transformers/prismatic_axiom.py 的程式碼 (印出 progress)
	- Run

#### Export
- Export > Vector database > Add block > Elasticsearch
	- Connection string: http://elasticsearch:9200
	- Edit
	- 貼上 05-orchestration/mageai/llm/rager/data_exporters/numinous_fission.py 的程式碼 (印出 progress)
	- Run

#### Retrieval
- Inference > Retrieval > Iterative retrieval > Add block > Elasticsearch
	- 使用 hard coding sample embedding 來查詢

#### Trigger
- Pipelines > 點擊 pipeline > New trigger
	- Trigger type: Schedule
	- Trigger name: Daily document refresh
	- Frequency: daily
	- timeout: 3600
	- status: failed
	- 勾選 Skip run if previous run still in progress
	- 勾選 Create initial pipeline run if start date is before current execution period
	- Start date and time: 設定成昨天
	- Save changes > Enable trigger
