# coding: utf-8
require 'cfndsl/rake_task'
require 'json'
require 'rake/clean'
require 'fileutils'

SRC_DIR = 'src/'
DIST_DIR = 'dist/'

PRODUCTS = 'dist/**/*.json'

CLEAN.include(FileList[DIST_DIR])

task :default => "beautify"

desc "JSONの整形"
task "beautify" => "generate" do
  Dir.glob(PRODUCTS).each do |path|
    File.open(path, 'r+') do |f|
      json = JSON.parse(f.read)
      f.rewind
      f.write JSON.pretty_generate(json)
    end
  end
end

desc "Cfnテンプレートを作成します"
task "copy2dist" => "clean" do
  FileUtils.cp_r(SRC_DIR, DIST_DIR)
  FileUtils.rm(Dir.glob("#{DIST_DIR}**/*.rb"))
end

CfnDsl::RakeTask.new do |t|
  t.cfndsl_opts = {
      verbose: true,
      files: Dir.glob("src/patterns/**/*.rb").map { |f|
        {filename: f, output: f.sub(/^src\//,"dist/").sub(/.rb$/,".json")}
      },
      extras: [
          [ :yaml, 'parameter/default.yml' ]
      ]
  }
end

Rake::Task[:generate].enhance([:copy2dist]) do
end