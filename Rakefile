@dtach_session = File.expand_path("tmp/session.dtach")
@rtorrent_session = File.expand_path("tmp/rtorrent.session")
@files_dir = File.expand_path("files")
@files_server = "opensourcebridge.org"

task :default => :help

task :help do
  puts "Tasks for Open Source Bridge's Bittorent server:"
  system "rake --silent -T"
end

desc "Start torrent server in the background"
task :start do
  sh "dtach -n #{@dtach_session} rake _serve"
end

desc "Stop torrent server"
task :stop do
  sh "expect bin/stop.expect"
end

desc "Restart torrent server"
task :restart => [:stop, :start]

desc "Attach to torrent server's console"
task :attach do
  puts '* Attaching to running session: CTRL-\ to detach, CTRL-q to stop'
  exec "dtach -a #{@dtach_session}"
end

task :connect => :attach

task :_serve do
  mkdir_p @rtorrent_session
  exec "rtorrent -s #{@rtorrent_session} -o cwd=#{@files_dir},upload_rate=768,port_range=14305-14399 #{@files_dir}/*.torrent"
end

desc "Pull torrent files from opensourcebridge.org to here"
task :pull do
  sh "rsync -vax --partial --stats --progress #{@files_server}:#{@files_dir} ."
end

desc "Update cron to start server on boot"
task :cron do
  sh "echo '@reboot cd #{Dir.pwd} && rake start' | crontab -"
end
