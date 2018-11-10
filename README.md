### Resque
---
https://github.com/resque/resque

```ruby
class Archive
  @queue = :file_serve
  def self.perform(repo_id, branch = 'master')
    repo = Repository.find(repo_id)
    repo.create_archive(branch)
  end
end

class Repository
  def async_create_archive(branch)
    Resque.enqueue(Archive, self.id, branch)
  end
end

klass, args = Resque.reserve(:file_serve)
klass.perform(*args) if klass.respond_to? :perform

Archive.perform(44, 'masterbrew')

repo = Repository.find(44)
repo.async_create_archive('masterbrew')

{
  'class': 'Archive',
  'args': [ 44, 'masterbrew' ]
}

Resque.enqueue(Archive, self, branch)

Resque.enqueue(Archive, self.id, branch)

require ''
require ''
require ''
Resque::Failure::Multiple.classes = [Resque::Failure::Redis, Resque::Failure::Airbrake]
Resque::Failure.backend = Resque::Failure::Multiple

start
loop do
  if job = reserve
    job.process
  else
    sleep 5
  end
end
shutdown

task "resque:setup" => :environment

task "resque:setup" => :environment do
  Grit::Git.git_timeout = 10.minutes
end

# config/initalizers/resque.rb
Resque.logger.level = Logger::DEBUG

# config/initalizers/resque.rb
Resque.logger = Logger.new(Rails.root.join('log', "#{Rails.env}_resque.log"))

# config/initalizers/resque.rb
class NullDataStore
  def stat(stat)
    0
  end
  def increment_stat(stat, by)
  end
  def decrement_stat(stat, by)
  end
  def clear_stat(stat)
  end
end
Resque.stat_data_store = NullDataStore.new


class MyTask
  def self.perform
    ActiveRecord::Base.verify_active_connections!
  end
end

class MyTask
  def self.perform
    ActiveRecord::Base.clear_active_connections!
  end
end

require 'resque/server'
run Rack::URLMap.new \
  "/" => Your::App.new,
  "/resque" => Resque::Server.new
  
mount Resque::Server.new, :at => "/resque"

require 'resque'

require 'your/app'
require 'rescue/tasks'

require 'resque/tasks'
task 'resque:setup' => :environment

require 'resque/tasks'

require 'resque/tasks'

rails_root = ENV['RAILS_ROOT'] || File.dirname(__FILE__) + '/../..'
rails_env = ENV['RAILS_ENV'] || 'development'
config_file = rails_root + '/config/resque.yml'
resque_config = YAML::load(ERB.new(IO.read(config_file)).result)
Resque.redis = resquee_config[rails_env]

Resque.inline = ENV['RAILS_ENV'] == "cucumber"

Resque.redis.namespace = "resque:GithHub"
```

```
cd app_root
QUEUE=file_serve rake resque:work

QUEUE=file_serve rake resque:work
QUEUE=file_serve rake environment resque:work

PIDFILE=./resque.pid QUEUE=file_serve rake environment resque:work

PIDFILE=./resque.pid BACKGROUND=yes QUEUE=file_serve \
  rake environment resque:work
  
INTERVAL=0.1 QUEUE=file_serve rake environment resque:work

QUEUES=file_serve,warm_cache rake resque:work

QUEUES=critical,archive,high,low rake resque:work

QUEUE=archive rake resque:work

QUEUE=* rake resque:work

COUNT=5 QUEUE=* rake resque:workers

ps -e -o pid,command | grep [r]esque
ps -e -o pid, command | grep [r]esque

resque-web
resque-web -p 8282
resque-web -p 8282 rails_root/config/initalizers/resque.rb
resque-web -p 8282 -N myapp
resque-web -p 8282 -r localhost:6379:2

gem install bundler
bundle install
gem install resque
rakeup config.ru

QUEUE=* rake resque:work

gem install resque

cat config/initializers/load_resque.rb

./script/server

QUEUE=* rake environment resque:work

./script/plugin install git://github.com/resque/resque

QUEUE=* rake environment resque:work
cat Gemfile
bundle install
rails server
QUEUE=* rake environment resque:work
RAILS_ENV=production resque-web rails-web rails_root/config/initializers/resque.rb

git clone git://github.com/resque/resque.git
cd resque
rake test

irb
require 'rubygems'
require 'redis/namespace'
```

```
// config/resque.yml
development: localhost:6379
test: localhost:6379
staging: redis1.se.github.com:6379
fi: localhost:6379
production: <%= ENV['REDIS_URL'] %>
```
