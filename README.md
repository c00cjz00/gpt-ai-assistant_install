### 1. 下載執行程式
```
git clone https://github.com/c00cjz00/gpt-ai-assistant_install.git
```

### 2. 取得 Webhook URL
```
%%bash
node_ip=$(cat /etc/hosts |grep $(hostname).nchc.opa | awk '{print $1}' ); 
node_port=$(cat ~/gpt/env.txt |grep APP_PORT | awk -F '=' '{print $(2)}');
echo "Webhook URL: https://node02.biobank.org.tw/redirect/${node_ip}/${node_port}/webhook"
```

### 3. 請編輯 env-template.txt 更新以下三個項目
- OPENAI_API_KEY=請填寫 (申請位置: https://beta.openai.com/)
- LINE_CHANNEL_ACCESS_TOKEN=請填寫  (申請位置: https://developers.line.biz/)
- LINE_CHANNEL_SECRET=請填寫  (申請位置: https://developers.line.biz/)

### 4. 安裝及啟動
```
%%bash
## 安裝位置 (填寫你目前git clone下來的位置)
install_dir=~/gpt-ai-assistant_install

## 參數設定
file_url=https://github.com/memochou1993/gpt-ai-assistant/archive/refs/tags/4.4.3.tar.gz
file_basename=$(basename ${file_url})

## 安裝套件
cd ${install_dir}
wget -q ${file_url} -O ${file_basename}
extract_folder=$(tar -xzvf ${file_basename} |head -n 1)
rm -rf ${extract_folder}
tar -xzf ${file_basename}
rm ${file_basename}
cp env-template.txt ${extract_folder}/.env
cd ${install_dir}/${extract_folder}
npm ci --only=production

##啟動程式 (若需要觀看互動過程, 請將註解 #npm start, 並將最下方的指令貼在下一個cell執行)
echo "!cd ${install_dir}/${extract_folder} ; npm start"
npm start
```
