source "https://rubygems.org"

gem "jekyll", "~> 4.4.0"
gem 'logger', '~> 1.6'

group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
  gem "jekyll-toc", "~> 0.19"
  gem "jekyll-target-blank", "~> 2.0.2"
  gem "liquid_reading_time", "~> 1.1.3"
  gem "jekyll-loading-lazy", "~> 0.1.1"
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1", :platforms => [:mingw, :x64_mingw, :mswin]

# Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds since newer versions of the gem
# do not have a Java counterpart.
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]
