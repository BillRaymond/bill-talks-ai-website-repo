## Create Hugo site, install and configure bootstrap
1. Create a new folder
2. Add a file and name it `Dockerfile`
3. In the Dockerfile, add `FROM billraymond/bill-talks-ai-docker-image`
4. Create a `.gitignore` file
5. In .gitignore, add `public/`
6. Run `git init` then `git commit` with the nane `initial commit`
7. Run `npm init -y`
8. Run `npm install bootstrap`
9. Run `hugo new site . --force` to create a new Hugo website
10. Run `hugo new theme bill-talks-ai` to create a new theme for the website
11. Rename the top-level `hugo.toml` to `hugo.yaml`
12. Edit the top-level `hugo.yaml` and modify the code from toml format to yaml format, filling in settings as needed, like this:
```
baseURL: 'https://bill-talks-ai.com/'
languageCode: 'en-us'
title: 'Bill Talks AI'
theme: 'bill-talks-ai'
```
13. Run `hugo` to verify the site builds without errors
14. edit the top-level `config.yaml` file, add the following lines of code toward the bottom:
```
