# Adapted from Scott Kyle's Rakefile
# http://github.com/appden/appden.github.com/blob/master/Rakefile

def jekyll(opts = "", path = "$HOME/.rvm/gems/default/bin/")
  sh "rm -Rf /home/jdios/public_html/*"
  sh path + "jekyll " + opts
end
 
desc "Build site using Jekyll"
task :build do
  jekyll
end
 
desc "Serve at localhost:4000"
task :default do
  jekyll("--server --auto")
end

desc "Serve at localhost:4000 sans autogeneration"
task :hack do
  jekyll("--server")
end
 
desc "Deploy to dev"
task :deploy => :"deploy:dev"
 
namespace :deploy do
  desc "Deploy to dev"
  task :dev => :build do
    rsync "$HOME/Sites/jd-ios/"
  end
  
  desc "Deploy to live"
  task :live => :build do
    rsync "jdios:/home/jdios/public_html/"
  end
  
  desc "Deploy to dev and live"
  task :all => [:dev, :live]
  
  def rsync(location)
    sh "rsync -rtvz --exclude='.DS_Store' --delete _site/ #{location}"
  end
end
