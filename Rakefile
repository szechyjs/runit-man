require 'rubygems'
require 'rake/gempackagetask'

$LOAD_PATH.unshift('./lib')

require 'runit-man/version'

spec = Gem::Specification.new do |s|
  s.platform = Gem::Platform::RUBY
  s.summary = "Runit web management tool."
  s.name = 'runit-man'
  s.author = 'Akzhan Abdulin'
  s.email = 'akzhan.abdulin@gmail.com'
  s.homepage = 'https://github.com/Undev/runit-man'
  s.version = RunitManVersion::VERSION.dup
  s.requirements << 'none'
  s.require_path = 'lib'
  s.files = FileList["{bin,lib,public,views,i18n,sv}/**/*"].exclude(/^\.gitignore|supervise$/).to_a
  s.executables << 'runit-man'
  s.add_dependency 'yajl-ruby'
  s.add_dependency 'erubis'
  s.add_dependency 'sinatra', '>= 1.1'
  s.add_dependency 'sinatra-content-for2', '>=0.2.4'
  s.add_dependency 'sinatra-r18n', '>=0.4.2'
  s.add_development_dependency 'rspec-core'
  s.add_development_dependency 'rspec-expectations'
  s.add_development_dependency 'rr'
  s.add_development_dependency 'rack-test'
  s.description = File.open(File.join(File.dirname(__FILE__), 'DESCRIPTION')).read
end

task :default => [:package]

Rake::GemPackageTask.new(spec) do |pkg|
  pkg.need_tar = true
end

begin
  require 'rspec/core/rake_task'

  RSpec::Core::RakeTask.new do |t|
    t.rspec_opts = ["-c", "-f progress"]
  end

  RSpec::Core::RakeTask.new(:rcov) do |t|
    t.rcov = true
    t.ruby_opts = '-w'
    t.rspec_opts = ["-c", "-f progress"]
    t.rcov_opts = %q[-Ilib --exclude "spec/*,gems/*"]
  end
rescue LoadError
  $stderr.puts "RSpec not available. Install it with: gem install rspec-core rspec-expectations"
end

