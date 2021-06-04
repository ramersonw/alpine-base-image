$script1 = <<-SCRIPT
apk update
apk add git make gcc python3 nodejs yarn php8 postgresql alpine-sdk
apk add curl bash libc6-compat libx11-dev libxkbfile-dev libsecret-dev
SCRIPT

$script2 = <<-SCRIPT
yarn global add node-gyp
yarn global add code-server
SCRIPT

$script3 = <<-SCRIPT
/usr/local/bin/code-server --install-extension esbenp.prettier-vscode
/usr/local/bin/code-server --install-extension eamodio.gitlens
/usr/local/bin/code-server --install-extension bmewburn.vscode-intelephense-client
SCRIPT

Vagrant.configure('2') do |config|
  config.vm.box = "alpine-dev"
  config.ssh.shell = '/bin/ash'
  config.vm.network "forwarded_port", guest: 3335, host: 3335, auto_correct: true
  config.vm.usable_port_range = 3333..3999
  config.vm.provider 'virtualbox' do |v|
    v.customize ['modifyvm', :id, '--vrde', 'off']
  end
  config.vm.provision "shell", inline: $script1
  config.vm.provision "shell", inline: $script2
  config.vm.provision "shell", inline: $script3
end