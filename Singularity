Bootstrap: docker
From: ubuntu:xenial

%help
Please refer to https://github.com/chidiugonna/nklab-neuro-tools for documentation about this singularity container.

%setup
cp ./src/fsl_sub $SINGULARITY_ROOTFS
cp ./src/changePython2.sh $SINGULARITY_ROOTFS
cp ./src/changePython3.sh $SINGULARITY_ROOTFS
cp ./src/license.txt $SINGULARITY_ROOTFS
cp ./src/startup.sh $SINGULARITY_ROOTFS
cp ./src/readme $SINGULARITY_ROOTFS
cp ./src/version $SINGULARITY_ROOTFS


%environment
LD_LIBRARY_PATH=/usr/local/cuda/lib64:/.singularity.d/libs:/usr/lib:/opt/freesurfer/mni/lib:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH
export FSLDIR=/opt/fsl
export PATH=$FSLDIR/bin:$PATH
export PATH=$FSLDIR/bin/FSLeyes:$PATH
export PATH=/opt/bin:$PATH
export FREESURFER_HOME=/opt/freesurfer
export FUNCTIONALS_DIR=/opt/freesurfer/sessions
export FSFAST_HOME=/opt/freesurfer/fsfast
export FS_LICENSE=$FREESURFER_HOME/license.txt
export SUBJECTS_DIR=/opt/freesurfer/subjects
export MINC_BIN_DIR=/opt/freesurfer/mni/bin
export MINC_LIB_DIR=/opt/freesurfer/mni/lib
export MNI_PERL5LIB=$FREESURFER_HOME/mni/share/perl5
export PERL5LIB=$FREESURFER_HOME/mni/share/perl5
export FSL_DIR=/opt/fsl
export MNI_DIR=/opt/freesurfer/mni
export MNI_DATAPATH=/opt/freesurfer/mni/data
export FSF_OUTPUT_TYPE=nii.gz
export SUBJECTS_DIR=/opt/data/freesurfer-outputs
export PATH=$FREESURFER_HOME/bin:$PATH
export PATH=$FREESURFER_HOME/tktooks:$PATH
export PATH=$FREESURFER_HOME/fsfast/bin:$PATH
export PATH=$FREESURFER_HOME/mni/bin:$PATH
export PATH=$MNI_DIR/bin:$PATH
export LD_LIBRARY_PATH=/.singularity.d/libs:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/usr/lib:$LD_LIBRARY_PATH
export PATH=$PATH:/opt/build/CommandLine
export PATH=$PATH:/opt/build/Desktop
export PATH=$PATH:/opt/workbench/wb_shortcuts
export MYBASEDIR=/opt
export PATH=$PATH:${MYBASEDIR}/ciftify/ciftify/bin
export PYTHONPATH=$PYTHONPATH:${MYBASEDIR}/ciftify
export CIFTIFY_TEMPLATES=${MYBASEDIR}/ciftify/data
export HCP_DATA=/opt/data/
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8

%files

%runscript
cd /opt/data
exec /opt/bin/startup.sh "$@"

%test

%post
mkdir -p /uaopt /extra /xdisk /rsgrps /opt/data /opt/bin /opt/work /opt/input /opt/output
apt-get update && apt-get install -y \
	nano \
	wget \
	curl \
        dc \
	lsb-core \
	python-pip \
        libx11-6 \
        libgl1 \
        libgtk-3-0 \
        libgtk-3-dev \
        libsm6 \
        libxext6 \
        libxt6 \
        mesa-common-dev \
        freeglut3-dev \
        zlib1g-dev \
        libpng-dev \
        expat \
        unzip \
        libeigen3-dev \
        zlib1g-dev \
        libqt4-opengl-dev \
        libgl1-mesa-dev \
        libosmesa6-dev \
        libfftw3-dev \
        libtiff5-dev \
        qt5-default \
        qtdeclarative5-dev \
        graphviz \
        libgraphviz-dev \
        software-properties-common      
add-apt-repository universe
apt-get update && apt-get install -y \
        tcsh \
        xfonts-base \
        python-qt4 \
        gsl-bin \
        gnome-tweak-tool \
        libjpeg62 \
        xvfb \
        xterm \
        vim \
        libglu1-mesa-dev \
        libglw1-mesa   \
        libxm4 \
        netpbm
apt-get update && apt-get install -y \
        hdf5-tools \
        openmpi-bin \
        openmpi-doc \
        libopenmpi-dev \
        gfortran \
        python-matplotlib \
        git \
        x11-xserver-utils \
        firefox \
        midori \
        python3-pip \
        
pip install numpy
pip install scipy
pip install nibabel
pip install networkx==1.11
pip install nipype
pip install rdflib
pip install nipy
pip install dipy
pip install jupyter
pip install pyBIDS

pip3 install xgboost
pip3 install numpy
pip3 install scipy
pip3 install nibabel
pip3 install networkx==1.11
pip3 install nipype
pip3 install rdflib
pip3 install nipy
pip3 install dipy
pip3 install nitime
pip3 install nilearn
pip3 install MNE
pip3 install nilearn
pip3 install jupyter
pip3 install pyBIDS
pip3 install docopt
pip3 install matplotlib
pip3 install pandas
pip3 install pyyaml
pip3 install seaborn
pip3 install Pillow


cd /tmp
echo "LC_ALL=en_US.UTF-8" >> /etc/environment
echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
echo "LANG=en_US.UTF-8" > /etc/locale.conf
locale-gen en_US.UTF-8
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8

cd /tmp
wget https://cmake.org/files/v3.12/cmake-3.12.0-rc3.tar.gz
tar xz -f cmake-3.12.0-rc3.tar.gz
rm cmake-3.12.0-rc3.tar.gz
cd cmake-3.12.0-rc3
./configure
make
make install
./bootstrap --prefix=/usr
make
make install

cd /tmp
wget http://www.vtk.org/files/release/7.1/VTK-7.1.1.tar.gz
tar xz -f VTK-7.1.1.tar.gz
rm VTK-7.1.1.tar.gz
cd VTK-7.1.1
cmake .
make
make install

#install QT 5.9
printf '\n' | add-apt-repository ppa:beineri/opt-qt59-xenial
apt-get update
apt install -y qt-latest  

#set up environmental variables
export PATH=/opt/qt59/bin:$PATH
export LD_LIBRARY_PATH=/opt/qt59/lib:$LD_LIBRARY_PATH
export QT_SELECT=opt-qt59
export QTTOOLDIR=/opt/qt59/bin
export QTLIBDIR=/opt/qt59/lib

cd /opt
git clone https://github.com/Washington-University/workbench.git
mkdir build
cd build
cmake -D CMAKE=/opt/qt59/lib/cmake -D QMAKE=/opt/qt59/bin/qmake CMAKE_BUILD_TYPE=Release -D WORKBENCH_MESA_DIR=/usr -D WORKBENCH_USE_QT5=TRUE ../workbench/src
sed -i "s#/usr/lib/x86_64-linux-gnu/cmake#/opt/qt59/lib/cmake#g" CMakeCache.txt
nice make -j8

cd /opt/workbench
git clone https://github.com/Washington-University/wb_shortcuts.git

cd /opt
export FREESURFER_HOME=/opt/freesurfer
wget ftp://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/dev/freesurfer-linux-centos6_x86_64-dev.tar.gz
tar xz -f freesurfer-linux-centos6_x86_64-dev.tar.gz
cd /usr/lib/x86_64-linux-gnu
ln -s libtiff.so.4 libtiff.so.3
rm /opt/freesurfer-linux-centos6_x86_64-dev.tar.gz
cd $FREESURFER_HOME
curl "https://surfer.nmr.mgh.harvard.edu/fswiki/MatlabRuntime?action=AttachFile&do=get&target=runtime2014bLinux.tar.gz" -o "runtime.tar.gz"
tar xvf runtime.tar.gz
rm $FREESURFER_HOME/runtime.tar.gz

cd /opt
export FSLDIR=/opt/fsl
export PATH=${FSLDIR}/bin:${PATH}
wget https://www.dropbox.com/s/chetucmygqyz992/fsl-5.0.11-sources.tar.gz
tar xz -f fsl-5.0.11-sources.tar.gz
rm fsl-5.0.11-sources.tar.gz
chmod -R 777 fsl
sed -i 's/#FSLCONFDIR/FSLCONFDIR/g' ${FSLDIR}/etc/fslconf/fsl.sh
sed -i 's/#FSLMACHTYPE/FSLMACHTYPE/g' ${FSLDIR}/etc/fslconf/fsl.sh
sed -i 's/#export FSLCONFDIR/export FSLCONFDIR /g' ${FSLDIR}/etc/fslconf/fsl.sh
. ${FSLDIR}/etc/fslconf/fsl.sh
cp -r ${FSLDIR}/config/linux_64-gcc4.8 ${FSLDIR}/config/${FSLMACHTYPE}
sed -i "s#scl enable devtoolset-2 -- c++#c++#g" $FSLDIR/config/$FSLMACHTYPE/systemvars.mk
sed -i "s#CUDA_INSTALLATION = /opt/cuda-7.5#CUDA_INSTALLATION = /usr/local/cuda-8.0#g" $FSLDIR/config/$FSLMACHTYPE/systemvars.mk
sed -i "s#VTKDIR_INC = /home/fs0/cowboy/var/caper_linux_64-gcc4.4/VTK7/include/vtk-7.0#VTKDIR_INC = /usr/local/include/vtk-7.1/#g" $FSLDIR/config/$FSLMACHTYPE/externallibs.mk
sed -i "s#VTKDIR_LIB = /home/fs0/cowboy/var/caper_linux_64-gcc4.4/VTK7/lib#VTKDIR_LIB = /usr/local/lib/#g" $FSLDIR/config/$FSLMACHTYPE/externallibs.mk
sed -i "s#VTKSUFFIX = -7.0#VTKSUFFIX = -7.1#g" $FSLDIR/config/$FSLMACHTYPE/externallibs.mk
sed -i "s#{LIBRT}#{LIBRT} -ldl#g" $FSLDIR/src/mist-clean/Makefile
sed -i "s#lpng -lz#lpng -lz -lm#g" $FSLDIR/src/miscvis/Makefile
cd ${FSLDIR}
./build
sed -i "s#dropprivileges=1#dropprivileges=0#g" ${FSLDIR}/etc/fslconf/fslpython_install.sh
${FSLDIR}/etc/fslconf/fslpython_install.sh
mkdir -p $FSLDIR/bin/eddypatch
cd  ${FSLDIR}/bin/eddypatch
wget https://fsl.fmrib.ox.ac.uk/fsldownloads/patches/eddy-patch-fsl-5.0.11/centos6/eddy_cuda8.0
chmod +x eddy_cuda8.0
wget https://fsl.fmrib.ox.ac.uk/fsldownloads/patches/eddy-patch-fsl-5.0.11/centos6/eddy_openmp
chmod +x eddy_openmp
cd  ${FSLDIR}/bin
wget https://fsl.fmrib.ox.ac.uk/fsldownloads/fsleyes/FSLeyes-latest-ubuntu1604.zip
unzip FSLeyes-latest-ubuntu1604.zip
rm FSLeyes-latest-ubuntu1604.zip

cd /tmp
wget https://www.dropbox.com/s/61ew2urguo3t27j/probtrackx2_gpu_80.zip
unzip probtrackx2_gpu_80.zip
rm -f probtrackx2_gpu.zip
mv probtrackx2_gpu $FSLDIR/bin

mkdir /tmp/bedpost
cd /tmp/bedpost
wget https://www.dropbox.com/s/zj9ad4qtmxwkq2r/bedpostx_gpu_80.zip
unzip bedpostx_gpu_80.zip
rm -f bedpostx_gpu.zip
cp /tmp/bedpost/bin/* $FSLDIR/bin
cp /tmp/bedpost/lib/* $FSLDIR/lib
rm -r /tmp/bedpost
sed -i 's\#!/bin/sh\#!/bin/bash\g' $FSLDIR/bin/bedpostx_postproc_gpu.sh

mv /changePython2.sh /opt/bin/changePython2.sh
mv /changePython3.sh /opt/bin/changePython3.sh

. /opt/bin/changePython3.sh
export MYBASEDIR=/opt
cd ${MYBASEDIR}
git clone https://github.com/edickie/ciftify.git
export PATH=$PATH:${MYBASEDIR}/ciftify/ciftify/bin
export PYTHONPATH=$PYTHONPATH:${MYBASEDIR}/ciftify
export CIFTIFY_TEMPLATES=${MYBASEDIR}/ciftify/data
export HCP_DATA=/opt/data/


chmod -R 777 /opt

mv /fsl_sub $FSLDIR/bin
mv /license.txt $FREESURFER_HOME
mv /startup.sh /opt/bin
mv /readme /opt/bin
mv /version /opt/bin

