.PHONY: installdeps srpm

installdeps:
	dnf -y install git autoconf automake make gettext-devel openssh-clients openssh-server python3-devel gcc

srpm: installdeps
	$(eval SUFFIX=$(shell sh -c " echo '.$$(date -u +%Y%m%d%H%M%S).git$$(git rev-parse --short HEAD)'"))
	mkdir -p tmp.repos/SOURCES
	autopoint
	autoreconf -ivf
	./configure
	make dist
	rpmbuild \
		-D "_topdir tmp.repos" \
		-D "release_suffix ${SUFFIX}" \
		-ts ./*.tar.gz
	cp tmp.repos/SRPMS/*.src.rpm $(outdir)
