# lint-staged-issue

Reproduce by modifying a file and adding the change to git:
echo "test" >> README.md
git add README.md

Then run:
yarn lint-staged
