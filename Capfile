load 'deploy' if respond_to?(:namespace) # cap2 differentiator

role :server, "wltv", "palmer", "pus2", "har", "har", "dbs"
role :backup, "backup"
role :web, "har"

desc "Do all"
task :all do
  freespace
  freeweb
  check_backups
end

desc "Check freespace on servers"
task :freespace, :roles => [:server, :backup] do
  output "df -h | head -2 | grep -v Filesystem"
end

desc "freespace on webserver"
task :freeweb, :roles => :web do
  output "df -h | grep 'webserver'"
end

desc "check backups"
task :check_backups, :roles => :backup do
  output "ls -ltr harlan/var/www/** | tail -1"
  output "ls -ltr palmer/var/www/** | tail -1"
  output "ls -ltr dbs/ | tail -1"
end

def output(cmd)
  run cmd do |ch, stream, data|
    puts data
  end
end