* Install magento-cloud CLI

  * curl -sS https://accounts.magento.cloud/cli/installer | php
  * export PATH=$PATH:$HOME/.magento-cloud/bin
  * . ~/.bash_profile
  
* log in
  * magento-cloud login

* Set Authentication keys
  *  ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
  *  magento-cloud ssh-key:add ~/.ssh/id_rsa.pub
  *  [document github](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=linux)
  * [document adobe](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/authentication-keys.html?lang=en#composer-auth-environment-variable)

* Clone the project
  * magento-cloud project:list  #check the project ID
  * magento-cloud project:get <project-ID> 
  * switch to the project file
  * magento-cloud environment:list  #you can see the existing branch
  * magento-cloud checkout <branch-ID>
 
* Dump integration 2 db
  * magento-cloud db:dump
 
* Create an auth.json file 
  * {
    "http-basic": {
        "repo.magento.com": {
            "username": "pubilc ID",
            "password": "private ID"
        },
        "packages.geissweb.de": {
            "username": "pubilc ID",
            "password": "private ID" } } }
* Run composer update
 
* Build docker file 
  * ./vendor/bin/ece-docker 'build:compose' --with-entrypoint --mode=developer --with-cron --sync-engine=mutagen --no-varnish --port=80 
     (developer:允許write data, mutagen:同步數據)
  * 檢查是否有 docker-compose.yml file
 
* 一次啟用所有docker container
  * docker compose up -d
 
* 將專案複製到container內
  * ./bin/magento-docker copy-to --all
* 進bash 
  * docker-compose run --rm deploy bash
* 設定資料庫user
  * bin/magento admin:user:create --admin-firstname={{FIRST_NAME}} --admin-lastname={{LAST_NAME}} --admin-email={{EMAIL}} --admin-user={{LOGIN_ACCOUNT}} --admin-password={{PASSWORD}}
* 匯入資料庫
  * mysql -h db.magento2.docker -u username -p database_name < file.sql
* Update docker setup:
  * ./bin/magento setup:upgrade
* compile code
  * ./bin/magento setup:di:compile
* Deploy static content:
  * ./bin/magento setup:static-content:deploy
  * ./bin/magento setup:static-content:deploy -f
* Update index:
  * ./bin/magento indexer:reindex
* Flush cache:
  * ./bin/magento cache:flush
* i18n collection:
  * ./bin/magento i18n:collect-phrases -o code_zyxel.csv app/code/Zyxel
  * ./bin/magento i18n:collect-phrases -o design_zyxel.csv app/design/frontend/Zyxel/default

* Apply Patches
  * ./vendor/bin/ece-patches apply
    
* Else
  * 查看container狀態
    * docker ps
  * 停下docker container
    * docker compose stop
  * 重啟docker container
    * docker compose start
  * 刪除docker container
    * docker compose rm
