# You need to prepare a decomposeParDict
# FoamFile
# {
# 	format		ascii;
# 	class		dictionary;
# 	object		decomposeParDict;
# }
#
# numberOfSubdomains	8;
# method scotch;

.PHONY: pre ready run runall read recon show clean restore

NP ?= 8

pre:
	blockMesh
	checkMesh
	setFields -time 0

ready:
	decomposePar

run:
	mpirun -np $(NP) foamRun -parallel > log.foamRun 2>&1

runall:
	blockMesh
	checkMesh
	setFields -time 0
	decomposePar
	mpirun -np $(NP) foamRun -parallel > log.foamRun 2>&1

read:
	tail -f log.foamRun

recon:
	reconstructPar

show:
	paraFoam

clean:
	rm -rf -- ./0.0001

restore:
	@test -d ./back.bak || { echo "Error: back.bak is missing." >&2; exit 1; }
	find . -mindepth 1 -maxdepth 1 \
		! -name 'back.bak' \
		! -name '0' \
		! -name 'system' \
		! -name 'constant' \
		! -name 'Makefile' \
		-exec rm -rf -- {} +
	@if [ -d ./0 ]; then \
		find ./0 -mindepth 1 -maxdepth 1 -exec rm -rf -- {} +; \
	else \
		mkdir ./0; \
	fi
	cp -a ./back.bak/. ./0/
