require 'rake'

require 'rspec/core/rake_task'
require 'puppet-lint'

task :lint do
  PuppetLint.configuration.with_filename = true
  PuppetLint.configuration.fail_on_warnings = true
  linter = PuppetLint.new

  Dir.glob('spec/fixtures/modules/aptmirror/manifests/**/*.pp').each do |file|
    linter.file = file
    linter.run
  end
  fail if linter.errors?
end

task :bootstrap do
  Dir.chdir('spec/fixtures') do
    `bundle exec librarian-puppet install`
  end
end

RSpec::Core::RakeTask.new(:spec) do |t|
  t.pattern = 'spec/*/*_spec.rb'
end

task :test => [:bootstrap, :spec, :lint]
