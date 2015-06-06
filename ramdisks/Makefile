SUBDIRS=stock cm-10.1 cm-10.2 cm-11.0 cm-12.1

.PHONY: cpio cpio.gz zip clean

OUT=$(addprefix out/,$(SUBDIRS))
CPIO=$(addsuffix .cpio, $(OUT))
GZIP=$(addsuffix .gz, $(CPIO))
ZIP=$(addsuffix .zip, $(OUT))

CPIO += out/recovery.cpio

cpio: $(CPIO)
cpio.gz: $(GZIP)
zip: $(ZIP)

out:
	mkdir -p out

out/%.cpio: % | out
	cd $< && find . | grep -v .git | grep -v "~$$" | cpio -o -Hnewc > ../$@

out/%.cpio.gz: out/%.cpio
	gzip -k -9 $<

out/%.zip: out/%.cpio.gz
	ln -fs $< boot.cpio.gz
	zip -r $@ META-INF boot.cpio.gz
	rm -f boot.cpio.gz

clean:
	rm -f out/*cpio* out/*.zip
