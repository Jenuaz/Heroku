# Heroku
## Rails


# Prerequisites:
Version of your rails need to be 6.x.x.x. To check it write: **rails -v**
My -v's:
- ruby 2.7.1p83 (2020-03-31 revision a0c7c23c9c) [x86_64-linux-gnu]
- Rails 6.0.3.2
- bundle version 2.1.4
- yarn 1.22.4

```bash
rails -v
ruby -v
bundle version
gem list bundler
```

If your version less update it by commands:
```bash
curl -o- -L https://yarnpkg.com/install.sh | bash
apt-get upgrade ruby
gem install rails --no-document
gem install bundler:2.1.4
```
Bundler need to be brnad new :).

```bash
rails new app-name --skip-active-record
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
Our app ready to go to Heroku. But before deploy I will initialize my git repository. Inside
root repository of your project:
```bash
git init
git add .
git commit -m "Rails app"
```
Now I need to login in to Heroku platform. But before login we need to install our heroku.
I use Linux iOS so in terminal I write the next command to install heroku:
```bash
curl https://cli-assets.heroku.com/install.sh | sh
```
Finally we can LogIn in to our heroku:
```bash
heroku login
```

After successfuly Login we can create a new heroku application by writing command:
```bash
heroku create
```
This command setup a new domain name: https://git.heroku.com/new-domain-name
It it also initialize a git repository that I'll push to, which will eventually
deploy this application onto heroku. To make sure that heroku create command
added the Heroku upstream to my git repository files I will use this command
to list that:
```bash
git config --list | grep heroku
```
And I have my heroku pieces there. Now I will deploy application simply
pushing it to heroku.
```bash
git push heroku master
```

Application is deployed and available at https://domain.herokuapp.com/

Note:
If you see error like: Failed to install gems via Bundler.
It easy fixed by:
Running:
**bundle update** locally, fixes the issue. Locally run it's mean in your project folder.
if it's not helped try:
```bash
bundle update nokogiri
```

# Hot fixes
Facing this issue while installing bundler 2.1.4 but the system shows both 2.1.2 and 2.1.4 as default bundler gems.

Running this seems to have strange behaviour on the installed bundler version:

# gem install bundler -v 2.1.4 --default
Successfully installed bundler-2.1.4 as a default gem
# /path/to/ruby/gems/bundler-2.1.4/exe/bundle -v
Bundler version 2.1.2  <== but not bundler 2.1.4

Fixed the issue by following this to remove the default spec of bundler and gem install bundler -v 2.1.4 again without the default flag

rubygems/rubygems#2157

```bash
 rm /path/to/ruby/gems/specifications/default/rails-2.1.2.gemspec
 gem uninstall bundler -v 2.1.2
 gem install bundler -v 2.1.4
```

P.S. /path/to/ruby-gems can be found by running gem env

! You can check routes in congif/routes.rb

# Test controller which was described above works?
If all work properly. We will build our rails API app. Which catch JSON from Riverbrain and 
return it to our https://....heroku.../api/v1/rivers. First step is lets delete our welcome
controller:
```bash
rails destroy controller Welcome
```
Also it's greate to delete data about routes:
```bash
vi config/routes.rb
```
and delete raw with route.
Now we need to create new controller:
```bash
rails g controller Rivers
```
Go to config/routes.rb and replace standard get route related to our RiversController:
```bash
get 'api/v1/rivers', to: "rivers#index"
```
Also we need to change our RiversController add this raws:
```ruby
render json: RestClient.get("http://brainriver.com/api/v1/rivers", {})
```
Also extend Gemfile with(this gem allow to use Rest Client):

```bash
#vendor/routes
gem 'rest-client'
```


# Gemfile 
Gemfile is kind of file where all dependencies that this app uses and very bottom 
we add ruby 'version' and it help heroku to understand what verion of ruby do we 
use. Also we add there gem 'rest-client' to be able use API RestClient class in our
app.
