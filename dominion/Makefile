CFLAGS = -Wall -fpic -coverage -lm -std=c99 -ftest-coverage -fprofile-arcs

rngs.o: rngs.h rngs.c
	gcc -c rngs.c -g  $(CFLAGS)

dominion.o: dominion.h dominion.c rngs.o
	gcc -c dominion.c -g  $(CFLAGS)

playdom: dominion.o playdom.c
	gcc -o playdom playdom.c -g dominion.o rngs.o $(CFLAGS)

testDrawCard: testDrawCard.c dominion.o rngs.o
	gcc -o testDrawCard -g  testDrawCard.c dominion.o rngs.o $(CFLAGS)

badTestDrawCard: badTestDrawCard.c dominion.o rngs.o
	gcc -o badTestDrawCard -g  badTestDrawCard.c dominion.o rngs.o $(CFLAGS)

testBuyCard: testDrawCard.c dominion.o rngs.o
	gcc -o testDrawCard -g  testDrawCard.c dominion.o rngs.o $(CFLAGS)

testAll: dominion.o testSuite.c
	gcc -o testSuite testSuite.c -g  dominion.o rngs.o $(CFLAGS)

interface.o: interface.h interface.c
	gcc -c interface.c -g  $(CFLAGS)

unittestresults.out: unittest1.o unittest2.o unittest3.o unittest4.o cardtest1.o cardtest2.o cardtest3.o cardtest4.o
	rm unittestresults.out; for file in ????test?; do echo Running $${file} >> unittestresults.out; ./$${file} >> unittestresults.out 2>> unittestresults.out; gcov $${file}.gcda | grep "Lines executed" >> unittestresults.out; echo "" >> unittestresults.out; done
	
tests: unittest1.o unittest2.o unittest3.o unittest4.o cardtest1.o cardtest2.o cardtest3.o cardtest4.o randomtestadventurer.out randomtestcard.out testdominion.out

unittest1.o: unittest1.c dominion.o rngs.o
	gcc -o unittest1.o -g unittest1.c dominion.o rngs.o $(CFLAGS)

unittest2.o: unittest2.c dominion.o rngs.o
	gcc -o unittest2.o -g unittest2.c dominion.o rngs.o $(CFLAGS)

unittest3.o: unittest3.c dominion.o rngs.o
	gcc -o unittest3.o -g unittest3.c dominion.o rngs.o $(CFLAGS)

unittest4.o: unittest4.c dominion.o rngs.o
	gcc -o unittest4.o -g unittest4.c dominion.o rngs.o $(CFLAGS)

cardtest1.o: cardtest1.c dominion.o rngs.o
	gcc -o cardtest1.o -g cardtest1.c dominion.o rngs.o $(CFLAGS)

cardtest2.o: cardtest2.c dominion.o rngs.o
	gcc -o cardtest2.o -g cardtest2.c dominion.o rngs.o $(CFLAGS)

cardtest3.o: cardtest3.c dominion.o rngs.o
	gcc -o cardtest3.o -g cardtest3.c dominion.o rngs.o $(CFLAGS)

cardtest4.o: cardtest4.c dominion.o rngs.o
	gcc -o cardtest4.o -g cardtest4.c dominion.o rngs.o $(CFLAGS)

randomtestadventurer.out: randomtestadventurer.c dominion.o rngs.o
	gcc -o randomtestadventurer.out -g randomtestadventurer.c dominion.o rngs.o $(CFLAGS)

randomtestcard.out: randomtestcard.c dominion.o rngs.o
	gcc -o randomtestcard.out -g randomtestcard.c dominion.o rngs.o $(CFLAGS)

testdominion.out: testdominion.c dominion.o rngs.o interface.o
	gcc -o testdominion.out -g testdominion.c dominion.o rngs.o interface.o $(CFLAGS)

runtests: testDrawCard 
	./testDrawCard &> unittestresult.out
	gcov dominion.c >> unittestresult.out
	cat dominion.c.gcov >> unittestresult.out

player: player.c interface.o
	gcc -o player player.c -g  dominion.o rngs.o interface.o $(CFLAGS)

all: playdom player testDrawCard testBuyCard badTestDrawCard

clean:
	rm -f *.o playdom.exe playdom test.exe test player player.exe testInit testInit.exe *.gcov *.gcda *.gcno *.so *.out
