# opensea-bot

## 目標

1. 當有人掛賣的 NFT 比地板價低很多的時候，自動把它買下來

## OpenSea API 申请秘诀

Opensea 审核很松，申请中需要填写项目网址信息，其实填什么都可以，twitter，FB group 或者是 IG，只要 follower 数多就能通过。（大家可以找一些知名的账号，自圆其说即可）

## 参数设定

1. 複製 `.env.example` 至 `.env`，設定必要的變數：

   - `OPENSEA_API_KEY`: Opensea 提供的 API Key，需自行申請
   - `CONTRACT_ADDRESS`: 要監聽的合約地址
   - `COLLECTION_ID`: 監聽的合約地址在 Opensea 上對應的 ID，可在 collection 頁面的網址列找到
   - `INFURA_PROJECT_ID`: Infura 提供的 key，需自行申請
   - `PRIVATE_KEY_HEX`: 錢包私鑰，格式為不帶 `0x` 開頭的 hex （如 `1234...`）
   - `WALLET_ADDRESS`: 錢包的地址（如 `0xabcd...`）
   - `GAS_PRICE`: 要設多少 max gas price 去搶低價 NFT
   - `FLOOR_UNDERPRICED_RATIO`: 低於地板價的幾倍時自動買入（如 `0.2`）
   - `FLOOR_UNDERPRICED_VALUE`: 低於多少 ETH 時自動買入（如 `3`）

2. 若要同時監聽多組 collection，需在以下四個變數設置多個值，並以 `|` 符號隔開

   - `COLLECTION_ID`
   - `CONTRACT_ADDRESS`
   - `FLOOR_UNDERPRICED_RATIO`
   - `FLOOR_UNDERPRICED_VALUE`

     範例：

     ```bash
     CONTRACT_ADDRESS=0x60e4d786628fea6478f785a6d7e704777c86a7c6|0x67d9417c9c3c250f61a83c7e8658dac487b56b09|0x49cf6f5d44e70224e2e23fdcdd2c053f30ada28b
     COLLECTION_ID=mutant-ape-yacht-club|phantabear|clonex
     FLOOR_UNDERPRICED_RATIO=0.2|0.4|0
     FLOOR_UNDERPRICED_VALUE=0|0|1
     ```
     
#### 注意事项

- 每一个OpenSea API 最多支持监听6个项目
- FLOOR_UNDERPRICED_RATIO 与 FLOOR_UNDERPRICED_VALUE 请选择其中一个作为监听标准。 FLOOR_UNDERPRICED_RATIO 可以根据设定的比例自动调整，而FLOOR_UNDERPRICED_VALUE 则会按照固定的价格进行买入
- FLOOR_UNDERPRICED_RATIO 与 FLOOR_UNDERPRICED_VALUE 如果一个被作为监听标准，请输入具体的数字，另一个请设置为0 来取消对这个条件的监听。

## 使用步驟

1. 下載最新版程式碼 (`.zip`)，並解壓縮，得到 `opensea-bot` 資料夾
2. 使用 VS Code 開啟 `opensea-bot` 資料夾
3. 在 `opensea-bot` 資料夾下複製檔案 `.env.example` 至 `.env`
4. 在 `.env` 中按照前述方式設定各個參數
5. 请先安装 nodejs 前往 https://nodejs.org/en/download/
6. 下载 yarn，前往查看 https://classic.yarnpkg.com/en/docs/install
   ```
   npm install --global yarn
   ```
8. 安装typescript 前往查看 https://www.typescriptlang.org/download 
   ```
   npm install -g typescript
   ```
9. 安裝套件： `yarn install`
10. 編譯並執行： `tsc && node dist/index.js`(Mac)  `tsc ; node dist/index.js`(Windows) 

## 开发新功能
1. 修改時自動編譯： `tsc -w`
2. 編譯並執行： `tsc && node dist/index.js`(Mac)  `tsc ; node dist/index.js`(Windows) 
