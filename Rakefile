require "bundler/gem_tasks"
require "rspec/core/rake_task"
require "open-uri"

def yellow(str)
  "\e[33m#{str}\e[m"
end

ENV['VAGRANT_CWD'] = File.expand_path('spec/integration/vm')


desc 'Run unit and integration tests'
task :spec => ['spec:unit', 'spec:integration']

namespace :spec do
  RSpec::Core::RakeTask.new("unit") do |task|
    task.pattern = "./spec/unit{,/*/**}/*_spec.rb"
  end

  RSpec::Core::RakeTask.new("integration") do |task|
    task.pattern = "./spec/integration{,/*/**}/*_spec.rb"
  end

  namespace :integration do
    integration_dir = 'spec/integration'

    desc 'Clean'
    task :clean => ['vagrant:destroy'] do
    end

    desc 'Prepare'
    task :prepare => ['vagrant:up'] do
    end

    namespace :vagrant do
      task :up do
        puts yellow('Starting VM...')
        system 'vagrant', 'up'
      end

      task :destroy do
        puts yellow('Destroying VM...')
        system 'vagrant', 'destroy', '-f'
      end

      task :provision do
        puts yellow('Provisioning VM...')
        system 'vagrant', 'provision'
      end

      task :ssh, :name do |t, args|
        system 'vagrant', 'ssh', args[:name]
      end
    end
  end
end
