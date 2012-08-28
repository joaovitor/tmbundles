namespace :textmate do
  desc "Textmate setup with submodules"
  task :setup do
    [
      ["git://github.com/vigetlabs/whitespace-tmbundle.git", "Whitespace.tmbundle"],
      ["git://github.com/bmabey/cucumber-tmbundle.git", "Cucumber.tmbundle"],
      ["git://github.com/carlosbrando/handcrafted-haml-textmate-bundle.git", "Haml.tmbundle"],
      ["git://github.com/carlosbrando/ruby-on-rails-tmbundle.git", "Ruby on Rails.tmbundle"],
      ["git://github.com/rspec/rspec-tmbundle.git", "RSpec.tmbundle"],
      ["git://github.com/drnic/Bundler.tmbundle.git"],
      ["git://github.com/drnic/copy-as-rtf-tmbundle.git", "Copy as RTF.tmbundle"],
      ["git://github.com/drnic/ruby-shoulda-tmbundle.git", "Shoulda.tmbundle"],
      ["git://github.com/jcf/git-tmbundle.git", "Git.tmbundle"],
      ["git://github.com/szeryf/rails-routes.tmbundle.git"],
      ["git://github.com/pivotal/jasmine-tmbundle.git", "Jasmine.tmBundle"],
    ].each do |git_path, path|
      path = "\"#{path}\"" if path
      system "git submodule add #{git_path} #{path}"
    end
  end

  desc "Install this Bundles configuration as your official Bundles"
  task :install do
    cmd_exec = lambda{|cmd_to_execute|system "#{cmd_to_execute}"; puts "Executed #{cmd_to_execute}"}
    cmd_exec["git submodule init"]
    cmd_exec["git submodule update"]
    app_support = File.join(ENV["HOME"], "Library", "Application Support", "Textmate")
    bundles_dir = File.join(app_support, "Bundles")
    bundlesbkp_dir = File.join(app_support, "Bundles-bkp")
    if File.exist?(bundles_dir)
      puts "Your old Bundles backup path is: #{bundlesbkp_dir}"
      FileUtils.mv bundles_dir, bundlesbkp_dir, :verbose => true
    end
    FileUtils.ln_s "#{File.expand_path(File.dirname(__FILE__))}", bundles_dir, :verbose => true
    Rake::Task['textmate:reload'].invoke
  end

  desc "Reload textmate setup"
  task :reload do
    system %Q{osascript -e 'tell app "TextMate" to reload bundles'}
    puts "Textmate setup reloaded!"
  end
end