# Adapted from Scott Kyle's Rakefile
# http://github.com/appden/appden.github.com/blob/master/Rakefile 

desc "Build site using Jekyll"
task :build => :"build:default"

namespace :build do
    desc "Build site using Jekyll"
    task :default do
        jekyll
    end
 
    desc "Serve at localhost:4000"
    task :server do
        jekyll("--server --auto")
    end
    
    desc "Serve at localhost:4000 sans autogeneration"
    task :hack do
      jekyll("--server")
    end
    
    desc "Build site with future posts"
    task :future do
        jekyll("--future")
    end
    
    def jekyll(opts = "", path = "")
      sh "rm -Rf _site/*"
      sh path + "jekyll " + opts
    end
end
 
desc "Deploy to dev"
task :deploy => :"deploy:dev"
 
namespace :deploy do
  desc "Deploy to dev"
  task :dev => :"build:future" do
    rsync "jack:/Users/admin/Sites/jd-ios"
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
