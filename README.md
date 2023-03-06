# A simple chatbot using the gpt-3.5-turbo model deployed with Dokku

very simple: PHP | CSS | html | Javascript

based on 
(1) https://github.com/rueetschli/OpenAI-GPT-3.5-turbo-simple-script which was forked from 
(2) https://github.com/dirk1983/chatgpt 

Source (1) was translated to English and an input field was added to query for OpenAI API Key instead of saving key in script on server. Added empty composer.json for deployment with dokku.

All files needed for deployment and running the chatbot are contained in this repository. Instead of deployment with dokku all files can also be copied to (protected) web directory.

To run use the chatbot: Register at https://platform.openai.com/ for an API key.

# Deployment with Dokku

example: deploy wordpress blog for **example.com** with the app name **chat** yielding **chat.example.com**

### create folder for deployment

`mkdir chatbot`  
`cd chatbot`

### create app named **blog**
`dokku apps:create chat`  

### Initialize repository and make initial commit 

`git init` \
`git add .` \
`git commit -m "initial commit"`
`git remote add dokku dokku@hostname.tld:blog` #hostname = your servers hostname, where you host **example.com**   
`git push dokku master`


### install and enable letsencrypt plugin to get ssl certificate

`sudo dokku plugin:install https://github.com/dokku/dokku-letsencrypt.git` #install letsencript plugin 
`dokku config:set --global DOKKU_LETSENCRYPT_EMAIL=your@email.tld` #define email ... only once 
`dokku letsencrypt:enable chat`
`dokku letsencrypt:auto-renew` #activate auto-renewal of ssl certs
`dokku letsencrypt:cron-job --add` #setup cronjob to do auto renewal 

## website to be reached via **chat.example.com** served via https