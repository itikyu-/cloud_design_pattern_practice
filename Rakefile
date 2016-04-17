require 'cfndsl/rake_task'

CfnDsl::RakeTask.new do |t|
  t.cfndsl_opts = {
    verbose: true,
    files: [{
      filename: 'templates/application.rb',
      output: 'application.json'
    }],
    extras: [
      [ :yaml, 'templates/default_params.yml' ]
    ]
  }
end
