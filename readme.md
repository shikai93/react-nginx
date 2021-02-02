# NGINX Deployment
Replace all {sub-directory} and {sub-directory-folder} with your relevant project specific values

## Pre-deployment
1. Change all of react router to have a basename of your intended subdirectory
2. Change homepage in package.json to have subdirectory
3. Change index.html to have a base href of your sub directory `<base href="/">`
4. npm run build to build application for production

## Deployment
1. Place build folder in html/{sub-directory-folder}
2. Change port configurations using ` listen       3000;`
3. Set Nginx config to have 
```
location /{sub-directory} {
    return 301 https://{domain}/{sub-director}/;
}
location ^~ /{sub-directory}/ {
    alias html/{sub-directory-folder}/build/;
    try_files $uri $uri/ /index.html;
}
```
4. Run `nginx.exe -p {path/to/nginx.exe}`
5. Run `nginx.exe -s stop` to shutdown nginx

## Install as windows service 
1. Run `nginxservice.exe nginxservice.xml` as Administrator
2. When restarting service, if it fails, run `taskkill /F /IM nginx.exe` to kill all instances of nginx running on the server