



mkdir <new-projec>-bdds-tests

cd <new-projec>-bdds-tests

git clone git@bitbucket.org:printerlogicDev/template-bdds-tests.git .

git remote set-url origin git@bitbucket.org:printerlogicDev/<new-projec>-bdd-tests.git

npm run sync

open pl-saas-web-bdd-steps folder and update the url of .gitmodules file to git@bitbucket.org:printerlogicDev/pl-saas-web-fi.git

npm run sync2

npm run sync3

npm run local-test