

create a new repository in bitbucket

mkdir <new-projec>-bdds-tests

cd <new-projec>-bdds-tests

git clone git@bitbucket.org:printerlogicDev/template-bdds-tests.git .

git remote set-url origin git@bitbucket.org:printerlogicDev/<new-projec>-bdd-tests.git

npm run setup

npm run local-test