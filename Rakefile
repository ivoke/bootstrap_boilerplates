require 'rubygems'
require 'bundler'
begin
  Bundler.setup(:default, :development)
rescue Bundler::BundlerError => e
  $stderr.puts e.message
  $stderr.puts "Run `bundle install` to install missing gems"
  exit e.status_code
end
require 'rake'

VERSION = "2.0.3"
DIRECTORY = "docs/assets/css"
BOOTSTRAP_CSS = "#{DIRECTORY}/bootstrap.css"
BOOTSTRAP_RESPONSIVE_CSS = "#{DIRECTORY}/responsive.css"

SASS_COMMAND = "sass --precision 10 --load-path lib --style"

task BOOTSTRAP_CSS do |target|
  sh "#{SASS_COMMAND} expanded lib/bootstrap.scss:#{target}"
  css = IO.read(target.to_s)
  css.gsub!('@DATE', `date`.strip)
  File.open(target.to_s, 'w+') { |f| f.write(css) }
end

task BOOTSTRAP_RESPONSIVE_CSS do |target|
  sh "#{SASS_COMMAND} expanded lib/responsive.scss:#{target}"
  css = IO.read(target.to_s)
  css.gsub!('@DATE', `date`.strip)
  File.open(target.to_s, 'w+') { |f| f.write(css) }
end


desc "build regular and compresed versions of bootstrap"
task :build => [BOOTSTRAP_CSS, BOOTSTRAP_RESPONSIVE_CSS]

desc "rebuild bootstrap when modifications are made"
task :watch do
  sh "#{SASS_COMMAND} expanded --watch lib:#{DIRECTORY}"
end

task :default => :build
