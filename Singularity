Bootstrap: docker
From: ubuntu:xenial

%help
Please refer to https://github.com/chidiugonna/nklab-neuro-tools for documentation about this singularity container.

%setup
cp ./src/resting_pipeline.py $SINGULARITY_ROOTFS
cp ./src/fsl_sub $SINGULARITY_ROOTFS
cp ./src/statusfeat.py $SINGULARITY_ROOTFS
cp ./src/runfeat-1.py $SINGULARITY_ROOTFS
cp ./src/make_fsl_stc.py $SINGULARITY_ROOTFS
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
export BXHVER=bxh_xcede_tools-1.11.1-lsb30.x86_64
export BXHBIN=/opt/$BXHVER
export RSFMRI=/opt/rsfmri_python
export PATH=$BXHBIN/bin:$PATH
export PATH=$BXHBIN/lib:$PATH
export PATH=$RSFMRI/bin:$PATH
export PATH=/opt/bin:$PATH
export PATH=/opt/abin:$PATH
export PATH=/opt/mrtrix3/bin:$PATH
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
export ANTSPATH=/opt/ANTScode/bin/bin
export PATH=$ANTSPATH:$PATH
export ITK_GLOBAL_DEFAULT_NUMBER_OF_THREADS=4 
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/.singularity.d/libs:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/usr/lib:$LD_LIBRARY_PATH
export PATH=/usr/local/cuda/bin:$PATH
export PATH=$PATH:/opt/build/CommandLine
export PATH=$PATH:/opt/build/Desktop
export PATH=$PATH:/opt/workbench/wb_shortcuts
%files

%runscript
cd /opt/data
exec /opt/bin/startup.sh "$@"

%test

%post
mkdir -p /uaopt /extra /xdisk /rsgrps /opt/data /opt/bin /opt/work /opt/input /opt/output
export BXHVER=bxh_xcede_tools-1.11.1-lsb30.x86_64
export BXHLOC=7384
export BXHBIN=/opt/$BXHVER
export RSFMRI=/opt/rsfmri_python
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

cd /tmp
echo "LC_ALL=en_US.UTF-8" >> /etc/environment
echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
echo "LANG=en_US.UTF-8" > /etc/locale.conf
locale-gen en_US.UTF-8

cd /tmp
wget https://cmake.org/files/v3.10/cmake-3.10.0-rc1.tar.gz
tar xz -f cmake-3.10.0-rc1.tar.gz
rm cmake-3.10.0-rc1.tar.gz
cd cmake-3.10.0-rc1
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


cd /opt
git clone https://github.com/Washington-University/workbench.git
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE=Release -D WORKBENCH_MESA_DIR=/usr -D WORKBENCH_USE_QT5=TRUE ../workbench/src
nice make -j8
#make install

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


chmod -R 777 /opt


mv /resting_pipeline.py /opt/bin
mv /fsl_sub $FSLDIR/bin
mv /statusfeat.py /opt/bin
mv /runfeat-1.py /opt/bin
mv /make_fsl_stc.py /opt/bin
mv /license.txt $FREESURFER_HOME
mv /startup.sh /opt/bin
mv /readme /opt/bin
mv /version /opt/bin

