# lustre_prac
0. ntp설정
1. iml 다운로드 및 서버 추가
2. 러스터 설치
3. lnet 설정 및 시작
4. 러스터 모듈 추가
5. zfs 모듈 추가 
6. zfspool 생성
7. dataset 생성
8. 마운트
9. iml
 
------------------------------------
managed lustre
--------------

yum repolist

yum-config-manager --disable updates
yum install -y createrepo vsftpd
mkdir /repo
mount -t nfs 10.73.10.33:/root/Downloads /repo

tar -xvzf /repo/local_repos.tar.gz -C /var/ftp
createrepo /var/ftp

vi /etc/yum.repos.d/remote.repo

[remote]
name=reomte
baseurl=ftp://10.73.10.10
enabled=1
gpgcheck=0

yum-config-manager --enable remote
yum repolist
yum install -y python2-iml-manager
chroma-config setup admin lustre localhost --no-dbspace-check -v

chroma --username admin --password lustre server add mds1.local --server_profile base_managed_rh7

--------------------------------

lnetctl set discovery [0 | 1]
