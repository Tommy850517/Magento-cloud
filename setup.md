* Install magento-cloud CLI

  * curl -sS https://accounts.magento.cloud/cli/installer | php
  * export PATH=$PATH:$HOME/.magento-cloud/bin
  * . ~/.bash_profile
  
* log in
  * magento-cloud

* Set Authentication keys 
  * [document](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/authentication-keys.html?lang=en#composer-auth-environment-variable)

* Clone the project
  * magento-cloud project:list  #check the project ID
  * magento-cloud project:get <project-ID> 
  * switch to the project file
  * magento-cloud environment:list  #you can see the existing branch
  * magento-cloud checkout <branch-ID>
 
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
  * ./vendor/bin/ece-docker build:compose --mode="developer" --sync-engine="mutagen" (developer:允許write data, mutagen:同步數據)
  * 檢查是否有 docker-compose.yml file
 
* 一次啟用所有docker container
  * docker compose up -d
* 查看container狀態
  * docker ps
* 停下docker container
  * docker compose down
* 重啟docker container
  * docker compose start
* 刪除docker container
  * docker compose rm
