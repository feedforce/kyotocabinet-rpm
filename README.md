# What is this spec?

Import kyotocabinet.spec of https://github.com/kyohsuke/srpms/blob/master/kyotocabinet-1.2.76-1.src.rpm

# Example to build SRPM and RPM

You need to install [VirtualBox](https://www.virtualbox.org/) and [Vagrant](http://www.vagrantup.com/).

```
$ vagrant up
$ vagrant ssh
$ mkdir -p ~/rpmbuild/{BUILD,BUILDROOT,RPMS,SOURCES,SPECS,SRPMS}
$ (cd ~/rpmbuild/SOURCES && curl -LO http://fallabs.com/kyotocabinet/pkg/kyotocabinet-1.2.76.tar.gz)
$ cp /vagrant/kyotocabinet.spec ~/rpmbuild/SPECS
$ sudo yum update -y
$ sudo yum install -y rpm-build
$ rpmbuild -ba ~/rpmbuild/SPECS/kyotocabinet.spec
エラー: ビルド依存性の失敗:
        gcc-c++ は kyotocabinet-1.2.76-1.x86_64 に必要とされています
        zlib-devel は kyotocabinet-1.2.76-1.x86_64 に必要とされています
$ sudo yum install -y gcc-c++ zlib-devel
$ rpmbuild -ba ~/rpmbuild/SPECS/kyotocabinet.spec
(snip)
書き込み完了: /home/vagrant/rpmbuild/SRPMS/kyotocabinet-1.2.76-1.src.rpm
書き込み完了: /home/vagrant/rpmbuild/RPMS/x86_64/kyotocabinet-1.2.76-1.x86_64.rpm
書き込み完了: /home/vagrant/rpmbuild/RPMS/x86_64/kyotocabinet-devel-1.2.76-1.x86_64.rpm
```

## How to build RPM from SRPM

```
$ vagrant up
$ vagrant ssh
$ sudo yum update -y
$ sudo yum install -y rpm-build
$ curl -LO https://github.com/feedforce/kyotocabinet-rpm/releases/download/1.2.76/kyotocabinet-1.2.76-1.src.rpm
$ rpmbuild --rebuild kyotocabinet-1.2.76-1.src.rpm
kyotocabinet-1.2.76-1.src.rpm をインストール中です。
エラー: ビルド依存性の失敗:
        gcc-c++ は kyotocabinet-1.2.76-1.x86_64 に必要とされています
        zlib-devel は kyotocabinet-1.2.76-1.x86_64 に必要とされています
$ sudo yum install -y gcc-c++ zlib-devel
$ rpmbuild --rebuild kyotocabinet-1.2.76-1.src.rpm
(snip)
書き込み完了: /home/vagrant/rpmbuild/RPMS/x86_64/kyotocabinet-1.2.76-1.x86_64.rpm
書き込み完了: /home/vagrant/rpmbuild/RPMS/x86_64/kyotocabinet-devel-1.2.76-1.x86_64.rpm
```
