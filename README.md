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

rails_root = ENV[] || File.dirname() + ''
rails_env = ENV[] || ''
config_file = rails_root + ''
resque_config = YAML::load()
Resque.redis = resquee_config[]

Resque.inline = ENV[] == ""

Resque.redis.namespace = "resque:GithHub"
```

```
```
