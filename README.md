# Docker Magento Dev Env
## Dockerized Just Right Magento 2 development setup 
Built from [Mark Shust's configuration template](https://github.com/markshust/docker-magento)
    
Refer to Mark Shust's github page for more details on the predefined custom CLI commands he created to interact with the containerized services.

## Prerequisites
### Docker-Desktop resources
- CPUs: 4
- Memory: 8.00 GB
- Swap: 1 GB

## Setup Steps
1. Clone this project to your desired location
2. Inside the project, clone the Just Right platform to the <code>src/</code> folder.

    <code>git clone ssh://git@52.166.71.39:7999/npujr/purina-us-justright-platform.git src</code>
3. Navigate into <code>src/</code> and checkout the desired branch for the platform code.
4. Create the <code>src/app/code</code> and <code>src/app/design</code> folders if they do not exist.
5. Get the provided magento sql dump file and the master-data.sql file and save them in <code>db/</code>
6. <code> cp config/nginx.conf.sample src/</code>
7. <code>cp config/env.php.sample src/app/etc/env.php</code>
8. <code> bin/start </code> to start up the containers
9. <code>bin/copytocontainer --all</code>

    Note: for platform after the 11.5 release, there were changes that now involve a newly created <code>composer.patches.json</code> file that is required for the <code>bin/composer install</code> step.

    If this is the case, then you will need to copy that file over to the container with:
    >bin/copytocontainer composer.patches.json
10. <code>bin/clinotty mysql -hdatabase -umagento -pmagento magentodb < db/magento.sql</code> to seed the magento database
11. <code>bin/clinotty mysql -hdatabase -umagento -pmagento magentodb < db/master-data.sql</code>
12. <code>bin/composer install</code>
13. <code>bin/magento setup:upgrade</code>
14. <code>bin/magento app:config:import</code>
15. <code>bin/setup-domain justrightpetfood.local</code>
