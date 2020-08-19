CXX:=g++
object_files=$(addsuffix .o, $(basename $(filter-out runner.cpp,$(wildcard *.cpp))))

LDFLAGS:= -lgtest_main -lgtest -lpthread


.PHONY: test clean done runner

test: CXXFLAGS := -fPIC -g -O0
test: runner
	$(MAKE) clean
	./runner

done: CXXFLAGS := -O3 -fPIC
done: cache_info_final.o
cache_info_final.o: $(object_files)
	ld -r $^ -o $@

clean:
	rm -f *.o

runner: $(object_files) runner.o
	$(CXX) $(CXXFLAGS) $^ -o $@ $(LDFLAGS)

$(object_files): %.o: %.cpp
	$(CXX) $< $(CXXFLAGS) -c -o $@

runner.o: runner.cpp
	$(CXX) $(CXXFLAGS) $^ -c -o $@
