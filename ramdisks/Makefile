zip: cpio
	for i in out/*.cpio.gz; do n=out/`basename $$i .cpio.gz`.zip; ln -fs $$i boot.cpio.gz; zip -r $$n META-INF boot.cpio.gz; done
	rm -f boot.cpio.gz

cpio:
	mkdir -p out
	for i in cm-* stock; do cd $$i; find . | cpio -o -Hnewc | gzip -9 > ../out/$${i}.cpio.gz; cd ..; done

