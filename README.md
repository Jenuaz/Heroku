# Heroku
## Rails

```bash
rails new name-of-app --skip-active-record
```

**--skip-active-record** - this flag allow to skip configuration of database at this time.

Here we will generate rails controller which will print out message when we go to its index file.
```bash
cd name-of-app
rails g controller Welcome index
```
To provide changes to our index generated file:

```bash
vi app/view/welcome/index.html.erb
```

And manipulate the file as html file. Save it.
```vim
:wq
```
Our app ready to go to Heroku. But before deploy I will initialize my git repository:
```bash
git init
git add .
git commit -m "Rails app"
git push https://github.com/repository-name-here
```
Now I need to login to Heroku:


