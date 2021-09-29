cf html5-list (list all apps in the repo)\
cf a (list applications)\
cf services (list services)\
cf undeploy sap-btp-sapui5 --delete-services --delete-service-keys\
cf html5-push -n html5_repo_host . (deploy to HTML5 repo)\
cf open appname (open application)\
cf html5-delete --content -n html5_repo_host (delete content)\

npm run build\
cf deploy ./\
cf deploy mta_archives/approuter_html5_1.0.0.mtar\

cf mtas (get mta ID)\
cf undeploy (mta ID) --delete-services --delete-service-keys\
