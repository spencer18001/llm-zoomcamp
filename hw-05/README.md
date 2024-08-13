環境為 Github Codespaces

- github codespaces 設定:
    - Machine type > 4-core 16GB RAM

- 編輯 llm/requirements.txt
```
python-docx
elasticsearch
```

- 編輯 docker-compose.yml
```
elasticsearch:
  deploy:
    resources:
      limits:
        memory: 4G
```
