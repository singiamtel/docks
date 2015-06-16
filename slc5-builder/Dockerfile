FROM centos:5

# Patch uname
COPY fake-uname-slc5.sh /bin/uname

# Operations:
# - Install RPMforge (needed for git)
# - Install some required packages
# - Make ccache used by default
# - Install CMake v2.8 (only v2.6 is available from repos)
RUN \
  yum install -y wget && \
  mkdir /tmp/rpmforge && \
  cd /tmp/rpmforge && \
  rpm --import http://apt.sw.be/RPM-GPG-KEY.dag.txt && \
  wget http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el5.rf.x86_64.rpm && \
  yum install -y rpmforge-release-0.5.3-1.el5.rf.x86_64.rpm && \
  rm -rf /tmp/rpmforge && \
  yum install -y subversion install autoconf automake libtool zlib-devel libxml2-devel \
    openssl-devel gcc-c++ gcc-gfortran make libX11-devel libXpm-devel libXft-devel libXext-devel \
    mesa-libGLU-devel git curl bzip2 which file redhat-lsb bzip2-devel python-devel gmp gmp-devel \
    ccache java-1.7.0-openjdk && \
  yum clean all && \
  ln -nfs /usr/bin/ccache /usr/local/bin/gcc && \
  ln -nfs /usr/bin/ccache /usr/local/bin/g++ && \
  ln -nfs /usr/bin/ccache /usr/local/bin/cc && \
  ln -nfs /usr/bin/ccache /usr/local/bin/c++ && \
  mkdir /tmp/cmake && \
  cd /tmp/cmake && \
  wget http://www.cmake.org/files/v2.8/cmake-2.8.12.tar.gz && \
  tar xzf *.tar.gz && \
  cd cmake-2.8.12 && \
  ./bootstrap && \
  make -j$( grep -c bogomips /proc/cpuinfo ) install && \
  rm -rf /tmp/cmake