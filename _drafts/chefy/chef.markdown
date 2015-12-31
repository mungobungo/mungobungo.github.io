get temprorary access for hosted chef server

create virtual box for ubuntu, just in case
download [ubuntu chef-dk](https://downloads.chef.io/chef-dk/ubuntu/)
```
vagrant@vagrant-VirtualBox:~/Downloads$ cd Downloads/
vagrant@vagrant-VirtualBox:~/Downloads$ sudo dpkg -i chefdk_0.10.0-1_amd64.deb
Selecting previously unselected package chefdk.
(Reading database ... 194539 files and directories currently installed.)
Preparing to unpack chefdk_0.10.0-1_amd64.deb ...
Unpacking chefdk (0.10.0-1) ...
Setting up chefdk (0.10.0-1) ...
Thank you for installing Chef Development Kit!
vagrant@vagrant-VirtualBox:~/Downloads$
```

visually ![screenshot](images/install-chef-dk.png)

installing provisioning
```
gem install -V -y chef-provisioning-docker
```

but got this:
```
ERROR:  Error installing chef-provisioning-docker:
	ERROR: Failed to build gem native extension.

        /usr/bin/ruby1.9.1 extconf.rb
/usr/lib/ruby/1.9.1/rubygems/custom_require.rb:36:in `require': cannot load such file -- mkmf (LoadError)
	from /usr/lib/ruby/1.9.1/rubygems/custom_require.rb:36:in `require'
	from extconf.rb:39:in `deps'
	from extconf.rb:89:in `makemakefiles'
	from extconf.rb:138:in `<main>'
```

so trying to add dependendices

```
sudo apt-get install libxml2-dev libxslt-dev g++ ruby-dev
```

and failing again because of
```
ERROR:  Error installing chef-provisioning-docker:
	ohai requires Ruby version >= 2.0.0.

```

okey dokey..

installing rvm then

```
curl -sSL https://rvm.io/mpapis.asc | gpg --import -
curl -L https://get.rvm.io | bash -s stable --ruby

```

after a while

```
* To start using RVM you need to run `source /home/vagrant/.rvm/scripts/rvm`
    in all your open shell windows, in rare cases you need to reopen all shell windows.
```

so let's check it

```
ruby --version
ruby 2.2.1p85 (2015-02-26 revision 49769) [x86_64-linux]
```

and run again

```
sudo gem install -V -y chef-provisioning-docker chef-provisioning-aws chef-provisioning-fog
```

and after that

config files

```
cat ~/.aws/config
[default]
region=us-west-2
output=json

```

and also

```
cat ~/.aws/credentials
[default]
aws_access_key_id = KEY
aws_secret_access_key = another_KEY

```

running everything locally
```
chef-client -z  cluster.rb
```

```
require 'chef/provisioning'

chef_provisioning :image_max_wait_time => 600, :machine_max_wait_time => 240

timetag = Time.now. strftime("%Y-%m-%d_%H_%M_%S")
machine "mario#{timetag}" do
  tag 'itsa_me'
end

num_webservers = 1

machine_batch do
  1.upto(num_webservers) do |i|
    machine "luigi#{i}" do
     recipe 'apache'
#     recipe 'mywebapp'
    end
  end
end
~        
```
