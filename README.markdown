# A Recipe for a Redis RPM on CentOS

Perform the following on a build box as a user. (not root, never build as root)

## Get the prerequisite files
    
    sudo yum install rpmdevtools
    sudo yum groupinstall 'Development Tools

## Create an RPM Build Environment
    cd ~
    rpmdev-setuptree
    mkdir tmp
    cd tmp

## Download Redis

    wget http://download.redis.io/releases/redis-2.8.4.tar.gz
    cp redis-2.8.4.tar.gz ~/rpmbuild/SOURCES/

## Get Necessary System-specific Configs

    git clone git://github.com/uow-dmurrell/redis-centos.git
    cp redis-centos/spec/redis.spec ~/rpmbuild/SPECS/

## Build the RPM

    cd ~/rpmbuild/
    rpmbuild -ba SPECS/redis.spec

The resulting RPM will be:

    ~/rpmbuild/RPMS/x86_64/redis-2.8.4-stable.x86_64.rpm

## Credits

Based on the `redis.spec` file from Jason Priebe, found on [Google Code][gc].
(2014) Forked from https://github.com/causes/redis-centos, plus a few improvements from some unmerged pull requests.

 [gc]: http://groups.google.com/group/redis-db/files
