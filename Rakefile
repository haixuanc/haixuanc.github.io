require 'rake'

desc 'Preview the site with Jekyll'
task :preview do
    sh "bundle exec jekyll serve --watch --drafts --baseurl '' --config _config.yml,_config-dev.yml"
end

desc 'Search site and print specific deprecation warnings'
task :check do 
    sh "bundle exec jekyll doctor"
end
