require 'rubygems'
require 'rake'

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "rdbi-driver-postgresql"
    gem.summary = %Q{PostgreSQL driver for RDBI}
    gem.description = %Q{PostgreSQL driver for RDBI}
    gem.email = "rdbi@pistos.oib.com"
    gem.homepage = "http://github.com/Pistos/rdbi-dbd-postgresql"
    gem.authors = [ "Pistos", "Erik Hollensbe" ]

    gem.add_development_dependency 'test-unit'
    gem.add_development_dependency 'rdoc'
    gem.add_development_dependency 'rdbi-dbrc'

    gem.add_dependency 'rdbi'
    gem.add_dependency 'pg', '= 0.9.0'
    gem.add_dependency 'epoxy', '>= 0.3.1'

    # gem is a Gem::Specification... see http://www.rubygems.org/read/chapter/20 for additional settings
  end
  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler (or a dependency) not available. Install it with: gem install jeweler"
end

require 'rake/testtask'
Rake::TestTask.new(:test) do |test|
  test.libs << 'lib' << 'test'
  test.pattern = 'test/**/test_*.rb'
  test.verbose = true
end

begin
  require 'rcov/rcovtask'
  Rcov::RcovTask.new do |test|
    test.libs << 'test'
    test.pattern = 'test/**/test_*.rb'
    test.verbose = true
  end
rescue LoadError
  task :rcov do
    abort "RCov is not available. In order to run rcov, you must: sudo gem install spicycode-rcov"
  end
end

task :test => :check_dependencies

begin
  require 'roodi'
  require 'roodi_task'
  RoodiTask.new do |t|
    t.verbose = false
  end
rescue LoadError
  task :roodi do
    abort "Roodi is not available. In order to run roodi, you must: sudo gem install roodi"
  end
end

begin
  require 'reek/rake/task'
  Reek::Rake::Task.new do |t|
    t.reek_opts << '-q'
  end
rescue LoadError
  task :reek do
    abort "Reek is not available. 'gem install reek'."
  end
end

task :default => :test

require 'rdoc/task'
RDoc::Task.new do |rdoc|
  version = File.exist?('VERSION') ? File.read('VERSION') : ""

  rdoc.rdoc_dir = 'rdoc'
  rdoc.title = "rdbi-dbd-postgresql #{version}"
  rdoc.rdoc_files.include('README*')
  rdoc.rdoc_files.include('lib/**/*.rb')
end
