silkrad: silkrad.o bsp.o cudabsp.o cudarad.o raytracer.o
	nvcc -m64 silkrad.o bsp.o cudabsp.o cudarad.o raytracer.o -std=c++11 -o silkrad -g -lcudart -lcudadevrt

bsp.o: bsp.cpp bsp.h
	nvcc -m64 bsp.cpp -O3 -I ./include -std=c++11 -c -g -arch=compute_35 -rdc=true

bsp_mingw.o: bsp.cpp bsp.h
	g++ bsp.cpp -I ./include -I "$(CUDA_PATH)/include" -Wall -Wextra -Wfatal-errors -Wno-unknown-pragmas -std=c++11 -o bsp_mingw.o -c -g

bsp_shared_mingw.o:
	g++ bsp_shared.cpp -I ./include -I "$(CUDA_PATH)/include" -Wall -Wextra -Wfatal-errors -Wno-unknown-pragmas -std=c++11 -o bsp_shared_mingw.o -c -g

silkrad.o: silkrad.cpp bsp.h
	nvcc -m64 silkrad.cpp -O3 -I ./include -std=c++11 -c -g -arch=compute_35 -rdc=true

cudabsp.o: cudabsp.cu cudabsp.h
	nvcc -m64 cudabsp.cu -O3 -I ./include -std=c++11 -c -g -arch=compute_35 -rdc=true

cudarad.o: cudarad.cu cudarad.h
	nvcc -m64 cudarad.cu -O3 -I ./include -std=c++11 -c -g -arch=compute_35 -rdc=true

raytracer.o: raytracer.cu raytracer.h
	nvcc -m64 raytracer.cu -O3 -I ./include -std=c++11 -c -g -arch=compute_35 -rdc=true

comparelumps.o: comparelumps.cpp bsp.h
	nvcc comparelumps.cpp -I ./include -Wall -Wextra -Wfatal-errors -std=c++11 -c -g

comparelumps: comparelumps.o bsp.o
	nvcc comparelumps.o bsp.o -Wall -Wextra -Wfatal-errors -std=c++11 -o comparelumps -g

examinebsp.o: examinebsp.cpp bsp.h
	g++ examinebsp.cpp -I ./include -Wall -Wextra -Wfatal-errors -std=c++11 -c -g

examinebsp: examinebsp.o bsp_mingw.o bsp_shared_mingw.o
	g++ examinebsp.o bsp_mingw.o bsp_shared_mingw.o -Wall -Wextra -Wfatal-errors -std=c++11 -o examinebsp -g

clean:
	-rm -f *.o
	-rm -f *.exe
	-rm -f silkrad
	-rm -f rad
	-rm -f *.out
	-rm -f comparelumps
	-rm -f examinebsp
