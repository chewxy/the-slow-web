#!/usr/bin/ruby

SASS_DIR = "assets/sass"
CSS_DIR  = "assets/css"

desc "Alias for 'rake list'"
task :default => [:list]

desc "Serve the site on localhost and watch for SASS changes."
task :serve, [:style] do |task, args|
  args.with_defaults(:style => "compressed")
  jekyll_process = Process.spawn("jekyll serve --watch")
  sass_process   = Process.spawn("sass --watch #{SASS_DIR}:#{CSS_DIR} --style #{args.style}")
  processes = [jekyll_process, sass_process]
  trap("INT") do
    processes.each do |process|
      Process.kill(9, process) rescue Errno::ESRCH
    end
    exit 0
  end
  processes.each do |process|
    Process.wait(process)
  end
end

desc "List all rake tasks"
task :list do
  system "rake -T"
end
