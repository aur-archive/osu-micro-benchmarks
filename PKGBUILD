# Maintainer: Jason St. John <jstjohn .. purdue . edu>

pkgname=osu-micro-benchmarks
pkgver=4.4.1
pkgrel=1
pkgdesc="A suite of micro-benchmarks for testing various MVAPICH2 MPI operations (with compile-time optional CUDA support)."
arch=('i686' 'x86_64')
url='http://mvapich.cse.ohio-state.edu/benchmarks/'
license=('BSD')
depends=('mvapich2')
# Uncomment the next line if you need CUDA support
#depends=('mvapich2' 'cuda' 'nvidia-utils')
changelog=ChangeLog
source=("http://mvapich.cse.ohio-state.edu/benchmarks/${pkgname}-${pkgver}.tar.gz")
sha512sums=('468ce0acea826eaf88c1269ca8c2d5381a456e3b629a437a748376db38caca97f89c9dad8978e4482b3103cd7245f87697966372db4d679c746c7cda4835c16e')

build() {
	cd "${pkgname}-${pkgver}"

	if [ ${CARCH} == 'x86_64' ]; then
		_libdir='lib64'
	else
		_libdir='lib'
	fi

	#####################################################
	#
	# Without CUDA support
	#
	# Use the following configure command.
	#
	./configure --prefix=/usr --libexecdir=/usr/lib \
		CC=/opt/mvapich2/bin/mpicc
	#
	#
	#####################################################


	#####################################################
	#
	# With CUDA support
	#
	# Use the following configure command, and make sure that
	# the packages "cuda" and "nvidia-utils" are installed
	# BEFORE compiling.
	#
	# Read the documentation for more information:
	# https://scm.mvapich.cse.ohio-state.edu/svn/mpi-benchmarks/branches/4.3/README
	#
	#./configure --prefix=/usr --libexecdir=/usr/lib \
	#	--enable-cuda \
	#	--with-cuda-include=/opt/cuda/include \
	#	--with-cuda-libpath=/opt/cuda/${_libdir} \
	#	LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:/opt/cuda/${_libdir}" \
	#	CC=/opt/mvapich2/bin/mpicc
	#
	#####################################################

	make
}

check() {
	cd "${pkgname}-${pkgver}"
	make check
}

package() {
	cd "${pkgname}-${pkgver}"
	make DESTDIR="${pkgdir}" install
}
