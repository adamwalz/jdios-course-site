# Adapted from Scott Kyle's Rakefile
# http://github.com/appden/appden.github.com/blob/master/Rakefile 

def jekyll(opts = "", path = "")
  sh "rm -Rf _site/*"
  sh path + "jekyll " + opts
end

desc "Build site using Jekyll"
task :build do
    jekyll
end

desc "Build site using Jekyll"
task :default => :build

namespace :build do
    desc "Serve at localhost:4000"
    task :server do
        jekyll("--future --server --auto")
    end
    
    desc "Serve at localhost:4000 sans autogeneration"
    task :hack do
      jekyll("--future --server")
    end
    
    desc "Build site with future posts"
    task :future do
        jekyll("--future")
    end
end
 
desc "Deploy to dev"
task :deploy => :"deploy:dev"
 
namespace :deploy do
  desc "Deploy to dev"
  task :dev => :"build:future" do
    rsync "jdios:/home/jdios/public_html/"
  end
  
  desc "Deploy to live"
  task :live => :build do
    ftp "jdios.jdchs.org"
  end
  
  desc "Deploy to dev and live"
  task :all => [:dev, :live]
  
  def rsync(location)
    sh "rsync -rtvz --exclude='.DS_Store' --delete _site/ #{location}"
  end

  def ftp(location)
    sh "lftp -c \"set ftp:list-options -a; \
        open #{location}\; \
	lcd ./_site; \
	cd /jdios; \
	mirror --reverse --delete --use-cache --verbose --allow-chown \
	--allow-suid --no-umask --parallel=2 --exclude .DS_STORE\""
  end
end
