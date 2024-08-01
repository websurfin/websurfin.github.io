source "https://rubygems.org"
gem "github-pages", "~> 231", group: :jekyll_plugins

# building on default theme from Jekyll
gem "minima"

# to use GitHub Pages, remove the "gem "jekyll"" uncomment the bundle line below`.
gem "jekyll", "~> 3.9.5"

group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.17.0"  
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library. [from template]
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", "~> 1.2"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows [from template]
gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]

gem "webrick", "~> 1.7"
