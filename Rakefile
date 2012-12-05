# Adapted from Scott Kyle's Rakefile
# http://github.com/appden/appden.github.com/blob/master/Rakefile

def jekyll(opts = "", path = "/Users/adamwalz/.rvm/gems/ruby-1.9.3-p194/bin/")
  sh "rm -Rf _site/*"
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
