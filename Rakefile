# Stolen from @ejfinneran who stole is from @holman.
# Heavily modified to support extra scripts.

require 'rake'

desc "Hook our dotfiles into system-standard positions."
task :install do
  linkables = Dir.glob('*/**{.symlink}')
  `git submodule init`
  `git submodule update`
  skip_all = false
  overwrite_all = false
  backup_all = false

  linkables.each do |linkable|
    next if linkable.split('/').first == 'bin' # We'll install these seperately

    overwrite = false
    backup = false

    file = linkable.split('/').last.split('.symlink').last
    target = "#{ENV["HOME"]}/.#{file}"

    if File.exists?(target) || File.symlink?(target)
      unless skip_all || overwrite_all || backup_all
        puts "File already exists: #{target}, what do you want to do? [s]kip, [S]kip all, [o]verwrite, [O]verwrite all, [b]ackup, [B]ackup all"
        case STDIN.gets.chomp
        when 'o' then overwrite = true
        when 'b' then backup = true
        when 'O' then overwrite_all = true
        when 'B' then backup_all = true
        when 'S' then skip_all = true
        when 's' then next
        end
      end
      FileUtils.rm_rf(target) if overwrite || overwrite_all
      `mv "$HOME/.#{file}" "$HOME/.#{file}.backup"` if backup || backup_all
    end
    `ln -s "$PWD/#{linkable}" "#{target}"`
  end
end

task :uninstall do
  Dir.glob('**/*.symlink').each do |linkable|

    file = linkable.split('/').last.split('.symlink').last
    target = "#{ENV["HOME"]}/.#{file}"

    # Remove all symlinks created during installation
    if File.symlink?(target)
      FileUtils.rm(target)
    end
    
    # Replace any backups made during installation
    if File.exists?("#{ENV["HOME"]}/.#{file}.backup")
      `mv "$HOME/.#{file}.backup" "$HOME/.#{file}"` 
    end
  end
end

# I love writing little scripts to automate everyday tasks,
# but hate having to use Github gist to sync between environments.
# This makes that so much easier! Takes the bin directory in this repo
# and symlinks all files to the bin folder, adding them to the path.
desc "Hook all our binfiles into /usr/bin"
task :binfiles do
  binfiles = Dir.glob('bin/**{.symlink}')
  # TODO: Worry about overwriting files. But for now, YOLO!

  binfiles.each do |binfile|
    target = '/usr/' + binfile.split('.symlink').last
    `sudo ln -s "$PWD/#{binfile}" "#{target}"`
    `sudo chmod +x #{target}`
    puts "Symlinked #{binfile} to #{target}"
  end
end

task :default => 'install'
