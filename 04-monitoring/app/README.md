環境為 Github Codespaces

## 主流程
- github codespaces 設定:
    - Machine type > 4-core 16GB RAM
- 啟動 service:
    ```shell
    docker-compose up
    # docker-compose down
    # docker-compose up postgres
    # docker-compose stop streamlit
    # docker-compose build streamlit
    # docker-compose start streamlit
    ```
- 連上 postgres 服務:
    - psql:
        - \l: 列出所有數據庫
        - \c <database_name>: 切換到指定數據庫
        - \conninfo: 顯示當前連接的數據庫信息
        - \dt: 列出所有表
    ```shell
    pgcli postgres://your_username:your_password@localhost/course_assistant
    ```
- 前置作業:
    - 創建 elasticsearch 索引
    - 創建 db table
    ```shell
    pip install -r requirements.txt
    POSTGRES_HOST=localhost python prep.py
    ```
- ollama pull model:
    ```shell
    docker exec -it ollama ollama pull phi3
    ```
- 使用 app 服務:
    - https://super-trout-wr994x5q5x4jf5g7w-8501.app.github.dev/
    - Ask: I just discovered the course. Can I still join?
- 製作模擬資料
    ```shell
    POSTGRES_HOST=localhost python generate_data.py
    ```
## Grafana:
- https://super-trout-wr994x5q5x4jf5g7w-3000.app.github.dev/login
    - 預設 email/password: admin
- 建立 data source
    - DATA SOURCES > PostgreSQL
    - Host URL: postgres
    - Database name: course_assistant
    - Username: your_username
    - Password: your_password
    - TLS/SSL Mode: disable
    - Save & test
- 建立 dashboard
    - Dashboard name: Course assistant
    - DASHBOARDS > Add visualization
- 同步 dashboard
    - DASHBOARDS  > Import dashboard > Upload dashboard JSON file
    - Share > Export > Save to file
    - Dashboard settings > Settings > JSON Model (複製下來納入 git 管理)
